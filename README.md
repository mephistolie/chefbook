# ChefBook
#### NOTE: THIS README IS ACTUAL FOR NEW WIP VERSION

ChefBook is an cross platform Recipe Book & Shopping List app with an open sourced client
#### [📱 Google Play](https://play.google.com/store/apps/details?id=com.cactusknights.chefbook)
#### [📙 VK Page](https://vk.com/chefbook)
#### [👨‍🍳 Telegram Stickers](https://t.me/addstickers/chefbook)
##### PS: backend open source is planned when I'll make huge refactor
## Conception
ChefBook aimed to cover wide range of users and make personal space with maximum customization without losing possibility sharing data. I try to keep a balance between minimalism and functionality.

## Core Stack
* **Backend:** Go + GIN + Postgres + Docker Compose + Traefik
* **Android:** Kotlin (more at `chefbook-android` submodule)
* **iOS:** Swift + SwiftUI planned
* **Frontend:** React or Vue planned

## Submodules
* `chefbook-android` - Android Client
* `chefbook-backend` - Backend
* `chefbook-graphics` - Common Graphics sush as Logo or Stickers

## Features:
* Private, available by link and public recipes
* Social media elements such likes
* Hybrid data encryption for thoose, who need it (see below)
* Synchronization between devices in online mode
* Recipe preview and steps preview
* Customizable categories with emoji-covers
* Dividing ingredients and cooking steps into sections
* Ingredients-recipes and cooking steps-timers
* Recipes sorting
* Integrated Shopping List
* Sharing recipes as deeplink or text

## Encryption
ChefBook have encrypted recipes storage for professional cooks or just people, who cares about privacy.

When you enable encryption for recipe, app encrypt:
* Name
* Description
* Ingredients
* Cooking
* Pictures

Categories, time, servings and calories not being encrypt.

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
1. When recipient wants to get encrypted recipe by link, he sends his User Public Key to Server, except last 4 symbols.
2. Then recipe owner enters these symbols, app concatenates data, encrypt Recipe Key with recipient's Piblic Key and sends it to server.
3. Recipient's app gets data, decrypts it with recipient's Private Key and decrypts recipe.

Vault's password is an entrypoint, which generates AES in runtime. Other keys are stored everywhere in encrypted form.
