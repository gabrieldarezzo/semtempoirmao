Objetivos:
[ ] Copiar o conteudo do repositorio para o VueJs / Quasar
[ ]

Android
```
quasar dev -m cordova -T android
```

```
Ionic -> angular
Assim como
Quasar -> vue
```

Gerar icones para o Cordova:
https://pgicons.abiro.com
Jogar na pasta `src-cordova` :
```xml
<platform name="android">
    <allow-intent href="market:*" />
    <allow-intent href="market:*" />
    <preference name="SplashMaintainAspectRatio" value="true" />
    <preference name="SplashShowOnlyFirstTime" value="false" />
    <icon qualifier="hdpi" src="res/icon/android/hdpi.png" />
    <icon qualifier="ldpi" src="res/icon/android/ldpi.png" />
    <icon qualifier="mdpi" src="res/icon/android/mdpi.png" />
    <icon qualifier="xhdpi" src="res/icon/android/xhdpi.png" />
    <icon qualifier="xxhdpi" src="res/icon/android/xxhdpi.png" />
    <icon qualifier="xxxhdpi" src="res/icon/android/xxxhdpi.png" />
</platform>
```



# Publish in Android:

Leitura de apoio:
https://medium.com/@jeanscr/como-gerar-app-release-no-ionic-3cb448e87d15
https://cordova.apache.org/docs/en/8.x/guide/platforms/android/index.html#signing-an-app

```
quasar build -m cordova -T android
```

## Na primeira vez
```
cd src-cordova\platforms\android
keytool -genkey -v -keystore SemTempoIrmao.keystore -alias SemTempoIrmao -keyalg RSA -keysize 2048 -validity 20000
```

Senha:
Keke12345


```
mv SemTempoIrmao.keystore ..\..\SemTempoIrmao.jks
cd src-cordova\platforms\android
```

Leitura de apoio:
https://cordova.apache.org/docs/en/latest/guide/platforms/android/index.html#signing-an-app

Create file: in `src-cordova\platforms\android\release-signing.properties`  contains:
```
storeFile=SemTempoIrmao.jks
storeType=jks
keyAlias=SemTempoIrmao
// Se você não deseja inserir a senha em cada compilação, use isso:
keyPassword=Keke12345
storePassword=Keke12345
```


```
cordova run android --release -- --keystore=SemTempoIrmao.jks --storePassword=Keke12345 --alias=SemTempoIrmao --password=Keke12345
```


