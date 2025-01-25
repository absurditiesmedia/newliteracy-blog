---
publishDate: "23 January 2025"
title: Multi-Currency Self-Custodial Cryptocurrency Wallets 
description: I reviewed as many multi-currency self-custodial cryptocurrency wallets for desktop and found a pattern
tags: ["ethereum", "litecoin", "bitcoin", "monero", "cryptocurrency", "linux", "windows"]
coverImage:
    src: "../../assets/cryptocurrency.png"
    alt: "ethereum, monero, bitcoin, bitcoin cash and litecoin logos on a blue background with a question mark and a dollar sign to represent the confusion many have when trying to understand cryptocurrency, specifically all the different types and wallets."
---

I decided to take a look at a variety of cryptocurrency wallets for linux and windows. I am a huge beliver in the merits of a self-custodial wallet. No matter how big or transparent the provider, storing cryptocurrency where *ANYONE* else can access it, is not only a risk, it really just feels like it is entirely against the point. Anyway, I wanted to find an all-in-one solution to have the option to store my cryptocurrency, and I realized there just isn't that many great options, in fact, every piece of software that attempts to do this is essentially the same program over and over again. 

I feel like the most effective way to determine the investment potential of a specific coin is to look at the wallet software associated with it. 
Bitcoin and Monero have excellent wallet software. For bitcoin, you have **[Electrum](https://electrum.org)** and **[Sparrow](https://sparrowwallet.com/)**. Monero has it's own wallet software, **[Monero Wallet](https://getmonero.org/)**. Litecoin has **[Litecoin Core](https://litecoin.com/projects/core)**. Ethereum has **[geth or go-ethereum](https://geth.ethereum.org/)**. And these seem to work just fine. But if you want a solution for your desktop environment that allows you to store a variety of altcoins, the following wallet software are all essentially the same: 

- [Atomic Wallet](https://atomicwallet.io/)
- [Stack Wallet](https://stackwallet.com/)
- [Coinomi Wallet](https://www.coinomi.com/en/)
- [Exodus Wallet](https://www.exodus.com/)

If you want the tl;dr and just jump to my final reccmendation <a href="#tldr">skip to the conclusion</a>

Generally they work like this, you open the software, you're prompted to create or restore your wallet. Then you get a screen something like this, and all your altcoin wallets appear to be linked to your ethereum wallet. 

## Restore / Generate Wallet

![Atomic Restore/Generate Wallet](/images/crypto-wallets/atomic_restore.png)
Atomic wallet doesn't support BIP39 passphrase or 24 word seeds. Only the basic 12.

![Stack Restore/Generate Wallet](/images/crypto-wallets/stack_restore.png)
Stack wallet does support BIP39 passphrase and 24 word seeds. And it allows the creation of many wallets which can be open at the same time. This is a huge plus for Stack, take note of that.

![Coinomi Generate Wallet](/images/crypto-wallets/coinomi_new_wallet_24.png)
Coinomi new wallet screen. Notice that...

![Coinomi Restore Wallet](/images/crypto-wallets/coinomi_restore.png)
yes it1 supports BIP39 passphrase and 24 word seeds. But no on the multiple wallets. 

![Coinomi Gift Card Purchase Screen](/images/crypto-wallets/coinomi_got_it_backwards.png)
And what's up with the ability to purchase gift cards??? This is kind of weird because I've read people use stolen credit card numbers then buy gift cards which they seek out places to buy cryptocurrency with them so as to launder their stolen money. It seems somewhere along the way the association with gift cards and crypto made it to a developer as a feature request, but they got it backwards. LOL!!!

![Exodus Restore/Generate Wallet](/images/crypto-wallets/exodus_restore.png)
Exodus, like atomic does not support BIP39 passphrase or 24 word seeds.

## Send / Receive

Send and receive all pretty much look the same, what I **REALLY** did not like about any of these was the inability to generate multiple addresses. This is SO IMPORTANT FOR TRACKING WHERE FUNDS ARE COMING FROM. And if people expect large scale adoption of cryptocurrency to ever take place, this is such an important feature for so many reasons. Merchants can use this to track where customers are coming from. It may even be possible to use unique addresses to track inventory in a brick and mortar store. Disposable and many addresses are an incredibly important feature for any wallet. 

![Atomic Send](/images/crypto-wallets/atomic_send_eth_screen.png)
Atomic Sending Ethereum

![Atomic Receive](/images/crypto-wallets/atomic_recv_eth_screen.png)
Atomic screen for obtaining address to receive 

![Stack Send](/images/crypto-wallets/stack_send_eth_screen.png)
Stack screen for sending Ethereum.

![Stack Receive](/images/crypto-wallets/stack_recv_eth_screen.png)
Stack screen for obtaining address to receive.

![Coinomi Send](/images/crypto-wallets/coinomi_send_eth_screen.png)
Coinomi screen for sending Ethereum.  

![Coinomi Receive](/images/crypto-wallets/coinomi_recv_eth_screen.png)
Coinomi screen for obtaining address to receive.

![Exodus Send](/images/crypto-wallets/exodus_sendeth_screen.png)
Exodus screen for sending Ethereum.  

![Exodus Receive](/images/crypto-wallets/exodus_recveth_screen.png)
Exodus screen for obtaining address to receive.

## Coin Swap
This is a nice feature, which all of the wallets have. No doubt with an affiliate account associated. To be fair, there wouldn't really be a need for a self-custodial wallet that supports all of these altcoins without those exchanges. None of the altcoins would have ever gotten off the ground. So it makes sense these wallets would be developed with the promise of a cut of the tiny percentages that occur with every swap. I'm tempted to create my own variation on this theme. 

![Atomic Swap Currency](/images/crypto-wallets/atomic_swap_screen.png)
Atomic Currency Swap/

![Stack Swap Currency](/images/crypto-wallets/stack_swap.png)
Stack Currency Swap. Notice you're given the option to select the exchange. The other programs don't have such an option

![Coinomi Swap Currency](/images/crypto-wallets/coinomi_swap_screen.png)
Coinomi Currency Swap

![Exodus Swap Currency](/images/crypto-wallets/exodus_swap_screen.png)
Exodus Currency Swap


## Stake Your Coins for Profit?
Here is where the apps actually diverge, and again, this is clearly affiliate marketing at play here. 

Atomic allows you to stake your crypto for gains. You'll probably want to research it more before you do this, but who knows. Magic internet money is just that. Magic. Same as regular money, it's just not controlled centrally so its still possible for regular people to hit it big. Everyone knows with regular money that's resevered for people with over 100 years of extreme generational wealth. No, it's not just millions, barely 10s of millions. More like 100s of millions. And that's probably not you or anyone you know. And if it is. Here's my bitcoin address: 

![bc1qy2tqwljvv85uppxmlmnxmqlpc7dpaqe87h2ywm](/images/crypto-wallets/bitcoin-address.png)

<span style="font-size:2em; font-family:monospace;">bc1qy2tqwljvv85uppxmlmnxmqlpc7dpaqe87h2ywm</span>

You'll never miss a few... hundred thousand.  

![Atomic Stake Coins](/images/crypto-wallets/atomic_stake_coins_for_percent_per_year.png)


## Open Source? 
All of the organizations behind these wallets have some kind of source code available on github, but it appears the only one to have the entire application available is stack wallet. Part of the whole reason one would want to have a self-custodial wallet is a matter of trust and, to me, there's no better way to show trustworthiness than transparency. And with softeware, this means opening all of your source code. 

Here are the links to the github pages for each of these programs, you be the judge
[Exodus](https://github.com/ExodusMovement)
[Coinomi](https://github.com/coinomi/)
[Stack](https://github.com/cypherstack)
[Atomic](https://github.com/Atomicwallet)

<a name="tldr"></a>
## Conclusion
And there you have it. If you need a place to store altcoins, this is the way to go, but for the major coins... the ones you actually want to hold: Bitcoin, Litecoin, Monero, Ethereum. Stick with the software that's developed for them. 

But if you want my opinion on which of these four applications has the best features, I'm personally going to have to say [Stack](https://stackwallet.com/) or [Coinomi](https://www.coinomi.com/) for the following reasons:

| Feature                                 | Stack | Coinomi   | Atomic    | Exodus    |
| :-----------------------------------    | :---: | :-------: | :-------: | --------- |
| 24 word seeds.                          |   X   |   X       |           |           |
| BIP39 passphrase.                       |   X   |   X       |           |           |
| muliple wallets                         |   X   |           |           |           |
| Mutple exchanges                        |   X   |           |           |           |
| Tor support                             |   X   |           |           |           |
| All source code online                  |   X   |           |           |           |
| Support for a wider variety of altcoins.|       |   X       |   X       |   X       |



