# Happ Ultimate — XML + Kotlin

Самостоятельная Android-основа с интерфейсом на Android Views (XML + Kotlin), Material Components / Material You и AMOLED-оформлением. Это не оригинальные закрытые исходники Happ.

## Что изменено
- Jetpack Compose и Compose Gradle plugin удалены.
- Интерфейс переведён на XML layouts и Kotlin Activity.
- Используются Material Components for Android и динамические Material You цвета на Android 12+.
- Сохранена AMOLED-тёмная основа и чёрные системные панели.
- Сохранены `XrayBridge.kt`, `XrayVpnService.kt` и локальная библиотека `app/libs/libXray.aar`.

## Сборка
- Открыть корневую папку `Happ-Ultimate-Android` как Gradle project.
- Требуются JDK 17, Android SDK Platform 35 и Android Gradle Plugin 8.7.3. Сборочные файлы — Groovy (`build.gradle`), без Maven-зависимостей, чтобы проект собирался и в CodeAssist.
- Выполнить Gradle Sync, затем `:app:assembleDebug`.
- `libXray.aar` уже находится в `app/libs/`.

## Важно
Это исходный проект, а не готовый APK. В этой среде Android SDK/Gradle build не запускался, поэтому компиляция и запуск VPN на устройстве не подтверждены. VPN runtime зависит от версии libXray и формата Xray-конфигурации.

## libXray без AAR
Для сборщиков, которые не подключают локальные `.aar` (например, CodeAssist), содержимое `libXray.aar` разложено вручную:
- `app/libs/libXray-classes.jar` — Java-классы (`classes.jar` из aar);
- `app/src/main/jniLibs/<abi>/libgojni.so` — нативные библиотеки;
- оригинальный `libXray.aar` сохранён в `extras/`.

## Сборка через GitHub Actions
Загрузи проект в репозиторий GitHub — workflow `.github/workflows/build.yml` соберёт `app-debug.apk` (Actions → Artifacts).
`XrayBridge.kt` обращается к libXray через рефлексию, поэтому компилируется и там, где `libs/*.jar` не подключается.
