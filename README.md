### HD Wallet

A generic HD wallet for Elliptic Curve (Secp256k1) and (WIP) Edwards-curve (Ed25519) based crypto currencies like Bitcoin, Ethereum, Cosmos, Tezos, Tron, Cardano and more.  
HD wallets can be generated from mnemonic (w/ or w/o passphrase) or from extended private key (xprv) and non-hd wallets can be generated from private key.  

HD wallets can derive sub accounts, and from that accounts external (deposit) wallets or internal (change) wallets can be derived. Using generated wallets, addresses can be retrived by implementing address generators for related crypto currency. 

By using HDWallet.Secp256k1 project, any Elliptic Curve (Secp256k1) based crypto currency wallet can be generated with defining purpose (e.g. BIP44) and coin type (e.g. 195 for Tron).  
HDWallet.Tron project is already ready to go HD wallet for Tron (TRX) which uses HDWallet.Secp256k1 project.  

(WIP) By using HDWallet.Ed25519 project, any Edwards-curve (Ed25519) based crypto currency wallet can be generated by defining purpose (e.g. BIP44) and coin type (e.g. 1852 for Cardano).     

#### Samples  
Sample for generating Secp256k1 HD Wallet for Bitcoin (purpose: BIP44, coin type: 0) from mnemonic and getting the first account's first deposit wallet;  
```csharp
IHDWallet<BitcoinWallet> bitcoinHDWallet = new BitcoinHDWallet("conduct stadium ask orange vast impose depend assume income sail chunk tomorrow life grape dutch", "");
var depositWallet0 = bitcoinHDWallet.GetAccount(0).GetExternalWallet(0);        
var address = depositWallet0.Address;
```  

Sample for generating HD Wallet (m/44'/0'/0') from extended private key;  
```csharp
var accountExtendedPrivateKey = "xprv9xyvwx1jBEBKwjZtXYogBwDyfXTyTa3Af6urV2dU843CyBxLu9J5GLQL4vMWvaW4q3skqAtarUvdGmBoWQZnU2RBLnmJdCM4FnbMa72xWNy";
IAccountHDWallet<BitcoinWallet> accountHDWallet = new AccountHDWallet<BitcoinWallet>(accountExtendedPrivateKey, 0);

var depositWallet0 = accountHDWallet.Account.GetExternalWallet(0);
```

Sample for signing messages with generated wallets;  
```csharp
...
var signature = depositWallet0.Sign(messageBytes);
```