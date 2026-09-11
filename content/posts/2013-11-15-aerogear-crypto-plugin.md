---
layout: post
title: AeroGear Crypto Plugin
date: '2013-11-15T04:56:00.000-08:00'
author: Erik Jan de Wit
tags:
- aerogear
- crypto
- plugins
- cordova
modified_time: '2013-11-15T04:56:33.050-08:00'
blogger_id: tag:blogger.com,1999:blog-236071318451058546.post-4847237411390466999
blogger_orig_url: http://blog.nerdin.ch/2013/11/aerogear-crypto-plugin.html
---
One of our feature that is nearing completion is crypto. Even though we have Javascript support for this feature, we decided that we would create a Cordova Plugin for this as well. With a Plugin we can use the native libraries and by doing so we add a bit more security and more importantly we improve speed. I've tried to stay as close as possible to the Javascript API, but Cordova demands us to work asynchronous so I've ended up with something that is not exactly the same:

```js
//Password based key derivation support (PBKDF2)
AeroGear.Crypto().deriveKey( function(password) {
    console.log(password);
}, errorHandler, PASSWORD );

//Symmetric encryption support (GCM)
//Encryption:
var agCrypto = new AeroGear.Crypto();
agCrypto.deriveKey( function(rawPassword) {
    var options = {
            IV: "69696ee955b62b73cd62bda875fc73d68219e0036b7a0b37",
            AAD: "feedfacedeadbeeffeedfacedeadbeefabaddad2",
            key: rawPassword,
            data: "My Bonnie lies over the ocean, my Bonnie lies over the sea"
        };
    agCrypto.encrypt( function(cipherText) {
        console.log(cipherText)
    }, options );
}, errorHandler, 'myPassword' );

//Decryption:
var options = {
        IV: "69696ee955b62b73cd62bda875fc73d68219e0036b7a0b37",
        AAD: "feedfacedeadbeeffeedfacedeadbeefabaddad2",
        key: rawPassword,
        data: cipherText
    };
agCrypto.decrypt( function(text) {
    console.log(text)
}, options );

//Asymmetric encryption support (ECC) / iOS not supported
agCrypto.KeyPair(function(keyPair) {
    agCrypto.KeyPair(function(keyPairPandora) {
        var options = {
            IV: "69696ee955b62b73cd62bda875fc73d68219e0036b7a0b37",
            AAD: "feedfacedeadbeeffeedfacedeadbeefabaddad2",
            key: new agCrypto.KeyPair(keyPair.privateKey, keyPairPandora.publicKey),
            data: "My bonnie lies over the ocean"
        };
        agCrypto.encrypt(function (cipherText) {
            options.key = new agCrypto.KeyPair(keyPairPandora.privateKey, keyPair.publicKey);
            options.data = cipherText;
            agCrypto.decrypt(function (plainText) {
                console.log(plainText);
            }, options);
        }, options);
    });
});
```

For more information about the features that are coming have a look on the [site](http://aerogear.org) and on the [plugin github page](https://github.com/edewit/aerogear-crypto-cordova)

Let us know if you like the features so far and what features you would like to see next.