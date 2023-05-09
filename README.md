# ChefBook

ChefBook is an WIP cross platform open source Recipe Book & Shopping List app

#### [✨ Official website](https://chefbook.io)
#### [📱 Google Play](https://play.google.com/store/apps/details?id=com.cactusknights.chefbook)

### Other resources
##### [📙 VK Page](https://vk.com/chefbook)
##### [👨‍🍳 Telegram Stickers](https://t.me/addstickers/chefbook)

## Conception
ChefBook aimed to cover wide range of users to make personal cooking space. I try to keep balance between minimalism and functionality. Wanna get ready translated recipes from all over the world? Wanna publish your own recipes to share them with friends or app community? Just need to store them for yourself or even encrypt to hide from prying eyes? Anyway, ChefBook suits you.

## Features:
* Private, available by link and public recipes
* International community recipes with translations
* Data encryption
* Advanced ingredients & cooking steps management (sections, pictures, timers, adaptability)
* Customizable categories
* Synchronization between devices
* Integrated Shopping List
* Saving recipe book as document

## Architecture
You can find more information in appropriate submodules.

### Backend
Backend uses microservices architecture and deployed in Kubernetes Cluster (since this is a pet project, I can't invest in scaling, so it's pretty tiny). Services written on Go. Data stored in PostgreSQL + S3.

### Android
Android client is multimodule and written on pretty fresh stack: Kotlin + Jetpack Compose + MVI + Koin. KMM isn't planned for near future.

### iOS
I plan to develop iOS client when Android client version 4.0 will be released. It will definitely written on Swift + SwiftUI + Alamofire. I'm not sure about the MVI, cause it's pretty painful to implement it for iOS, as it seemed to me.

### Frontend
Development plan same as iOS. For this moment, frontend contains only stub homepage. It's quickly crooked made on React. I plan use that framework for full web app.

## Submodules
* `chefbook-backend` - Backend
* `chefbook-frontend` - Frontend
* `chefbook-android` - Android client
* `chefbook-graphics` - Common Graphics sush as logo and stickers

## Encryption
ChefBook have data encryption support.

When you enable encryption for recipe, app encrypt all sensitive information, including pictures.

### How encryption works?
#### User Key
1. When you create encrypted vault by input password, ChefBook hashes it via SHA-256 and converts to AES Key.
2. Then app generate user RSA Keys Pair (maybe I'll swap to Curve25519), encrypts Private Key with AES and saves Key Pair to file locally and remotely.
3. When you unlock the vault with password, app converts it to AES and tries to decrypt Key Pair file.
#### Recipe Key
1. When you create encrypted recipe, ChefBook generates random AES Key.
2. Then app uses User Public Key to encrypts AES and saves it to file locally and remotely.
3. When storage unlocked, all AES-keys is being decrypt by User Private Key.
#### Sharing
1. When recipient wants to get encrypted recipe by link, he sends his User Public Key to Server.
2. Then recipe owner encrypt Recipe Key with recipient's Piblic Key and sends it to server.
3. Recipient's app gets data, decrypts it with recipient's Private Key and decrypts recipe.

Vault password is an entrypoint, which generates AES in runtime. Other keys are stored in encrypted form.
