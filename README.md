<p align="center">
<img width="128" src="https://github.com/enricocid/Music-Player-GO/blob/main/fastlane/metadata/android/en-US/images/icon.png">
</p>

<h1 align="center">Music Player GO</h1>

<p align="center">
<img width="400" src="art16.gif">
</p>

<p align="center">
  <!-- Latest Release -->
    <a href="https://github.com/enricocid/Music-Player-GO/releases">
      <img alt="GitHub release"
      src="https://img.shields.io/static/v1?label=Tag&message=v4.4.24&color=58F5D1">
    </a>
   <!-- Minimum SDK -->
    <img alt="Minimum SDK" src="https://img.shields.io/static/v1?label=API&message=21&color=32B5ED">
     <!-- Android CI integration -->
    <a href="https://github.com/enricocid/Music-Player-GO/actions">
    <img alt="CI" src="https://github.com/enricocid/Music-Player-GO/workflows/Android%20CI/badge.svg">
    </a>
    <!-- Support Ukraine -->
    <a href="https://war.ukraine.ua/support-ukraine/">
    <img alt="Support Ukraine" src="https://img.shields.io/static/v1?label=Support Ukraine&message=now!&color=005BBB">
    </a>
</p>

  <h3 align="center">
  <a href="https://hosted.weblate.org/engage/music-player-go/">
    <img src="https://hosted.weblate.org/widgets/music-player-go/-/287x66-white.png" />
  </a>
  </h3>

  <h3 align="center">
  <a href="PRIVACY_POLICY.md">Privacy policy</a> |
  <a href="FAQ.md">FAQ</a> |
  <a href="LIBS.md">3rd party components</a> |
  <a href="CONTRIBUTORS.md">Contributors</a> |
  <a href="FORMATS.md">Formats</a>
  </h3>

  </h3>


# Table of contents

- [Description](#description)
- [Download](#download)
- [Features](#features)
- [Translations](#translations)
- [Contributing](#contributing)
- [License](#license)


# Description

Welcome to **Music Player GO**, your go-to local Android music player that strikes the perfect balance between simplicity and performance. Dive into a world where your music is organized intuitively, offering a minimal yet fully-featured experience!


# Download

[<img src="https://raw.githubusercontent.com/enricocid/fdroid-custom-badges/main/badge_get-it-on.png"
    alt="Get it on F-Droid"
    height="80">](https://f-droid.org/packages/com.iven.musicplayergo/)
[<img src="https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png"
    alt="Get it on Google Play"
    height="80">](https://play.google.com/store/apps/details?id=com.iven.musicplayergo)
  
# Features

- Minimal interface
- Equalizer
- Music organised by artist, albums, songs and folders; tabs are organisable
- Light, dark, automatic themes and accents
- Pure black theme
- Queue
- Sleep timer
- Audio focus, precise volume and headset management
- Now playing, embedded covers, search, playback speed, pause on completion, sorting, shuffle, fast-seeking, and more!
 

# Translations

We currently need help translating the project so our app can be more accessible to everyone worldwide!
The image below is an overview of the language translations that are currently being worked on:
- The smaller red bars indicate that there is a significant amount of translating needed
- We would ideally like each language to reach to green (less translations needed)
- Please feel free to add new languages that are not currently being translated

In order to contribute please use [Weblate](https://hosted.weblate.org/engage/music-player-go/). 
You will need to create an account with Weblate (if you don't already have one) in order to do so.

It would also be greatly appreciated if you could send some [love](https://weblate.org/donate/new/) to the Weblate contributors who made easy translations possible :)
By clicking the link, you will be directed to the Weblate monetary donations page, where you will also be prompted to sign in or create an account.

<a href="https://hosted.weblate.org/engage/music-player-go/">
<img src="https://hosted.weblate.org/widgets/music-player-go/-/horizontal-auto.svg" alt="Stato traduzione" />
</a>

# Contributing

Thank you for considering contributing to Music Player GO! We welcome contributions from the community to help improve and grow this project. Below are some guidelines for front and back end contributions. If you would like to contribute towards translations, please see the above [Translations](#translations) section.

### How to Contribute

* Feel free to submit pull requests for any contributions, using a [feature branch](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow).
* Once you have submitted a pull request, we will need to review and appove it before it can be merged with the project.
* After your contribution has been added we can add you to our list of [contributors](CONTRIBUTORS.md)!
* We would greatly appreciate if you could look at the [issues](https://github.com/enricocid/Music-Player-GO/issues) tab to see what needs fixing, especially if there are any bugs!!
* While there is no strict coding style for this project, we encourage you to strive for consistency within the existing codebase and UI following with the minimalistic aesthetic of the application.
* Please make sure to look at the the [FAQ's](FAQ.md), [Privacy Policy](PRIVACY_POLICY.md), [Formats](FORMATS.md), [libraries we utilize](LIBS.md), and [our license](LICENSE.md) before you get started to familiairze yourself with our app and frameworks.

## Environmental requirements

JDK version: Eclipse Temurin 17.0.16+

Gradle version: 8.0

Android SDK: It needs to include API 33 (Android 13)

Android Studio: Version 2022.3.1 or higher

## Compilation configuration

Compilation SDK version: 33

Minimum SDK version: 21 (Android 5.0)

Target SDK version: 33

Kotlin version: 1.8.21

# The steps of "from zero to run"

To get started, you would need to clone/fork this repository:
- Note *user* refers to your GitHub username

### Windows Terminal commands:

git clone https://github.com/*user*/Music-Player-GO.git

cd Music-Player-GO

### Mac Terminal commands:

git clone https://github.com/*user*/Music-Player-GO.git

cd Music-Player-GO

Then you can use Android Studio to open the "project" folder

### Environment Download

Most of environments will be downloaded by Android Studio automatically.

For JDK version, you can choose "settings"- "Bulid, Excution, Deployment"- "Bulid Tools"- "Gradle". Choose "Gradle JDK" and download Eclipse Temurin 17.0.16. Then you can run the app in Android Studio.



# License


2024 &copy; **Enrico D'Ortenzio**

This repository is copylefted libre software, licensed [GPLv3](https://www.gnu.org/licenses/#GPL), as described in the [LICENSE](LICENSE.md) file.
Use, study, change and share at will; with all.



# code function 目录与文件职责速览（Kotlin/Android 常见分层）

### dialogs（弹窗与底部面板）

Dialogs：集中创建/显示各类对话框的入口或工具。

FavoritesAdapter：收藏列表的 RecyclerView 适配器。

NowPlaying：显示“正在播放”曲目的弹窗/底部面板。

QueueAdapter：播放队列列表适配器。

RecyclerSheet：可复用的“底部抽屉/列表”组件。

### equalizer（均衡器）

EqualizerActivity：均衡器独立页面（Activity），负责创建 Fragment、处理返回键等。

EqualizerFragment：均衡器 UI 与逻辑（预设、频段滑条、开关等）。

### extensions（Kotlin 扩展）

MusicExts.kt：对 Music/播放相关类的扩展函数（如格式化时长、专辑艺人拼接等）。

ViewExts.kt：对 View/UI 的扩展（如简化点击、可见性、主题色应用等）。

### fragments（主要内容页）

AllMusicFragment：全部歌曲列表页（扫描结果、排序、搜索、点击播放/加入队列）。

DetailsFragment：专辑/艺人/文件夹等“容器”下的明细歌曲列表。

ErrorFragment：无权限/无媒体/异常时的错误占位页。

MusicContainersFragment：按“容器”（专辑、艺人、文件夹、收藏等）分组的一级页签/网格。

### models（数据模型）

Album：专辑实体（名称、艺人、封面 id、曲目数等）。

Music：歌曲实体（id、uri/path、标题、专辑/艺人、时长、位置信息、标签等）。

NotificationAction：通知栏动作的模型（播放/暂停/下一首等）。

SavedEqualizerSettings：均衡器预设/用户保存的配置。

Sorting：排序策略与字段（按标题、专辑、日期等）。

### player（播放内核与前台服务）

MediaButtonReceiver：耳机线控/车载/蓝牙媒体按键接收。

MediaPlayerHolder.kt：实际的播放器封装（ExoPlayer/MediaPlayer 的持有者；播放、暂停、seek、队列、回调）。

MediaPlayerInterface：对外暴露的播放控制接口（播放/暂停/上一首/下一首/设置队列等）。

MediaPlayerUtils：与播放相关的工具函数（音频焦点、会话、格式兼容等）。

MusicNotificationManager：前台服务的媒体样式通知（封面、标题、动作按钮）。

PlayerService.kt：前台服务（保持播放常驻、通知控制、音频焦点、后台存活）。

TileService.kt：快捷设置磁贴（下拉快捷开关）控制播放或打开应用。

### preferences（设置页与适配器）

AccentsAdapter：主题/强调色选择列表适配器。

ActiveTabsAdapter：主页显示哪些 Tab 的适配器（歌曲/专辑/艺人/文件夹/收藏等）。

ContextUtils：与 Context/主题/本地化/尺寸相关的工具。

FiltersAdapter：过滤条件适配器（如时长>30s、仅本地文件等）。

NotificationActionsAdapter：自定义通知栏按钮顺序/显示的适配器。

PreferencesFragment：“偏好设置”子页（具体项分组）。

SettingsFragment：设置总页（入口，承载多个子设置 Fragment）。

### ui（界面层通用）

ItemSwipeCallback / ItemTouchCallback：RecyclerView 滑动/拖拽回调（删除、置顶、拖动排序等）。

MainActivity：应用主入口（TabLayout + ViewPager2、Fragment 容器、权限申请、菜单）。

MediaControlInterface：上层 UI 可调用的媒体控制接口（面向 Fragment/Activity）。

SingleClickHelper：防止快速连点的工具。

UIControlInterface：UI 交互通用接口（切换页签、显示面板、SnackBar 等）。

### utils（基础设施与全局状态）

BaseActivity：通用基类（主题、系统栏、沉浸式、公共事件）。

GoApp：Application 子类（初始化日志、播放器、首选项、主题、媒体库扫描）。

GoConstants：常量定义（Intent key、默认值、请求码、渠道名等）。

GoPreferences：SharedPreferences 读写封装（用户设置、首次启动、上次播放等）。

MusicViewModel：共享 ViewModel（选中项、当前队列、播放状态、筛选/排序、UI 事件分发）。
