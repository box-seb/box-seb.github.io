---
layout: post
title:  "FIDO and WebAuthn"
date:   2022-06-21 12:13:04 +1200
---


[FIDO](https://fidoalliance.org/) Fast IDentity Online alliance is focused on simpler and stronger authentication, password elimination.

Published [white paper](https://fidoalliance.org/white-paper-multi-device-fido-credentials/) about multi device fido credentials

Its mission is to `help reduce the world’s over-reliance on passwords.`

On a very high level WebAuthn as described in more detail [here](https://webauthn.guide/)
- The solution uses public and private key
- Public key is stored by the service used by users
- Private key is stored only on user's device and kept secret
- When user authenticates they private key to sign the information sent to the service
- Service upon receiving signed message verify the signature
- If signature is valid then it must be provided by authenticated device

The key information here is that the private key is stored securely on user's device. Up to the point that it is impossible to extract it, what makes it very secure.

This benefit is as well a difficulty because it makes it impossible to use multiple devices to authenticate the same identity and in case of loosing the device it is hard to recover.

There are 2 types of authenticators used by FIDO:
- Platform authenticator - integrated with a device, capable of capturing an authentication factor. Examples are Touch ID, Face ID, Windows Hello - they are often biometric but not always. These devices usually have trusted platform module [TPM](https://en.wikipedia.org/wiki/Trusted_Platform_Module).
- Roaming authenticator - also called cross platform authenticators, i.e. physical security keys, smartphones. They present user's claim to another device. They are not part of the same platform as primary device. These devices allow access into laptop, service or app running on the primary device, such as laptop.


FIDO propose changes to address the gaps related with authentication mobility:
- Using phones as roaming authenticators. The proposal uses Bluetooth to communicate between user's phone and the device from which user is trying to authenticate. Thanks to the close proximity required by Bluetooth this is resistant to phishing attack. Phone becomes a hardware security key.
- Support for multi device authentication. It is expected that FIDO authenticator vendors adapt their implementation that it can `survive device loss`. It means that when user set up credentials on one phone those should be also available on user's new phone. The expectation is that on the new device user just need to pass the built in biometric challenge.

Sometimes FIDO credentials are called `passkeys` especially when they are multi device credentials.
The underlying platform, similar to password managers, synchronize the cryptographic keys that belong to credentials from ond device to another. This means that security and availability of of user's credentials depends on the security of the underlying platform. The security of the FIDO credentials is depends on the authentication mechanism for their online accounts on those platform. 

When FIDO credentials can't be synchronized because a new device comes from a different platform vendor the access to the service or app can be achieved via aforementioned Bluetooth protocol and secondary device (roaming authenticator) that is already equipped with required credentials.

FIDO2 for dotnet can be found [here](https://github.com/passwordless-lib/fido2-net-lib)