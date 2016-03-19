# helpeth

Help (with) Ethereum. Purists' commandline tool for key and transaction management.

It uses [ethereumjs-wallet](https://github.com/axic/ethereumjs-wallet) and [ethereumjs-tx](https://github.com/ethereumjs/ethereumjs-tx).

## How to use

Install it as a global package: `npm install -g helpeth`

See the help output with `helpeth --help`:

```
Usage: helpeth [command]

Commands:
  signMessage <message>                     Sign a message
  createTx <nonce> <to> <value> <data>      Sign a transaction
  <gasLimit> <gasPrice>
  parseTx <tx>                              Parse raw transaction
  keyGenerate [format]                      Generate new key
  keyConvert                                Convert a key to V3 keystore format
  keyDetails                                Print key details
  addressDetails <address>                  Print details about an address

Options:
  -p, --private      Private key as a hex string                        [string]
  --password         Password for the private key                       [string]
  --password-prompt  Prompt for the private key password               [boolean]
  -k, --keyfile      Encoded key file                                   [string]
  --show-private     Show private key details                          [boolean]
  --version          Show version number                               [boolean]
  --help             Show help                                         [boolean]
```

## Examples

### Generate a new key

```
$ ./helpeth keyGenerate
Address: 0xe0defb92145fef3c3a945637705fafd3aa74a241
Address (checksum): 0xe0DefB92145FeF3c3a945637705fAfd3AA74a241
ICAP: XE82 Q9ML VOQY V5TD N4MF MK9U KKHS JU9N 9S1
Public key: 0x93e39cde5cdb3932e204cdd43b89578ad58d7489c31cbc30e61d167f67e3c8e76b9b2249377fa84f73b11c68f2f7a62f205f430f3a4370fd5dab6e3139d84977
Private key: 0xba1488fd638adc2e9f62fc70d41ff0ffc0e8d32ef6744d801987bc3ecb6a0953
```

### Generate a new key and save as V3 keystore file

```
$ ./helpeth --password 'Use --password-prompt instead for security' keyGenerate v3
Address: 0x15f2f3e0f2d74ea7b185fc12f24cb4f402cc96d0
Address (checksum): 0x15F2f3e0F2D74eA7B185fC12F24cB4F402cC96D0
ICAP: XE53 2KAS Y050 UIFI VB1J 2636 IKXC 4QIP SK0
Public key: 0xf2a3a694026ed4abb16e18f0421a6e667803399dad2eae2ca8c3f95934fcb46e9440183fd278181deb501d2f0766d0f676d0cac84da3632590e2978cb6883bc4
Key saved as UTC--2016-03-17T19-06-57.064Z--15f2f3e0f2d74ea7b185fc12f24cb4f402cc96d0
```

### Print details of an existing keyfile

```
$ ./helpeth --password 'Use --password-prompt instead for security' --keyfile UTC--2016-03-17T19-06-57.064Z--15f2f3e0f2d74ea7b185fc12f24cb4f402cc96d0 --show-private keyDetails
Address: 0x15f2f3e0f2d74ea7b185fc12f24cb4f402cc96d0
Address (checksum): 0x15F2f3e0F2D74eA7B185fC12F24cB4F402cC96D0
ICAP: XE53 2KAS Y050 UIFI VB1J 2636 IKXC 4QIP SK0
Public key: 0xf2a3a694026ed4abb16e18f0421a6e667803399dad2eae2ca8c3f95934fcb46e9440183fd278181deb501d2f0766d0f676d0cac84da3632590e2978cb6883bc4
Private key: 0x71a7f0e2ef1b7ff501b65a1650d48b8d5521fadc9539eec146d4faa6f5ca9aca
```

### Sign a message

```
$ ./helpeth --password 'Use --password-prompt instead for security' --keyfile UTC--2016-03-17T19-06-57.064Z--15f2f3e0f2d74ea7b185fc12f24cb4f402cc96d0 signMessage 'Hello World'
Input message: Hello World
Message hash (Keccak): 0x592fa743889fc7f92ac2a37bb1f5ba1daf2a5c84741ca0e0061d243a2e6707ba
The signature: 0x167760997a69e225c0668e6761cd20cac70f3a6ace29fe2d287c3003daf6972b10d158a47e8f064cf982a3defdf236247c41249dbfb0fb81f0d126c26a94971d01
```

### Sign a transaction

```
$ ./helpeth --password 'Use --password-prompt instead for security' --keyfile UTC--2016-03-17T19-06-57.064Z--15f2f3e0f2d74ea7b185fc12f24cb4f402cc96d0 createTx 0x1 0xe0defb92145fef3c3a945637705fafd3aa74a241 0x2710 0x0 0x4208 0x42817c800
Nonce: 0x01
To: 0xe0defb92145fef3c3a945637705fafd3aa74a241
Value: 0x2710
Data: 0x00
Gas limit: 0x4208
Gas price: 0x042817c800
The signed transaction: 0xf8660185042817c80082420894e0defb92145fef3c3a945637705fafd3aa74a241822710001ba0909bb38d67799654ea53d3c05b839aa5f12f1f9e96205125d30a326a74eedd95a0634ee974baa4930dd4a943e392dcd526186531e20fb116ead9c0c10c520e3703
```

## License

MIT License

Copyright (C) 2016 Alex Beregszaszi
