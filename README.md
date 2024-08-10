<h1 align="center">
    PHP Telegram 机器人<br>
	<br>
    <img src="https://raw.githubusercontent.com/php-telegram-bot/assets/master/logo/512px/logo_plain.png" title="PHP Telegram 机器人" alt="PHP Telegram 机器人标志">
	<br>
</h1>

一个基于官方 [Telegram 机器人 API] 的 Telegram 机器人

[![API 版本](https://img.shields.io/badge/Bot%20API-7.1%20%28February%202024%29-32a2da.svg)](https://core.telegram.org/bots/api-changelog#february-16-2024)
[![加入 Telegram 机器人支持群组](https://img.shields.io/badge/telegram-@PHP__Telegram__Bot__Support-64659d.svg)](https://telegram.me/PHP_Telegram_Bot_Support)
[![捐赠](https://img.shields.io/badge/%F0%9F%92%99-Donate%20%2F%20Support%20Us-blue.svg)](#donate)

[![测试](https://github.com/php-telegram-bot/core/actions/workflows/tests.yaml/badge.svg)](https://github.com/php-telegram-bot/core/actions/workflows/tests.yaml)
[![代码覆盖率](https://img.shields.io/scrutinizer/coverage/g/php-telegram-bot/core/master.svg?style=flat)](https://scrutinizer-ci.com/g/php-telegram-bot/core/?b=master)
[![代码质量](https://img.shields.io/scrutinizer/g/php-telegram-bot/core/master.svg?style=flat)](https://scrutinizer-ci.com/g/php-telegram-bot/core/?b=master)
[![最新稳定版本](https://img.shields.io/packagist/v/longman/telegram-bot.svg)](https://packagist.org/packages/longman/telegram-bot)
[![依赖](https://tidelift.com/badges/github/php-telegram-bot/core?style=flat)][Tidelift]
[![总下载量](https://img.shields.io/packagist/dt/longman/telegram-bot.svg)](https://packagist.org/packages/longman/telegram-bot)
[![月下载量](https://img.shields.io/packagist/dm/longman/telegram-bot.svg)](https://packagist.org/packages/longman/telegram-bot)
[![最低 PHP 版本](http://img.shields.io/badge/php-%3E%3D8.1-8892BF.svg)](https://php.net/)
[![许可证](https://img.shields.io/packagist/l/longman/telegram-bot.svg)](https://github.com/php-telegram-bot/core/LICENSE)

## 目录
- [简介](#introduction)
- [说明](#instructions)
    - [创建你的第一个机器人](#create-your-first-bot)
    - [使用 Composer 安装此包](#require-this-package-with-composer)
    - [选择获取 Telegram 更新的方式](#choose-how-to-retrieve-telegram-updates)
- [使用自定义的 Bot API 服务器](#using-a-custom-bot-api-server)
- [Webhook 安装](#webhook-installation)
    - [自签名证书](#self-signed-certificate)
    - [取消 Webhook](#unset-webhook)
- [getUpdates 安装](#getupdates-installation)
    - [无数据库的 getUpdates](#getupdates-without-database)
- [过滤更新](#filter-update)
- [支持](#support)
    - [类型](#types)
    - [内联查询](#inline-query)
    - [方法](#methods)
    - [发送消息](#send-message)
    - [发送照片](#send-photo)
    - [发送聊天动作](#send-chat-action)
    - [getUserProfilePhoto](#getuserprofilephoto)
    - [getFile 和 downloadFile](#getfile-and-downloadfile)
    - [向所有活跃聊天发送消息](#send-message-to-all-active-chats)
- [实用工具](#utils)
    - [MySQL 存储 (推荐)](#mysql-storage-recommended)
        - [外部数据库连接](#external-database-connection)
    - [频道支持](#channels-support)
- [命令](#commands)
    - [预定义命令](#predefined-commands)
    - [自定义命令](#custom-commands)
    - [命令配置](#commands-configuration)
    - [管理员命令](#admin-commands)
        - [设置管理员](#set-admins)
        - [频道管理](#channel-administration)
- [上传和下载目录路径](#upload-and-download-directory-path)
- [日志记录](doc/01-utils.md)
- [文档](#documentation)
- [资源](#assets)
- [示例机器人](#example-bot)
- [使用此库的项目](#projects-with-this-library)
- [故障排除](#troubleshooting)
- [贡献](#contributing)
- [安全](#security)
- [捐赠](#donate)
- [针对企业](#for-enterprise)
- [许可证](#license)
- [致谢](#credits)

## 简介

这是一个纯 PHP 编写的 Telegram 机器人，可以通过插件进行完全扩展。

Telegram 宣布了对 [Bot API](https://telegram.org/blog/bot-revolution) 的官方支持，使各类集成者可以将自动化交互引入移动平台。
该机器人旨在提供一个平台，让用户可以简单地编写机器人并在几分钟内实现交互。

机器人可以：
- 使用 [webhook](#webhook-installation) 和 [getUpdates](#getupdates-installation) 方法获取更新。
- 支持所有类型和方法，符合 Telegram Bot API 7.1（2024 年 2 月）。
- 支持超级群组。
- 处理与其他机器人聊天中的命令。
- 从机器人管理员界面管理频道。
- 完全支持 **内联机器人**。
- 内联键盘。
- 消息、InlineQuery 和 ChosenInlineQuery 被存储在数据库中。
- 会话功能。

---

该代码可在 [GitHub](https://github.com/php-telegram-bot/core) 上找到。欢迎提交拉取请求。

## 说明

### 创建你的第一个机器人

1. 向 [`@BotFather`](https://telegram.me/BotFather) 发送以下文本：`/newbot`

   如果你不知道如何通过用户名发送消息，点击 Telegram 应用的搜索字段，输入 `@BotFather`，然后你就可以开始对话了。小心不要发给错误的联系人，因为有些用户的用户名与 `BotFather` 类似。

   ![BotFather 初始对话](https://user-images.githubusercontent.com/9423417/60736229-bc2aeb80-9f45-11e9-8d35-5b53145347bc.png)

2. `@BotFather` 回复：

    ```
    好的，一个新机器人。我们打算怎么称呼它？请为你的机器人选择一个名字。
    ```

3. 输入你想为机器人起的名字。

4. `@BotFather` 回复：

    ```
    好。现在我们来为你的机器人选择一个用户名。它必须以 `bot` 结尾。例如：TetrisBot 或 tetris_bot。
    ```

5. 输入你想要的用户名，最少 5 个字符，并且必须以 `bot` 结尾。例如：`telesample_bot`

6. `@BotFather` 回复：

    ```
    完成！恭喜你的新机器人诞生了。你可以在
    telegram.me/telesample_bot 找到它。你现在可以为你的机器人添加描述、简介和头像，查看 /help 以获取命令列表。

    使用此令牌访问 HTTP API：
    123456789:AAG90e14-0f8-40183D-18491dDE

    有关 Bot API 的描述，请参阅此页面：
    https://core.telegram.org/bots/api
    ```

7. 记下上面提到的“令牌”。

*可选设置机器人隐私：*

1. 向 `@BotFather` 发送 `/setprivacy`。

   ![BotFather 后续对话](https://user-images.githubusercontent.com/9423417/60736340-26439080-9f46-11e9-970f-8f33bbe39c5f.png)

2. `@BotFather` 回复：

    ```
    选择一个机器人来更改组消息设置。
    ```

3. 输入（或选择） `@telesample_bot`（更改为你在步骤 5 中设置的用户名，但以 `@` 开头）

4. `@BotFather` 回复：

    ```
    “启用” - 你的机器人将只接收以“/”符号开头或通过用户名提到机器人的消息。
    “禁用” - 你的机器人将接收所有发送到组的消息。
    当前状态为：启用
    ```

5. 输入（或选择）“禁用”以允许你的机器人接收发送到组的所有消息。

6. `@BotFather` 回复：

    ```
    成功！新状态为：禁用。/help
    ```

### 使用 Composer 安装此包

通过 [Composer] 安装此包。
编辑项目的 `composer.json` 文件以要求 `longman/telegram-bot`。

创建 *composer.json* 文件
```json
{
    "name": "yourproject/yourproject",
    "type": "project",
    "require": {
        "php": "^8.1",
        "longman/telegram-bot": "*"
    }
}
```
然后运行 `composer update`

**或**

运行以下命令在你的命令行:

```bash
composer require longman/telegram-bot
```

### 选择如何检索Telegram更新

该机器人可以处理更新 [**Webhook**](#Webhook安装) 或 [**getUpdates**](#getupdates安装) 方法:

||Webhook |getupdates |
|---- |：-----：|：-----：|
|描述|电报将更新直接发送给您的主机|您必须手动获取电报更新|
|主持人https |必需|不需要|
|mysql |不需要|（[非]（＃getupdates-without-database））必需|

## Using a custom Bot API server

**For advanced users only!**

As from Telegram Bot API 5.0, users can [run their own Bot API server] to handle updates.
This means, that the PHP Telegram Bot needs to be configured to serve that custom URI.
Additionally, you can define the URI where uploaded files to the bot can be downloaded (note the `{API_KEY}` placeholder).

```php
Longman\TelegramBot\Request::setCustomBotApiUri(
    $api_base_uri          = 'https://your-bot-api-server', // Default: https://api.telegram.org
    $api_base_download_uri = '/path/to/files/{API_KEY}'     // Default: /file/bot{API_KEY}
);
```

**Note:** If you are running your bot in `--local` mode, you won't need the `Request::downloadFile()` method, since you can then access your files directly from the absolute path returned by `Request::getFile()`.

## Webhook installation

Note: For a more detailed explanation, head over to the [example-bot repository] and follow the instructions there.

In order to set a [Webhook][api-setwebhook] you need a server with HTTPS and composer support.
(For a [self signed certificate](#self-signed-certificate) you need to add some extra code)

Create *[set.php]* with the following contents:
```php
<?php
// Load composer
require __DIR__ . '/vendor/autoload.php';

$bot_api_key  = 'your:bot_api_key';
$bot_username = 'username_bot';
$hook_url     = 'https://your-domain/path/to/hook.php';

try {
    // Create Telegram API object
    $telegram = new Longman\TelegramBot\Telegram($bot_api_key, $bot_username);

    // Set webhook
    $result = $telegram->setWebhook($hook_url);
    if ($result->isOk()) {
        echo $result->getDescription();
    }
} catch (Longman\TelegramBot\Exception\TelegramException $e) {
    // log telegram errors
    // echo $e->getMessage();
}
```

Open your *set.php* via the browser to register the webhook with Telegram.
You should see `Webhook was set`.

Now, create *[hook.php]* with the following contents:
```php
<?php
// Load composer
require __DIR__ . '/vendor/autoload.php';

$bot_api_key  = 'your:bot_api_key';
$bot_username = 'username_bot';

try {
    // Create Telegram API object
    $telegram = new Longman\TelegramBot\Telegram($bot_api_key, $bot_username);

    // Handle telegram webhook request
    $telegram->handle();
} catch (Longman\TelegramBot\Exception\TelegramException $e) {
    // Silence is golden!
    // log telegram errors
    // echo $e->getMessage();
}
```

### Self Signed Certificate

Upload the certificate and add the path as a parameter in *set.php*:
```php
$result = $telegram->setWebhook($hook_url, ['certificate' => '/path/to/certificate']);
```

### Unset Webhook

Edit *[unset.php]* with your bot credentials and execute it.

## getUpdates installation

For best performance, the MySQL database should be enabled for the `getUpdates` method!

Create *[getUpdatesCLI.php]* with the following contents:
```php
#!/usr/bin/env php
<?php
require __DIR__ . '/vendor/autoload.php';

$bot_api_key  = 'your:bot_api_key';
$bot_username = 'username_bot';

$mysql_credentials = [
   'host'     => 'localhost',
   'port'     => 3306, // optional
   'user'     => 'dbuser',
   'password' => 'dbpass',
   'database' => 'dbname',
];

try {
    // Create Telegram API object
    $telegram = new Longman\TelegramBot\Telegram($bot_api_key, $bot_username);

    // Enable MySQL
    $telegram->enableMySql($mysql_credentials);

    // Handle telegram getUpdates request
    $telegram->handleGetUpdates();
} catch (Longman\TelegramBot\Exception\TelegramException $e) {
    // log telegram errors
    // echo $e->getMessage();
}
```

Next, give the file permission to execute:
```bash
$ chmod +x getUpdatesCLI.php
```

Lastly, run it!
```bash
$ ./getUpdatesCLI.php
```

### getUpdates without database

If you choose to / or are obliged to use the `getUpdates` method without a database, you can replace the `$telegram->enableMySql(...);` line above with:
```php
$telegram->useGetUpdatesWithoutDatabase();
```

## Filter Update

:exclamation: Note that by default, Telegram will send any new update types that may be added in the future. This may cause commands that don't take this into account to break!

It is suggested that you specifically define which update types your bot can receive and handle correctly.

You can define which update types are sent to your bot by defining them when setting the [webhook](#webhook-installation) or passing an array of allowed types when using [getUpdates](#getupdates-installation).

```php
use Longman\TelegramBot\Entities\Update;

// For all update types currently implemented in this library:
// $allowed_updates = Update::getUpdateTypes();

// Define the list of allowed Update types manually:
$allowed_updates = [
    Update::TYPE_MESSAGE,
    Update::TYPE_CHANNEL_POST,
    // etc.
];

// When setting the webhook.
$telegram->setWebhook($hook_url, ['allowed_updates' => $allowed_updates]);

// When handling the getUpdates method.
$telegram->handleGetUpdates(['allowed_updates' => $allowed_updates]);
```

Alternatively, Update processing can be allowed or denied by defining a custom update filter.

Let's say we only want to allow messages from a user with ID `428`, we can do the following before handling the request:

```php
$telegram->setUpdateFilter(function (Update $update, Telegram $telegram, &$reason = 'Update denied by update_filter') {
    $user_id = $update->getMessage()->getFrom()->getId();
    if ($user_id === 428) {
        return true;
    }

    $reason = "Invalid user with ID {$user_id}";
    return false;
});
```

The reason for denying an update can be defined with the `$reason` parameter. This text gets written to the debug log.

## Support

### Types

All types are implemented according to Telegram API 7.1 (February 2024).

### Inline Query

Full support for inline query according to Telegram API 7.1 (February 2024).

### Methods

All methods are implemented according to Telegram API 7.1 (February 2024).

#### Send Message

Messages longer than 4096 characters are split up into multiple messages.

```php
$result = Request::sendMessage([
    'chat_id' => $chat_id,
    'text'    => 'Your utf8 text 😜 ...',
]);
```

#### Send Photo

To send a local photo, add it properly to the `$data` parameter using the file path:

```php
$result = Request::sendPhoto([
    'chat_id' => $chat_id,
    'photo'   => Request::encodeFile('/path/to/pic.jpg'),
]);
```

If you know the `file_id` of a previously uploaded file, just use it directly in the data array:

```php
$result = Request::sendPhoto([
    'chat_id' => $chat_id,
    'photo'   => 'AAQCCBNtIhAoAAss4tLEZ3x6HzqVAAqC',
]);
```

To send a remote photo, use the direct URL instead:

```php
$result = Request::sendPhoto([
    'chat_id' => $chat_id,
    'photo'   => 'https://example.com/path/to/pic.jpg',
]);
```

*sendAudio*, *sendDocument*, *sendAnimation*, *sendSticker*, *sendVideo*, *sendVoice* and *sendVideoNote* all work in the same way, just check the [API documentation](https://core.telegram.org/bots/api#sendphoto) for the exact usage.
See the *[ImageCommand.php]* for a full example.

#### Send Chat Action

```php
Request::sendChatAction([
    'chat_id' => $chat_id,
    'action'  => Longman\TelegramBot\ChatAction::TYPING,
]);
```

#### getUserProfilePhoto

Retrieve the user photo. (see *[WhoamiCommand.php]* for a full example)

#### getFile and downloadFile

Get the file path and download it. (see *[WhoamiCommand.php]* for a full example)

#### Send message to all active chats

To do this you have to enable the MySQL connection.
Here's an example of use (check [`DB::selectChats()`][DB::selectChats] for parameter usage):

```php
$results = Request::sendToActiveChats(
    'sendMessage', // Callback function to execute (see Request.php methods)
    ['text' => 'Hey! Check out the new features!!'], // Param to evaluate the request
    [
        'groups'      => true,
        'supergroups' => true,
        'channels'    => false,
        'users'       => true,
    ]
);
```

You can also broadcast a message to users, from the private chat with your bot. Take a look at the [admin commands](#admin-commands) below.

## Utils

### MySQL storage (Recommended)

If you want to save messages/users/chats for further usage in commands, create a new database (`utf8mb4_unicode_520_ci`), import *[structure.sql]* and enable MySQL support BEFORE `handle()` method:

```php
$mysql_credentials = [
   'host'     => 'localhost',
   'port'     => 3306, // optional
   'user'     => 'dbuser',
   'password' => 'dbpass',
   'database' => 'dbname',
];

$telegram->enableMySql($mysql_credentials);
```

You can set a custom prefix to all the tables while you are enabling MySQL:

```php
$telegram->enableMySql($mysql_credentials, $bot_username . '_');
```

You can also store inline query and chosen inline query data in the database.

#### External Database connection

It is possible to provide the library with an external MySQL PDO connection.
Here's how to configure it:

```php
$telegram->enableExternalMySql($external_pdo_connection);
//$telegram->enableExternalMySql($external_pdo_connection, $table_prefix)
```
### Channels Support

All methods implemented can be used to manage channels.
With [admin commands](#admin-commands) you can manage your channels directly with your bot private chat.

## Commands

### Predefined Commands

The bot is able to recognise commands in a chat with multiple bots (/command@mybot).

It can also execute commands that get triggered by events, so-called Service Messages.

### Custom Commands

Maybe you would like to develop your own commands.
There is a guide to help you [create your own commands][wiki-create-your-own-commands].

Also, be sure to have a look at the [example commands][ExampleCommands-folder] to learn more about custom commands and how they work.

You can add your custom commands in different ways:

```php
// Add a folder that contains command files
$telegram->addCommandsPath('/path/to/command/files');
//$telegram->addCommandsPaths(['/path/to/command/files', '/another/path']);

// Add a command directly using the class name
$telegram->addCommandClass(MyCommand::class);
//$telegram->addCommandClasses([MyCommand::class, MyOtherCommand::class]);
```

### Commands Configuration

With this method you can set some command specific parameters, for example:

```php
// Google geocode/timezone API key for /date command
$telegram->setCommandConfig('date', [
    'google_api_key' => 'your_google_api_key_here',
]);

// OpenWeatherMap API key for /weather command
$telegram->setCommandConfig('weather', [
    'owm_api_key' => 'your_owm_api_key_here',
]);
```

### Admin Commands

Enabling this feature, the bot admin can perform some super user commands like:
- List all the chats started with the bot */chats*
- Clean up old database entries */cleanup*
- Show debug information about the bot */debug*
- Send message to all chats */sendtoall*
- Post any content to your channels */sendtochannel*
- Inspect a user or a chat with */whois*

Take a look at all default admin commands stored in the *[src/Commands/AdminCommands/][AdminCommands-folder]* folder.

#### Set Admins

You can specify one or more admins with this option:

```php
// Single admin
$telegram->enableAdmin(your_telegram_user_id);

// Multiple admins
$telegram->enableAdmins([
    your_telegram_user_id,
    other_telegram_user_id,
]);
```
Telegram user id can be retrieved with the *[/whoami][WhoamiCommand.php]* command.

#### Channel Administration

To enable this feature follow these steps:
- Add your bot as channel administrator, this can be done with any Telegram client.
- Enable admin interface for your user as explained in the admin section above.
- Enter your channel name as a parameter for the *[/sendtochannel][SendtochannelCommand.php]* command:
```php
$telegram->setCommandConfig('sendtochannel', [
    'your_channel' => [
        '@type_here_your_channel',
    ]
]);
```
- If you want to manage more channels:
```php
$telegram->setCommandConfig('sendtochannel', [
    'your_channel' => [
        '@type_here_your_channel',
        '@type_here_another_channel',
        '@and_so_on',
    ]
]);
```
- Enjoy!

## Upload and Download directory path

To use the Upload and Download functionality, you need to set the paths with:
```php
$telegram->setDownloadPath('/your/path/Download');
$telegram->setUploadPath('/your/path/Upload');
```

## Documentation

Take a look at the repo [Wiki] for further information and tutorials!
Feel free to improve!

## Assets

All project assets can be found in the [assets](https://github.com/php-telegram-bot/assets) repository.

## Example bot

We're busy working on a full A-Z example bot, to help get you started with this library and to show you how to use all its features.
You can check the progress of the [example-bot repository]).

## Projects with this library

Here's a list of projects that feats this library, feel free to add yours!
- [Inline Games](https://github.com/jacklul/inlinegamesbot) ([@inlinegamesbot](https://telegram.me/inlinegamesbot))
- [Super-Dice-Roll](https://github.com/RafaelDelboni/Super-Dice-Roll) ([@superdiceroll_bot](https://telegram.me/superdiceroll_bot))
- [tg-mentioned-bot](https://github.com/gruessung/tg-mentioned-bot)
- [OSMdeWikiBot](https://github.com/OSM-de/TelegramWikiBot) ([@OSM_de](https://t.me/OSM_de))
- [pass-generator-webbot](https://github.com/OxMohsen/pass-generator-webbot)
- [Chess Quiz Bot](https://github.com/1int/chess-quiz-bot)
- [PHP Telegram Bot - Symfony Bundle](https://github.com/m4n50n/telegram_bot_bundle)

## Troubleshooting

If you like living on the edge, please report any bugs you find on the [PHP Telegram Bot issues][issues] page.

## Contributing

See [CONTRIBUTING](CONTRIBUTING.md) for more information.

## Security

See [SECURITY](SECURITY.md) for more information.

## Donate

All work on this bot consists of many hours of coding during our free time, to provide you with a Telegram Bot library that is easy to use and extend.
If you enjoy using this library and would like to say thank you, donations are a great way to show your support.

Donations are invested back into the project :+1:

Thank you for keeping this project alive :pray:

- [![Patreon](https://user-images.githubusercontent.com/9423417/59235980-a5fa6b80-8be3-11e9-8ae7-020bc4ae9baa.png) Patreon.com/phptelegrambot][Patreon]
- [![OpenCollective](https://user-images.githubusercontent.com/9423417/59235978-a561d500-8be3-11e9-89be-82ec54be1546.png) OpenCollective.com/php-telegram-bot][OpenCollective]
- [![Ko-fi](https://user-images.githubusercontent.com/9423417/59235976-a561d500-8be3-11e9-911d-b1908c3e6a33.png) Ko-fi.com/phptelegrambot][Ko-fi]
- [![Tidelift](https://user-images.githubusercontent.com/9423417/59235982-a6930200-8be3-11e9-8ac2-bfb6991d80c5.png) Tidelift.com/longman/telegram-bot][Tidelift]
- [![Liberapay](https://user-images.githubusercontent.com/9423417/59235977-a561d500-8be3-11e9-9d16-bc3b13d3ceba.png) Liberapay.com/PHP-Telegram-Bot][Liberapay]
- [![PayPal](https://user-images.githubusercontent.com/9423417/59235981-a5fa6b80-8be3-11e9-9761-15eb7a524cb0.png) PayPal.me/noplanman][PayPal-noplanman] (account of @noplanman)
- [![Bitcoin](https://user-images.githubusercontent.com/9423417/59235974-a4c93e80-8be3-11e9-9fde-260c821b6eae.png) 166NcyE7nDxkRPWidWtG1rqrNJoD5oYNiV][Bitcoin]
- [![Ethereum](https://user-images.githubusercontent.com/9423417/59235975-a4c93e80-8be3-11e9-8762-7a47c62c968d.png) 0x485855634fa212b0745375e593fAaf8321A81055][Ethereum]

## For enterprise

Available as part of the Tidelift Subscription.

The maintainers of `PHP Telegram Bot` and thousands of other packages are working with Tidelift to deliver commercial support and maintenance for the open source dependencies you use to build your applications. Save time, reduce risk, and improve code health, while paying the maintainers of the exact dependencies you use. [Learn more.][Tidelift]

## License

Please see the [LICENSE](LICENSE) included in this repository for a full copy of the MIT license, which this project is licensed under.

## Credits

Credit list in [CREDITS](CREDITS)

---

[Telegram Bot API]: https://core.telegram.org/bots/api "Telegram Bot API"
[Composer]: https://getcomposer.org/ "Composer"
[run their own Bot API server]: https://core.telegram.org/bots/api#using-a-local-bot-api-server "Using a Local Bot API Server"
[example-bot repository]: https://github.com/php-telegram-bot/example-bot "Example Bot repository"
[api-setwebhook]: https://core.telegram.org/bots/api#setwebhook "Webhook on Telegram Bot API"
[set.php]: https://github.com/php-telegram-bot/example-bot/blob/master/set.php "example set.php"
[unset.php]: https://github.com/php-telegram-bot/example-bot/blob/master/unset.php "example unset.php"
[hook.php]: https://github.com/php-telegram-bot/example-bot/blob/master/hook.php "example hook.php"
[getUpdatesCLI.php]: https://github.com/php-telegram-bot/example-bot/blob/master/getUpdatesCLI.php "example getUpdatesCLI.php"
[AdminCommands-folder]: https://github.com/php-telegram-bot/core/tree/master/src/Commands/AdminCommands "Admin commands folder"
[ExampleCommands-folder]: https://github.com/php-telegram-bot/example-bot/blob/master/Commands "Example commands folder"
[ImageCommand.php]: https://github.com/php-telegram-bot/example-bot/blob/master/Commands/Other/ImageCommand.php "example /image command"
[WhoamiCommand.php]: https://github.com/php-telegram-bot/example-bot/blob/master/Commands/WhoamiCommand.php "example /whoami command"
[HelpCommand.php]: https://github.com/php-telegram-bot/example-bot/blob/master/Commands/HelpCommand.php "example /help command"
[SendtochannelCommand.php]: https://github.com/php-telegram-bot/core/blob/master/src/Commands/AdminCommands/SendtochannelCommand.php "/sendtochannel admin command"
[DB::selectChats]: https://github.com/php-telegram-bot/core/blob/0.70.0/src/DB.php#L1148 "DB::selectChats() parameters"
[structure.sql]: https://github.com/php-telegram-bot/core/blob/master/structure.sql "DB structure for importing"
[Wiki]: https://github.com/php-telegram-bot/core/wiki "PHP Telegram Bot Wiki"
[wiki-create-your-own-commands]: https://github.com/php-telegram-bot/core/wiki/Create-your-own-commands "Create your own commands"
[issues]: https://github.com/php-telegram-bot/core/issues "PHP Telegram Bot Issues"

[Patreon]: https://www.patreon.com/phptelegrambot "Support us on Patreon"
[OpenCollective]: https://opencollective.com/php-telegram-bot "Support us on Open Collective"
[Ko-fi]: https://ko-fi.com/phptelegrambot "Support us on Ko-fi"
[Tidelift]: https://tidelift.com/subscription/pkg/packagist-longman-telegram-bot?utm_source=packagist-longman-telegram-bot&utm_medium=referral&utm_campaign=enterprise&utm_term=repo "Learn more about the Tidelift Subscription"
[Liberapay]: https://liberapay.com/PHP-Telegram-Bot "Donate with Liberapay"
[PayPal-noplanman]: https://paypal.me/noplanman "Donate with PayPal"
[Bitcoin]: https://www.blockchain.com/btc/address/166NcyE7nDxkRPWidWtG1rqrNJoD5oYNiV "Donate with Bitcoin"
[Ethereum]: https://etherscan.io/address/0x485855634fa212b0745375e593fAaf8321A81055 "Donate with Ethereum"
