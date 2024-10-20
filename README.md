# react-native-rsa
A library which provides cryptographic functions to React Native. This library is compatible with Expo, no ejection required.

## Use Case
Other similar libraries either do not provide key generation functionality or are not compatible with Expo. This library solves both problems.

## Examples

#### Installation
```
npm install react-native-rsa
```

#### Key Generation
```
const RSAKey = require('react-native-rsa');
const bits = 1024;
const exponent = '10001'; // must be a string. This is hex string. decimal = 65537
const rsa = new RSAKey();
rsa.generate(bits, exponent);
const publicKey = rsa.getPublicString(); // return json encoded string
const privateKey = rsa.getPrivateString(); // return json encoded string
```

#### Encryption
```
const rsa = new RSAKey();
rsa.setPublicString(publicKey);
const originText = 'sample String Value';
const encrypted = rsa.encrypt(originText);
```

#### Decryption
```
rsa.setPrivateString(privateKey);
const decrypted = rsa.decrypt(encrypted); // decrypted == originText
```

Tested works with ursa in nodejs (with ursa padding set to PKCS1).

## Credits
This library uses Tom Wu's jsbn http://www-cs-students.stanford.edu/~tjw/jsbn/.
The original creator of this library is https://github.com/z-hao-wang/. The original URL is https://github.com/z-hao-wang/react-native-rsa. I (Michael Rothkopf) have updated the documentation and plan on updating the NPM version to include updated functionalities.

## TODO
If you would like to contribute, please create a pull request. Currently, the library is missing PEM handling.

## Known issues:
* NodeJS may complain about 'window' is not defined. I commented out the lines referencing 'window' in rng.js without issue. (It looked like it just added some extra randomness. It should still work without that part, though may be less cryptographically secure.) I don't recommend using this library with NodeJS. I'd use ursa or node-rsa.
