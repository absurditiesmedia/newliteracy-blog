---
publishDate: "19 Jul 2025"
title: Secrets Management DevOps Tools and More
description: Encryption keys and database passwords are necessary for deploying web apps, but where to store them?
tags: [ "devops", "security"]
---

These tools provide a means of securely storing secrets (encryption keys, passwords, all that good stuff that you want to make available to your production systems, but you must protect from exposure) I started my research with [This Reddit Post](https://www.reddit.com/r/devops/comments/15zw4dp/so_what_are_you_all_using_for_secret_management/)

## Simple Tools

💫 [SOPS: Simple and flexible tool for managing secrets: getsops.io](https://getsops.io/) | [SOPS: github](https://github.com/getsops/sops): SOPS allows the encryption of secrets directly in the configuration files from which your applications load them. Using SOPS, secrets are decrypted at runtime.

👉 using SOPS is kind of a pain, but it doesn't involve relying on any external webservices. It supports encrypting secrets using PGP [(and that got me stuck on looking at all...](#post-quantum-cryptography). It works as follows.

👉 create a `sops.yaml` file in the root of your project, this file will at minimum need to specify the fingerprint for the pgp key you'll use to encrypt secrets. It supports other methods... but why? I'm not interested.

```yaml
    creation_rules:
  - path_regex: ./*
    pgp: 'FA2A456F0B079A46CDE2E2275D2D'
```

👉 move your `.env` file variables into a `json` file, converting the list of variables to a dictionary.

```json
#env.json
{"SECRET1":"SECRET1VAL", "SECRET2":"SECRET2VAL", ... "SECRETN":"SECRETNVAL"}
```

👉 run `sops encrypt env.json > env.enc.json` which will encrypt the individual values within the file. Take a look.

👉 run `sops exec-env env.enc.json <your app launch command>` any application launched with `sops exec-env <encrypted secrets file>` will have environment variables defined for each key in the json array... which is why we converted our .env variables to json keys. To use this, make sure your app doesn't specifically need the .env file. I got some warnings that I think came from python dotenv, but it all seems to be working fine anyway.

---

🤢 [pass the standard unix password manager](https://www.passwordstore.org/) bleh... 

## Components of Larger Software Packages

🪐 [Portainer.io: Container management for Docker and Kubernetes with a built in system for managing secrets](https://portainer.io) | [How to create and manage Kubernetes Secrets in Portainer](https://www.techrepublic.com/article/portainer-manage-kubernetes-secrets/)

🪐 [Ansible Vault](https://docs.ansible.com/ansible/latest/vault_guide/index.html)

## Webservice Based Solutions

😐 [Arctera Enterprise Vault](https://www.arctera.io/enterprise-vault)

⛔ [VaultPlusPlus](https://vaultplusplus.com/): looks promising, but command is provided binary only and it doesn't seem to work on my fedora kinoite system

🧐 [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/)[$0.40 per secret/month, $0.05 per 10k API Calls](https://aws.amazon.com/secrets-manager/pricing/) so pretty reasonable... except my newest app has like a dozen secrets at least. There are free options below that will be much less expensive,but less full-featured.

🤦 [1password.com](https://1password.com/developers/secrets-management): User Account is 2.99, but I think the $19.99 package is necessary to access the secrets management for web applications.

⚠️ [Evervault](https://docs.evervault.com/getting-started/encryption-101): [Free edition limited to 500 decrypts/mo](https://evervault.com/pricing) which, depending on how your project is coded, could be plenty or not nearly enough

---

✅ 👌😎🧸 [Infisical](https://infisical.com/): [Free edition is entirely usable](https://infisical.com/pricing)

👉🤛 [Using infisical](https://infisical.com/docs/cli/usage):fairly simple cli usage,

‍👉 first install (rpm, apt, or npm),

👉 go to the directory for the project where you want to create an association with an infisical project, run`infisical init` and choose the appropriate project

👉 now you can prefix any command with `infisical run --env=<dev,staging,production> --path=/path/to/application <application start command>`.

👉 Alternately, you can run `infisical secrets --env=<dev,staging,production>` and it will print out a table `SECRET NAME | SECRET VALUE | SECRET TYPE`.

---

✅ 🚀🔮🪐[Doppler](https://www.doppler.com/): [Free edition is entirely usable](https://www.doppler.com/pricing): similar cli usage to Infisical.

🧿 first install (rpm, apt, or shell-script -for the shell-script option on fedoria ostree based installs, you must save install.sh and edit it setting USE_PACKAGE_MANAGER=0 then run it as root)

💫 run `doppler login` to get a token

☄️ go to the directory for the project where you want to create an association with a doppler project and run `doppler setup` and choose the appropriate project

🌌 now you can prefix any command with `doppler run --command=` for example, the simplest case, to verify the secrets are accessible, if you created a secret called `TEST_SECRET` run `doppler run --command="echo \$TEST_SECRET"` it should print the secret value to the screen demonstrating that it is now available as an environment variable.

---

⚠️🤦[Hashicorp Vault](https://www.hashicorp.com/en/products/vault): Was Free, now Requires Hasicorp Dedicated 💵$400+/month.

😐 [Pulumi IaC ESC](https://www.pulumi.com/docs/esc/get-started/) : Pulumi is an infratructure as Code Provider.

## Summary

In experimenting with the reccomendations from the [reddit post](https://www.reddit.com/r/devops/comments/15zw4dp/so_what_are_you_all_using_for_secret_management/) I found [Doppler](https://www.doppler.com/) and [Infisical](https://infisicial.com) to be the best webservice options... really the only useable ones.

---

### Ubiq: Encryption for Everything

Not exactly a secrets manager, but an interesting service that I feel like mentioning anyway. Designed to be very easy to implement so that no sensitive data need be left unencrypted at rest.

[UBIQ](https://www.ubiqsecurity.com/) It might be possible to setup a workflow using ubiq for secrets management since it provides such generic access to encryption.

---

### Post Quantum Cryptography

<a name="post-quantum-cryptography"></a>

and that got me stuck on looking at all... the new encryption types that have appeared in the latest version of `gnupg`. unfortunately none are quantum safe, even though it sounds like the algorithms exist.

🔮 [Post Quantum Cryptography PQC](https://en.wikipedia.org/wiki/Post-quantum_cryptography)

👨‍💻 [Shor's Algoritm](https://en.wikipedia.org/wiki/Shor%27s_algorithm): theoretically capable of defeating all traditonal assymetric key encryption given sufficient quantum computing resources. (RSA, and all variations of the elliptic-curve) because of its potential to be able to factor large numbers. Not proven yet, but theoretical possibility is probable enough to warrant the development of new methods for genration asymmetric keypairs. So far the following have been proposed:

Post-quantum cryptography research is mostly focused on six different approaches:  

🔏 [Lattice Based Cryptography](https://en.wikipedia.org/wiki/Lattice-based_cryptography)

🔑 [Multivariate cryptography](https://en.wikipedia.org/wiki/Multivariate_cryptography)

🗝 [Hash Based Cryptography](https://en.wikipedia.org/wiki/Hash-based_cryptography)

💻 [Code-based cryptography](https://en.wikipedia.org/wiki/McEliece_cryptosystem)

🔢 [Isogeny-based cryptography](https://en.wikipedia.org/wiki/Isogeny)

🔐 [Symmetric key quantum resistance](https://docbox.etsi.org/Workshop/2013/201309_CRYPTOS03_INDUSTRY_SESSION/PITNEYBOWES_PINTSOV.pdf)

🕵🛡️ **Hybrid encryption** is often recommended, where data is encrypted with both a new Post Quantum Encryption Technology as well as an existing proven non Post Quantum encryption technology like ed25519. This way if the new algorithm turns out to be vulnerable to a non-quantum attack, then the data will be protected by the well tested, but not quantum safe algorithm. This is a good idea since there is a lot of risk with the new algorithms simply because they are that new.
