# LocalSend

[![CI status][ci-badge]][ci-workflow]
[![Translations][translate-badge]][translate-link]

[ci-badge]: https://github.com/localsend/localsend/actions/workflows/ci.yml/badge.svg
[ci-workflow]: https://github.com/localsend/localsend/actions/workflows/ci.yml
[translate-badge]: https://hosted.weblate.org/widget/localsend/app/svg-badge.svg
[translate-link]: https://hosted.weblate.org/engage/localsend/

[Homepage][homepage] • [Discord][discord] • [GitHub][github] • [Codeberg][codeberg]

[English](README.md) • [中文](readme_i18n/README_ZH.md) • [日本語](readme_i18n/README_JA.md) • [ภาษาไทย](readme_i18n/README_TH.md) • [Filipino](readme_i18n/README_PH.md) • [Polski](readme_i18n/README_PL.md) • [Español](readme_i18n/README_ES.md) • [Tiếng Việt](readme_i18n/README_VI.md) • [Portugês Brasil](readme_i18n/README_PT_BR.md) • [Italiano](readme_i18n/README_IT.md) • [Indonesia](readme_i18n/README_ID.md) • [ភាសាខ្មែរ](readme_i18n/README_KM.md) • [Français](readme_i18n/README_FR.md) • [فارسی](readme_i18n/README_FA.md)   • [Turkish](readme_i18n/README_TR.md)

[homepage]: https://localsend.org
[discord]: https://discord.gg/GSRWmQNP87
[github]: https://github.com/localsend/localsend
[codeberg]: https://codeberg.org/localsend/localsend

LocalSend is a free, open-source app that allows you to securely share files and messages with nearby devices over your local network without needing an internet connection.

- [About](#about)
- [Screenshots](#screenshots)
- [Download](#download)
- [How It Works](#how-it-works)
- [Getting Started](#getting-started)
- [Contributing](#contributing)
  - [Translation](#translation)
  - [Bug Fixes and Improvements](#bug-fixes-and-improvements)
- [Building](#building)
  - [Android](#android)
  - [iOS](#ios)
  - [macOS](#macos)
  - [Windows](#windows)
  - [Linux](#linux)

## About

LocalSend is a cross-platform app that enables secure communication between devices using a REST API and HTTPS encryption. Unlike other messaging apps that rely on external servers, LocalSend doesn't require an internet connection or third-party servers, making it a fast and reliable solution for local communication.

## Screenshots

<img src="https://localsend.org/img/screenshot-iphone.webp" alt="iPhone screenshot" height="300"/> <img src="https://localsend.org/img/screenshot-pc.webp" alt="PC screenshot" height="300"/>

## Download

It is recommended to download the app either from an app store or from a package manager because the app does not have an auto-update.

| Windows                 | macOS                   | Linux              | Android        | iOS           | Fire OS    |
|-------------------------|-------------------------|--------------------|----------------|---------------|------------|
| [Winget][]              | [App Store][]           | [Flathub][]        | [Play Store][] | [App Store][] | [Amazon][] |
| [Scoop][]               | [Homebrew][]            | [Nixpkgs][]        | [F-Droid][]    |               |            |
| [Chocolatey][]          | [DMG Installer][latest] | [Snap][]           | [APK][latest]  |               |            |
| [EXE Installer][latest] |                         | [AUR][]            |                |               |            |
| [Portable ZIP][latest]  |                         | [TAR][latest]      |                |               |            |
|                         |                         | [DEB][latest]      |                |               |            |
|                         |                         | [AppImage][latest] |                |               |            |

Read more about [distribution channels][].

[windows store]: https://www.microsoft.com/store/apps/9NCB4Z0TZ6RR
[app store]: https://apps.apple.com/us/app/localsend/id1661733229
[play store]: https://play.google.com/store/apps/details?id=org.localsend.localsend_app
[f-droid]: https://f-droid.org/packages/org.localsend.localsend_app
[amazon]: https://www.amazon.com/dp/B0BW6MP732
[winget]: https://github.com/microsoft/winget-pkgs/tree/master/manifests/l/LocalSend/LocalSend
[scoop]: https://scoop.sh/#/apps?s=0&d=1&o=true&q=localsend&id=fb88113be361ca32c0dcac423cb4afdeda0b0c66
[chocolatey]: https://community.chocolatey.org/packages/localsend
[homebrew]: https://formulae.brew.sh/cask/localsend
[flathub]: https://flathub.org/apps/details/org.localsend.localsend_app
[nixpkgs]: https://search.nixos.org/packages?show=localsend
[snap]: https://snapcraft.io/localsend
[aur]: https://aur.archlinux.org/packages/localsend-bin
[latest]: https://github.com/localsend/localsend/releases/latest
[distribution channels]: https://github.com/localsend/localsend/blob/main/CONTRIBUTING.md#distribution

**Compatibility**

| Platform | Minimum Version | Note                                                                                                                        |
|----------|-----------------|-----------------------------------------------------------------------------------------------------------------------------|
| Android  | 5.0             | -                                                                                                                           |
| iOS      | 12.0            | -                                                                                                                           |
| macOS    | 11 Big Sur      | Use OpenCore Legacy Patcher 2.0.2 (See [#1005](https://github.com/localsend/localsend/issues/1005#issuecomment-2449899384)) |
| Windows  | 10              | The last version to support Windows 7 is v1.15.4. There might be backports of newer versions for Windows 7 in the future.   |
| Linux    | N.A.            | -                                                                                                                           |

## Setup

In most cases, LocalSend should work out of the box. However, if you are having trouble sending or receiving files, you may need to configure your firewall to allow LocalSend to communicate over your local network.

| Traffic Type | Protocol | Port  | Action |
|--------------|----------|-------|--------|
| Incoming     | TCP, UDP | 53317 | Allow  |
| Outgoing     | TCP, UDP | Any   | Allow  |

Also make sure to disable AP isolation on your router. It should be usually disabled by default but some routers may have it enabled (especially guest networks).

**Portable Mode**

(Introduced in v1.13.0)

Create a file named `settings.json` located in the same directory as the executable.
This file can be empty.
The app will use this file to store settings instead of the default location.

**Start hidden**

(Updated in v1.15.0)

To start the app hidden (only in tray), use the `--hidden` flag (example: `localsend_app.exe --hidden`).

On v1.14.0 and earlier, the app starts hidden if `autostart` flag is set, and the hidden setting is enabled.

## How It Works

LocalSend uses a secure communication protocol that allows devices to communicate with each other using a REST API. All data is sent securely over HTTPS, and the TLS/SSL certificate is generated on the fly on each device, ensuring maximum security.

For more information on the LocalSend Protocol, see the [documentation](https://github.com/localsend/protocol).

## Getting Started

To compile LocalSend from the source code, follow these steps:

1. Install Flutter [directly](https://flutter.dev) or using [fvm](https://fvm.app) (see [version required](.fvmrc))
2. Clone the `LocalSend` repository
3. Run `cd app` to enter the app directory
4. Run `flutter pub get` to download dependencies
5. Run `flutter run` to start the app

> [!NOTE]
> LocalSend currently requires an older Flutter version (specified in [.fvmrc](.fvmrc))
> and thus build issues may be caused by a mismatch between the required and the (system-wide) installed Flutter version.  
> To make development more consistent, LocalSend uses [fvm](https://fvm.app) to manage the project Flutter version.
> After installing `fvm`, run `fvm flutter` instead of `flutter`.

## Contributing

We welcome contributions from anyone interested in helping improve LocalSend. If you'd like to contribute, there are a few ways to get involved:

### Translation

You can help translate LocalSend into other languages. We use the [Weblate](https://hosted.weblate.org/projects/localsend/app) platform to manage translations.

Alternatively, you can also contribute by forking this repository and adding translations manually.

The translations are located in the [app/assets/i18n](https://github.com/localsend/localsend/tree/main/app/assets/i18n) directory. Edit the `_missing_translations_<locale>.json` or `strings_<locale>.i18n.json` file to add or update translations.

<a href="https://hosted.weblate.org/engage/localsend/">
<img src="https://hosted.weblate.org/widget/localsend/app/multi-auto.svg" alt="Translation status" />
</a>

**_Take note:_ Fields decorated with `@` are not meant to be translated; they are not used in the app in any way, being merely informative text about the file or to give context to the translator.**

### Bug Fixes and Improvements

- **Bug Fixes:** If you find a bug, please create a pull request with a clear description of the issue and how to fix it.
- **Improvements:** Have an idea for how to improve LocalSend? Please create an issue first to discuss why the improvement is needed.

For more information, see the [contributing guide](https://github.com/localsend/localsend/blob/main/CONTRIBUTING.md).

## Building

These commands are intended for maintainers only.

### Android

Traditional APK

```bash
flutter build apk
```

AppBundle for Google Play

```bash
flutter build appbundle
```

### iOS

```bash
flutter build ipa
```

### macOS

```bash
flutter build macos
```

### Windows

**Traditional**

```bash
flutter build windows
```

**Local MSIX App**

```bash
flutter pub run msix:create
```

**Store ready**

```bash
flutter pub run msix:create --store
```

### Linux

**Traditional**

```bash
flutter build linux
```

**AppImage**

```bash
appimage-builder --recipe AppImageBuilder.yml
```

**Snap**

Instructions in [localsend/snap/README.md](https://github.com/localsend/snap/blob/main/README.md)

## Contributors

<a href="https://github.com/localsend/localsend/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=localsend/localsend"  alt="Localsend Contributors"/>
</a>

17.02.26
# 📑 Звіт AI-консультанта: Проект "LocalSend"

Цей звіт базується на аналізі репозиторію **LocalSend** — відкритої кросплатформенної альтернативи AirDrop.

---

## 🧬 Частина 1: "ДНК" Проекту

**LocalSend** — це додаток, який забезпечує безпечний обмін файлами та повідомленнями в локальній мережі без доступу до інтернету. Його логіку можна розбити на такі **атомарні функції**:

*   **Мережева комунікація (REST API):** Використання власного протоколу зв’язку, де пристрої взаємодіють через REST-запити.
*   **Динамічне шифрування (HTTPS/TLS):** Генерація TLS/SSL сертифікатів "на льоту" для кожного пристрою, що забезпечує максимальний захист HTTPS без сторонніх серверів.
*   **Виявлення пристроїв (Discovery):** Логіка пошуку активних вузлів у локальній мережі через TCP/UDP порт 53317.
*   **Обробка черги передачі (Data Streaming):** Сегментація та передача великих файлів і текстових повідомлень між різними ОС (Windows, macOS, Linux, Android, iOS).
*   **Керування налаштуваннями (Persistence):** Підтримка портативного режиму через файл `settings.json` для локального зберігання конфігурацій.

### 💎 Головна технічна цінність
Головна технічна цінність полягає в **повному суверенітеті даних**. LocalSend не покладається на зовнішні сервери або хмарні рішення, забезпечуючи швидку та приватну передачу даних за рахунок прямого зв’язку пристроїв через локальний протокол шифрування.

---

## 🚀 Частина 2: "Трансформація" (Інтеграція з Gemini LLM)

Інтеграція з Gemini (використовуючи можливості **GitHub Models**) перетворює LocalSend із простого інструменту передачі на **інтелектуальний вузол розподілу знань**.

### Як зміниться функціонал?
1.  **Контекстна передача:** Gemini може аналізувати вміст файлів, що передаються, і автоматично пропонувати відповідні пристрої (наприклад, надсилати код на ПК, а фото — на планшет).
2.  **Голосове управління діями:** Використання LLM для виконання команд природною мовою: *"Відправ останній звіт на всі пристрої в кабінеті"*.
3.  **Інтелектуальне резюмування повідомлень:** При передачі довгих текстових повідомлень через локальну мережу, Gemini може автоматично створювати їх короткий зміст для отримувача.

### Сценарій сервісу (LocalSend + Gemini + ID_{$})

Створення сервісу **"Local Smart-Sync Hub"** на вашому сайті.

**Алгоритм роботи:**
1.  **Ввід:** Користувач завантажує документ через ваш сайт (локальний хост).
2.  **Обробка (Gemini):** Ваш базовий Python-скрипт `ID_{$}` відправляє документ до Gemini для аналізу та категоризації.
3.  **Логіка (ID_{$}):** Скрипт вирішує, куди саме потрібно доставити цей файл на основі інструкцій користувача.
4.  **Виконання (LocalSend API):** Скрипт `ID_{$}` звертається до REST API LocalSend на вашому сервері та ініціює передачу файлу на цільовий пристрій у локальній мережі.
5.  **Візуалізація:** Використовуючи **GitHub Spark**, ви створюєте інтерфейс сайту, де відображається карта активних пристроїв та статус "інтелектуальної" передачі.

---

## 📋 План дій для Notion
| Крок | Дія | Результат |
| :--- | :--- | :--- |
| **1** | Компіляція проекту через Flutter (`flutter run`) | Готова робоча інстанція |
| **2** | Налаштування фаєрволу для порту 53317 | Відкритий шлях для передачі |
| **3** | Створення Python-містка (`ID_{$}`) до REST API | Можливість керування через код |
| **4** | Інтеграція Gemini через **GitHub Models** | Додавання "мізків" до процесу передачі |

---

### 💡 Резюме

**Суть:** **Безпечний локальний обмін файлами без інтернету**.

**AI-Роль:** **Інтелектуальна маршрутизація та обробка локальних даних**. (Роль AI є аналітичним прогнозом на основі згаданих у джерелах інструментів GitHub для створення інтелектуальних додатків).
