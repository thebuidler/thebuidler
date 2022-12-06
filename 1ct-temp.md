# Overview

One-click trading (1CT) is a feature that removes the need to interact with a wallet when submitting transactions, reducing the time to trade. 
It does this through the use of two new mechanisms:
* 1CT wallet
* Trade delegation

# 1CT Wallet

gTrade uses a derived EOA wallet for submitting trading transactions. 

It relies on the following sequence:
1. Trader provides a 4 digit PIN
    * This pin should be remembered for future recovery
2. Trader signs a prefixed message of the PIN using their wallet
    * The wallet used to sign the message should be remembered for future recovery
3. gTrade website generates an Secp256k1 key pair using the signed message as a seed
4. gTrade website encrypts and stores the key material on the local device

> Key material is deterministic meaning it can be replicated. Pin + personalSign gives strong security guarantees while allowing a trader to recover material if lost. A trader can also use this to prevent storing on device between trading sessions (clear and regenerate for each session).

Once a trader creates a 1CT wallet, they must grant it permissions to trade on their behalf by approving it as a delegate.

# Trade Delegation

gTrade smart contracts support a delegation feature, allowing EOAs to submit transactions on behalf of other EOAs.

To delegate trading to another EOA, a trader must approve the address as a delegate through the trading contract. 

A delegation wallet only needs gas funds for submitting transactions, as collateral and PnL are tied to the trader address.

Supported actions:
* Open a trade
* Open an order
* Cancel an order
* Update stop loss
* Update take profit
* Close a trade

The 1CT wallet is a delegation wallet.

# Onboard

gTrade offers an onboarding experience for all of the above
1. Create PIN
2. Sign message
3. Approve 1CT wallet
4. Fund 1CT wallet
5. Enable feature


# Manage

Once a trader has onboarded, they may manage the feature under the accounts dropdown
A place to
* Enable/disable the feature
* Fund 1CT wallet
* Withdraw all funds from 1CT wallet
* Export private key
* Reset/wipe all 1CT data


# Use

Once onboarded, a trader may enable the feature and use their normal trading workflows. At this point there is nothing different other than not having to confirm transactions in a wallet.

# Transactions

Because 1CT wallet is managed by the site, transaction management is taken in-house. This provides a place to track transactions and interact if they're stuck by speeding up or canceling. 

# FAQ

### Is the 1CT wallet key material stored somewhere? 
Only on your device. You can wipe it using "Reset" whenever you choose.

### I wiped my device storage, is my 1CT wallet gone?
Yes but you can restore it by using the same PIN and wallet when re-generating.

### Are trades opened against my 1CT wallet?
No, they are opened against your connected wallet.

### Do I have to have 1CT enabled to interact with trades I opened with it? 
No, you may toggle the feature on and off whenever you'd like.

### Can I use the same 1CT wallet on multiple devices?
Yes, as long as you use the same PIN and wallet while generating.

### Can I use the same 1CT wallet for multiple accounts?
Yes, you may delegate to your 1CT wallet with any connected wallet.

### Can I have multiple 1CT wallets?
For each account you use to trade, you may have one delegate. The recommended setup is to use the same 1CT wallet for all trading accounts.

### What if my transaction is stuck?
In the accounts dropdown, you'll find a transactions list. Here you may speed up and/or cancel a stuck transaction.

### Do I have to have key material stored on device?
No, you can re-create your 1CT wallet and reset it at the end of each trading session. Just use the same PIN and wallet to sign.
