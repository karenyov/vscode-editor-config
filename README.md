<!-- Title -->

<h1 align="center"> :iphone: 11Care </h1>

<!-- Header -->

<p align="center">
  <!-- iOS -->
  <img alt="Supports Expo iOS" longdesc="Supports Expo iOS" src="https://img.shields.io/badge/iOS-000.svg?style=flat-square&logo=APPLE&labelColor=999999&logoColor=fff" />
  <!-- Android -->
  <img alt="Supports Expo Android" longdesc="Supports Expo Android" src="https://img.shields.io/badge/Android-000.svg?style=flat-square&logo=ANDROID&labelColor=A4C639&logoColor=fff" />
  <!-- Web -->
  <img alt="Supports Expo Web" longdesc="Supports Expo Web" src="https://img.shields.io/badge/web-000.svg?style=flat-square&logo=GOOGLE-CHROME&labelColor=4285F4&logoColor=fff" />
</p>

## Requirements

- [NodeJs](https://nodejs.org/en/).
- [Expo](https://docs.expo.dev/get-started/installation/).

## Features

- Lib para construção dos componentes: [Native Base](https://nativebase.io/).

<!-- Installation -->

### Installation

### Run

> using Git

```sh

# Clone this repository
git clone <repository name>

# cmd in project file
# install all dependencies
npm install

# run aplication
npx expo start

# Modo ProduÃ§Ã£o
npx expo start --no-dev --minify

# Login expo
expo login

```

### Configs

> DEV_API_URL: para testes em modo dev, PROD_API_URL: automaticamente configurado após realizar o build do APK.

Configs in .env.example file.

### Scripts

```sh
# list all inconsistencies
npm run lint

# list all inconsistencies and fix
npm run lint-and-fix

# format all code with prettier format
npm run prettier-format
```

### Gerar APK - MANUALMENTE

#### Versão Release - ANDROID

> Doc: https://reactnative.dev/docs/signed-apk-android

```sh
# Gerar Key
cd android/app

keytool -genkey -v -keystore my-upload-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
```

Alterar arquivo `/.gradle/gradle.properties`:

```
MYAPP_UPLOAD_STORE_FILE=my-upload-key.keystore
MYAPP_UPLOAD_KEY_ALIAS=my-key-alias
MYAPP_UPLOAD_STORE_PASSWORD=*****
MYAPP_UPLOAD_KEY_PASSWORD=*****
```

Alterar o arquivo `android/app/build.gradle`:

```
...
android {
    ...
    defaultConfig { ... }
    signingConfigs {
        ...
        release {
            if (project.hasProperty('MYAPP_UPLOAD_STORE_FILE')) {
                storeFile file(MYAPP_UPLOAD_STORE_FILE)
                storePassword MYAPP_UPLOAD_STORE_PASSWORD
                keyAlias MYAPP_UPLOAD_KEY_ALIAS
                keyPassword MYAPP_UPLOAD_KEY_PASSWORD
            }
        }
    }
    buildTypes {
        ...
        release {
            signingConfig signingConfigs.release
            minifyEnabled enableProguardInReleaseBuilds
            proguardFiles getDefaultProguardFile("proguard-android.txt"), "proguard-rules.pro"
        }
    }
}
...
```

#### Gerar APK

> Arquivo gerado ficará em: `android/app/build/outputs/apk/release/app-release.apk`.

Executar em `/android`:
`./gradlew assembleRelease`

#### Gerar aab

> Arquivo gerado ficará em: `android/app/build/outputs/bundle/release/app-release.aab`.

Executar em `/android`:
`./gradlew bundleRelease`

### Gerar APK - EAS

> DOC: https://docs.expo.dev/build-reference/apk/

```sh

# Gerando secrets do arquivo .env
eas secret:push --force

# Gerar APK - EAS
eas build -p android --profile preview
```

O Link da Build aparecerão no terminal.
`.

### Criando variáveis no arquivo .env

> https://blog.logrocket.com/understanding-react-native-env-variables/#what-node-env
> Ao Criar uma nova variável no arquivo, serÃ¡ preciso definir a tipagem em: `/src/@types/env.d.ts`.

### Criando novas rotas

Ao Criar uma nova rota, serÃ¡ preciso definir a tipagem em: `/src/@types/navigation.d.ts`.

### Úteis

#### Problemas build, ícones etc.

É necessário deletar a pasta `./android` e rodar novamente o `expo run:android`.

#### Nome do Aplicativo

Alterar nome do Aplicativo Android: `android\app\src\main\res\values\strings.xml` alterar chave `app_name`.

#### Adicionar nova Pasta/Rota

Fazer o mapeamento nos seguintes arquivos: `babel.config.js` e `tsconfig.json`.
