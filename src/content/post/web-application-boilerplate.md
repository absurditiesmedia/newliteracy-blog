---
publishDate: "22 July 2025"
title: Web Application Boilerplate
description: a good starting point for any complex web application
tags: ["development", "devops"]

---
I've been tinkering with a number of projects and along the way I've come up with what I think is a solid starting point for any web application that you might build. 

Understanding that your application will be made up of multiple moving parts, it seems a good starting point to create a `docker-compose.yaml` where you can define each of the components that will make up your application. 
At the minimum, you'll probably define a volume for your database data, and name and define a subnet for your app's network.

```
services:
  your-app-db:
    ...
  your-app-backend:
    ...
  your-app-frontend:

volumes:
  your-app-db-vol
network:
  your-app-net:
    driver: bridge
    ipam:
      config:
        - subnet: 172.30.0.0/16
```

Another thing that almost every web application will need to handle is environment variables and secrets. You may as well get this out of the way from the start. I reviewed a number of webservices that provide secrets management, and they're nice, but ultimately I found [`sops`](https://github.com/getsops/sops) which uses pgp keys to encrypt your secrets and can be run locally to be the best solution.

You may as well treat all your environment variables as secrets for this process, it's much simpler that way. 

Create a json file that stores all your environment variables, I named mine `env.json` 

```
{
'POSTGRES_USER':'postgresuser',
'POSTGRES_DB':'yourappdb',
'POSTGRES_PASSWORD':'a strong password',
...
...
...
'JWT_ES256_PRIVATE_KEY':"-----BEGIN EC PRIVATE KEY-----\nJDKELCVlejks02...
'JWT_ES256_PUBLIC_KEY':"-----BEGIN EC PUBLIC KEY-----\nFkdKGdfS3S...
}
```
Now, you'll want to be sure to add a line for `env.json` to your project's `.gitignore` file to make sure you don't commit secrets to the repository.

next you'll need to supply a `.sops.yaml` file that tells `sops` which pgp key to use for your project. This file should contain something like:
```
creation_rules:
  - path_regex: ./*
    pgp: '[REPLACE WITH THE FINGERPRINT OF A PGP KEY YOU WANT TO USE TO ENCRYPT YOUR SECRETS]'
```

Now once you've got that in place, to encrypt the values in your `env.json` you'll run the command:

`sops -e env.json > env.encrypted.json`

This will create a new file `env.encrypted.json` that has the keys from the original, but the values have been encrypted.

And to make these available as environment variables run:

`sops exec-env env.encrypted.json /usr/bin/bash`

and a new shell environment will be opened with the values from your `env.json` all avalable as environment variables. Have a look

`printenv`

You can also use the above command to directly lanch parts of your application, and this is most likely how you would use this in production:

`sops exec-env env.encrypted.json ./entrypoint.sh`

The important part is that it is safe to commit `env.encrypted.json` to your project git repository as the secrets have been encrypted.

Notice I listed a public and private key, it is likely that your application will make use of user authentication, and for that you'll proabaly want to use JSON Web Tokens somewhere in your application. As far as I can tell, the most secure way of handling these involves encrypting them using ellipic curve assymetric key encryption. So for that, you'll need to generate a keypair. 
This is how you generate that keypair. 

```
openssl ecparam -name  prime256v1 -genkey -noout -out private.pem
openssl ec -in private.pem -pubout -out public.pem 
```
Then you can replace the newlines with `\n` and paste them into your env.json using whatever environment variable name fits your implementation.

Finally, to wrap everything up, you might consider creating a **Makefile** where you can store (and self-document) all the commands necessary for administration of your application.

```
.PHONY: sops-encrypt sops-load db-up db-down db-nuke 
CONTAINER_HANDLER=podman
COMPOSE_FILE=docker-compose.yaml
DB_CONTAINER=your-app-db
DB_VOLUME=your-app-db-vol
ENV_SOURCE_FILE=./env.json
ENCRYPED_ENV_FILE=./env.encrpted.json

sops-encrypt:
	@echo "Encrypting the .env file"
	sops -e $(ENV_SOURCE_FILE) > $(ENCRYPED_ENV_FILE)

sops-load:
	@echo "Decrypting into session"
	sops exec-env $(ENCRYPED_ENV_FILE) /usr/bin/zsh

db-up:
	@echo "📦 Brining up database container..."
	$(CONTAINER_HANDLER) compose --file=$(COMPOSE_FILE) up --build $(DB_CONTAINER)
	@echo "✅ Done!"

db-down:
	@echo "🛑 shutting down database"
	$(CONTAINER_HANDLER) compose  --file=$(COMPOSE_FILE) down $(DB_CONTAINER)
	@echo "💤 Done!"

run-backend:
  @echo "running backend"
   ...
run-frontend:
  @echo "running frontend"
    ...
```

And that's it. I hope you find this as useful as I have.
