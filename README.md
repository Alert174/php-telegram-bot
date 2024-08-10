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
- [简介](#简介)
- [说明](#说明)
    - [创建你的第一个机器人](#创建你的第一个机器人)
    - [使用Composer安装此包](#使用Composer安装此包)
    - [选择如何检索Telegram更新](#选择如何检索Telegram更新)
- [使用自定义机器人API服务器](#使用自定义机器人API服务器)
- [Webhook安装](#Webhook安装)
    - [自签名证书](#自签名证书)
    - [取消Webhook](#取消Webhook)
- [getUpdates安装](#getUpdates安装)
    - [无数据库的getUpdates](#无数据库的getUpdates)
- [过滤更新](#过滤更新)
- [支持](#支持)
    - [类型](#类型)
    - [内联查询](#内联查询)
    - [方法](#方法)
    - [发送消息](#发送消息)
    - [发送照片](#发送照片)
    - [发送聊天动作](#发送聊天动作)
    - [getUserProfilePhoto](#getuserprofilephoto)
    - [getFile和downloadFile](#getFile和downloadFile)
    - [向所有活跃聊天发送消息](#向所有活跃的聊天发送消息)
- [实用工具](#实用工具)
    - [MySQL 存储 (推荐)](#MySQL存储（推荐）)
        - [外部数据库连接](#外部数据库连接)
    - [频道支持](#频道支持)
- [命令](#命令)
    - [预定义命令](#预定义命令)
    - [自定义命令](#自定义命令)
    - [命令配置](#命令配置)
    - [管理员命令](#管理员命令)
        - [设置管理员](#设置管理员)
        - [频道管理](#频道管理)
- [上传和下载目录路径](#上传和下载目录路径)
- [日志记录](doc/01-实用工具.md)
- [文档](#文档)
- [资源](#资源)
- [示例机器人](#实例机器人)
- [使用这个库的项目](#使用这个库的项目)
- [疑难解答](#疑难解答)
- [贡献](#贡献)
- [安全](#安全)
- [捐赠](#捐赠)
- [企业支持](#企业支持)
- [许可证](#许可证)
- [致谢](#致谢)

## 简介

这是一个纯 PHP 编写的 Telegram 机器人，可以通过插件进行完全扩展。

Telegram 宣布了对 [Bot API](https://telegram.org/blog/bot-revolution) 的官方支持，使各类集成者可以将自动化交互引入移动平台。
该机器人旨在提供一个平台，让用户可以简单地编写机器人并在几分钟内实现交互。

机器人可以：
- 使用 [webhook](#Webhook安装) 和 [getUpdates](#getUpdates安装) 方法获取更新。
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

### 使用Composer安装此包

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

该机器人可以处理更新 [**Webhook**](#Webhook安装) 或 [**getUpdates**](#getUpdates安装) 方法:

|      | Webhook | getUpdates |
| ---- | :----: | :----: |
| 描述 | Telegram将更新直接发送给您的主机 | 您必须手动获取Telegram 更新 |
| 带有HTTPS的主机 | 必需的 | 不需要 |
| MySQL | 不需要 | ([不](#无数据库的getUpdates)) 需要  |

## 使用自定义机器人API服务器

**仅适用于高级用户！**

从Telegram bot API 5.0中，用户可以 [运行他们自己的Bot API 服务器] to handle updates.
这意味着，需要配置PHPTelegram 机器人以服务于自定义URI。
此外，您可以在可以下载上传到机器人的文件的情况下定义URI（请注意`{api_key}`占位符）。

```php
Longman\TelegramBot\Request::setCustomBotApiUri(
    $api_base_uri          = 'https://your-bot-api-server', // Default: https://api.telegram.org
    $api_base_download_uri = '/path/to/files/{API_KEY}'     // Default: /file/bot{API_KEY}
);
```

**注意：** 如果你在 `--local` 模式下运行你的机器人，你不需要使用 `Request::downloadFile()` 方法，因为你可以直接从 `Request::getFile()` 返回的绝对路径访问你的文件。

## Webhook安装

注意：想要更详细的说明，请访问[示例机器人存储库]并按照那里的指示进行操作。

为了设置 [Webhook][api-setwebhook]，你需要一个支持 HTTPS 和 Composer 的服务器。
（对于[自签名证书](#自签名证书)，你需要添加一些额外的代码）

创建 *[set.php]*，内容如下：

```php
<?php
// 加载 composer
require __DIR__ . '/vendor/autoload.php';

$bot_api_key  = 'your:bot_api_key';
$bot_username = 'username_bot';
$hook_url     = 'https://你的域名/path/to/hook.php';

try {
    // 创建Telegram API对象
    $telegram = new Longman\TelegramBot\Telegram($bot_api_key, $bot_username);

    // 设置 webhook
    $result = $telegram->setWebhook($hook_url);
    if ($result->isOk()) {
        echo $result->getDescription();
    }
} catch (Longman\TelegramBot\Exception\TelegramException $e) {
    // 日志Telegram 错误
    // echo $e->getMessage();
}
```

通过浏览器打开你的 *set.php* 来向 Telegram 注册 webhook。
你应该会看到 `Webhook was set`。

现在，创建 *[hook.php]*，内容如下：

```php
<?php
// 加载 composer
require __DIR__ . '/vendor/autoload.php';

$bot_api_key  = 'your:bot_api_key';
$bot_username = 'username_bot';

try {
    // 创建Telegram API对象
    $telegram = new Longman\TelegramBot\Telegram($bot_api_key, $bot_username);

    // 处理Telegram Webhook请求
    $telegram->handle();
} catch (Longman\TelegramBot\Exception\TelegramException $e) {
    // 沉默是金！
    // 日志Telegram 错误
    // echo $e->getMessage();
}
```

### 自签名证书

上传证书并在 *set.php* 中将其路径作为参数添加：
```php
$result = $telegram->setWebhook($hook_url, ['certificate' => '/path/to/certificate']);
```
### 取消Webhook

编辑 *[unset.php]*，填写你的机器人凭据并执行它。

## getUpdates安装

为了获得最佳性能，建议为 `getUpdates` 方法启用 MySQL 数据库！

创建 *[getUpdatesCLI.php]*，内容如下：
```php
#!/usr/bin/env php
<?php
require __DIR__ . '/vendor/autoload.php';

$bot_api_key  = 'your:bot_api_key';
$bot_username = 'username_bot';

$mysql_credentials = [
   'host'     => 'localhost',
   'port'     => 3306, // 选填
   'user'     => 'dbuser',
   'password' => 'dbpass',
   'database' => 'dbname',
];

try {
    // 创建Telegram API对象
    $telegram = new Longman\TelegramBot\Telegram($bot_api_key, $bot_username);

    // 开启 MySQL
    $telegram->enableMySql($mysql_credentials);

    // 处理Telegram getupdates请求
    $telegram->handleGetUpdates();
} catch (Longman\TelegramBot\Exception\TelegramException $e) {
    // 日志Telegram 错误
    // echo $e->getMessage();
}
```

接下来，授予文件权限以执行：
```bash
$ chmod +x getUpdatesCLI.php
```

最后，运行
```bash
$ ./getUpdatesCLI.php
```
### 无数据库的getUpdates

如果你选择或必须在没有数据库的情况下使用 `getUpdates` 方法，你可以将上面代码中的 `$telegram->enableMySql(...);` 行替换为：
```php
$telegram->useGetUpdatesWithoutDatabase();
```
## 过滤更新

:exclamation: 请注意，默认情况下，Telegram 会发送未来可能添加的任何新更新类型。这可能导致那些没有考虑到这些新类型的命令出现问题！

建议你明确定义你的机器人可以接收和正确处理的更新类型。

你可以在设置 [webhook](#Webhook安装) 时定义发送到机器人哪些更新类型，或者在使用 [getUpdates](#getUpdates安装) 时传递一个允许的类型数组。
```php
use Longman\TelegramBot\Entities\Update;

// 对于当前在此库中实现的所有更新类型：
// $allowed_updates = Update::getUpdate类型();

// 手动定义允许更新类型的列表：
$allowed_updates = [
    Update::TYPE_MESSAGE,
    Update::TYPE_CHANNEL_POST,
    // etc.
];

// 设置Webhook时
$telegram->setWebhook($hook_url, ['allowed_updates' => $allowed_updates]);

// 处理getupdates方法时
$telegram->handleGetUpdates(['allowed_updates' => $allowed_updates]);
```

另外，可以通过定义自定义更新过滤器来允许或拒绝更新处理。

假设我们只想允许来自具有ID为428的用户的消息，我们可以在处理请求之前执行以下操作：
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
拒绝更新的原因可以通过 `$reason` 参数定义。该文本会被写入调试日志。
## 支持

### 类型

所有类型均根据 Telegram API 7.1（2024年2月）实现。

### 内联查询

完全支持内联查询，符合 Telegram API 7.1（2024年2月）。

### 方法

所有方法均根据 Telegram API 7.1（2024年2月）实现。

#### 发送消息

超过 4096 个字符的消息将被分成多个消息发送。
```php
$result = Request::sendMessage([
    'chat_id' => $chat_id,
    'text'    => 'Your utf8 text 😜 ...',
]);
```
#### 发送照片

要发送本地照片，请使用文件路径正确地将其添加到 `$data` 参数中：

```php
$result = Request::sendPhoto([
    'chat_id' => $chat_id,
    'photo'   => Request::encodeFile('/path/to/pic.jpg'),
]);
```
如果你知道先前上传文件的 `file_id`，只需直接在数据数组中使用它：

```php
$result = Request::sendPhoto([
    'chat_id' => $chat_id,
    'photo'   => 'AAQCCBNtIhAoAAss4tLEZ3x6HzqVAAqC',
]);
```

要发送远程照片，请改用直接URL：

```php
$result = Request::sendPhoto([
    'chat_id' => $chat_id,
    'photo'   => 'https://example.com/path/to/pic.jpg',
]);
```
*sendAudio*、*sendDocument*、*sendAnimation*、*sendSticker*、*sendVideo*、*sendVoice* 和 *sendVideoNote* 的工作方式都相同，只需查看 [API 文档](https://core.telegram.org/bots/api#sendphoto) 以获取具体的使用方法。
请参阅 *[ImageCommand.php]* 获取完整示例。

#### 发送聊天动作

```php
Request::sendChatAction([
    'chat_id' => $chat_id,
    'action'  => Longman\TelegramBot\ChatAction::TYPING,
]);
```

#### getUserProfilePhoto

获取用户照片。（查看 *[WhoamiCommand.php]* 以获取完整示例）

#### getFile和downloadFile

获取文件路径并下载文件。（查看 *[WhoamiCommand.php]* 以获取完整示例）

#### 向所有活跃的聊天发送消息

要实现此功能，你需要启用 MySQL 连接。
以下是一个使用示例（查看 [`DB::selectChats()`][DB::selectChats] 了解参数用法）：

```php
$results = Request::sendToActiveChats(
    'sendMessage', // 回调函数要执行 (详见 Request.php 方法)
    ['text' => 'Hey! Check out the new features!!'], // Param to evaluate the request
    [
        'groups'      => true,
        'supergroups' => true,
        'channels'    => false,
        'users'       => true,
    ]
);
```

你也可以从与你的机器人私聊中向用户广播消息。请查看下面的 [管理员命令](#admin-commands)。

## 实用工具

### MySQL存储（推荐）

如果你想保存消息/用户/聊天以便在命令中进一步使用，创建一个新的数据库（`utf8mb4_unicode_520_ci`），导入 *[structure.sql]*，并在 `handle()` 方法之前启用 MySQL 支持：

```php
$mysql_credentials = [
   'host'     => 'localhost',
   'port'     => 3306, // 选填
   'user'     => 'dbuser',
   'password' => 'dbpass',
   'database' => 'dbname',
];

$telegram->enableMySql($mysql_credentials);
```

在启用MySQL时，您可以为所有表设置自定义前缀：

```php
$telegram->enableMySql($mysql_credentials, $bot_username . '_');
```

您还可以在数据库中存储内联查询和选择的外线查询数据。

#### 外部数据库连接

可以为该库提供一个外部的 MySQL PDO 连接。
以下是配置方法：

```php
$telegram->enableExternalMySql($external_pdo_connection);
//$telegram->enableExternalMySql($external_pdo_connection, $table_prefix)
```
### 频道支持

所有已实现的方法都可以用于管理频道。
通过 [管理员命令](#admin-commands)，你可以直接通过与你的机器人私聊来管理你的频道。

## 命令

### 预定义命令

机器人能够在与多个机器人聊天时识别命令（/command@mybot）。

它还可以执行由事件触发的命令，即所谓的服务消息。

### 自定义命令

你可能想开发自己的命令。
这里有一份指南可以帮助你[创建自己的命令][wiki-create-your-own-commands]。

此外，一定要查看[示例命令][ExampleCommands-folder]，以了解更多关于自定义命令及其工作方式的信息。

你可以通过不同的方式添加自定义命令：

```php
// 添加一个包含命令文件的文件夹
$telegram->addCommandsPath('/path/to/command/files');
//$telegram->addCommandsPaths(['/path/to/command/files', '/another/path']);

// 使用类名直接添加命令
$telegram->addCommandClass(MyCommand::class);
//$telegram->addCommandClasses([MyCommand::class, MyOtherCommand::class]);
```
### 命令配置

通过这种方法，你可以设置一些特定命令的参数，例如：

```php
// Google geocode/timezone API key 用于 /date 命令
$telegram->setCommandConfig('date', [
    'google_api_key' => 'your_google_api_key_here',
]);

// OpenWeatherMap API key 用于 /weather 命令
$telegram->setCommandConfig('weather', [
    'owm_api_key' => 'your_owm_api_key_here',
]);
```
### 管理员命令

启用此功能后，机器人管理员可以执行一些超级用户命令，例如：
- 列出所有与机器人开始的聊天 */chats*
- 清理旧的数据库条目 */cleanup*
- 显示有关机器人的调试信息 */debug*
- 向所有聊天发送消息 */sendtoall*
- 向你的频道发布任何内容 */sendtochannel*
- 使用 */whois* 检查用户或聊天

查看存储在 *[src/Commands/AdminCommands/][AdminCommands-folder]* 文件夹中的所有默认管理员命令。

#### 设置管理员

你可以使用此选项指定一个或多个管理员：

```php
// 单个管理员
$telegram->enableAdmin(your_telegram_user_id);

// 多个管理员
$telegram->enableAdmins([
    your_telegram_user_id,
    other_telegram_user_id,
]);
```
Telegram 用户 ID 可以通过 *[/whoami][WhoamiCommand.php]* 命令获取。

#### 频道管理

要启用此功能，请按照以下步骤操作：
- 将你的机器人添加为频道管理员，这可以通过任何 Telegram 客户端完成。
- 按照上面管理部分的说明，为你的用户启用管理员界面。
- 将你的频道名称作为 *[/sendtochannel][SendtochannelCommand.php]* 命令的参数输入：

```php
$telegram->setCommandConfig('sendtochannel', [
    'your_channel' => [
        '@type_here_your_channel',
    ]
]);
```
- 如果你想管理更多频道：
```php
$telegram->setCommandConfig('sendtochannel', [
    'your_channel' => [
        '@type_here_your_channel',
        '@type_here_another_channel',
        '@and_so_on',
    ]
]);
```
- 享受吧！

## 上传和下载目录路径

要使用上传和下载功能，你需要设置路径：
```php
$telegram->setDownloadPath('/your/path/Download');
$telegram->setUploadPath('/your/path/Upload');
```

## 文档

查看仓库中的 [Wiki] 以获取更多信息和教程！
欢迎改进！

## 资源

所有项目资源都可以在 [assets](https://github.com/php-telegram-bot/assets) 仓库中找到。

## 示例机器人

我们正在努力创建一个完整的 A-Z 示例机器人，以帮助你开始使用这个库，并展示如何使用其所有功能。
你可以查看 [示例机器人存储库] 的进展。

## 使用这个库的项目

以下是使用此库的一些项目列表，欢迎添加你的项目！
- [Inline Games](https://github.com/jacklul/inlinegamesbot) ([@inlinegamesbot](https://telegram.me/inlinegamesbot))
- [Super-Dice-Roll](https://github.com/RafaelDelboni/Super-Dice-Roll) ([@superdiceroll_bot](https://telegram.me/superdiceroll_bot))
- [tg-mentioned-bot](https://github.com/gruessung/tg-mentioned-bot)
- [OSMdeWikiBot](https://github.com/OSM-de/TelegramWikiBot) ([@OSM_de](https://t.me/OSM_de))
- [pass-generator-webbot](https://github.com/OxMohsen/pass-generator-webbot)
- [Chess Quiz Bot](https://github.com/1int/chess-quiz-bot)
- [PHP Telegram Bot - Symfony Bundle](https://github.com/m4n50n/telegram_bot_bundle)
## 疑难解答

如果你喜欢追求最新版本，请在 [PHP Telegram Bot issues][issues] 页面报告你发现的任何错误。

## 贡献

有关更多信息，请参阅 [CONTRIBUTING](CONTRIBUTING.md)。

## 安全

有关更多信息，请参阅 [SECURITY](SECURITY.md)。

## 捐赠

这个机器人项目的所有工作都由我们在空闲时间进行的编程工作组成，目的是为你提供一个易于使用和扩展的 Telegram 机器人库。
如果你喜欢使用这个库并想表达谢意，捐赠是表示支持的好方法。

捐款将被重新投资到项目中 :+1:

感谢你让这个项目得以持续 :pray:

- [![Patreon](https://user-images.githubusercontent.com/9423417/59235980-a5fa6b80-8be3-11e9-8ae7-020bc4ae9baa.png) Patreon.com/phptelegrambot][Patreon]
- [![OpenCollective](https://user-images.githubusercontent.com/9423417/59235978-a561d500-8be3-11e9-89be-82ec54be1546.png) OpenCollective.com/php-telegram-bot][OpenCollective]
- [![Ko-fi](https://user-images.githubusercontent.com/9423417/59235976-a561d500-8be3-11e9-911d-b1908c3e6a33.png) Ko-fi.com/phptelegrambot][Ko-fi]
- [![Tidelift](https://user-images.githubusercontent.com/9423417/59235982-a6930200-8be3-11e9-8ac2-bfb6991d80c5.png) Tidelift.com/longman/telegram-bot][Tidelift]
- [![Liberapay](https://user-images.githubusercontent.com/9423417/59235977-a561d500-8be3-11e9-9d16-bc3b13d3ceba.png) Liberapay.com/PHP-Telegram-Bot][Liberapay]
- [![PayPal](https://user-images.githubusercontent.com/9423417/59235981-a5fa6b80-8be3-11e9-9761-15eb7a524cb0.png) PayPal.me/noplanman][PayPal-noplanman] (账号 @noplanman)
- [![Bitcoin](https://user-images.githubusercontent.com/9423417/59235974-a4c93e80-8be3-11e9-9fde-260c821b6eae.png) 166NcyE7nDxkRPWidWtG1rqrNJoD5oYNiV][Bitcoin]
- [![Ethereum](https://user-images.githubusercontent.com/9423417/59235975-a4c93e80-8be3-11e9-8762-7a47c62c968d.png) 0x485855634fa212b0745375e593fAaf8321A81055][Ethereum]

## 企业支持

可作为 Tidelift 订阅的一部分。

`PHP Telegram Bot` 的维护者和其他数千个软件包的开发者正在与 Tidelift 合作，为你构建应用程序所使用的开源依赖项提供商业支持和维护。节省时间，降低风险，并改善代码健康状况，同时支付你所使用的确切依赖项的维护者。 [了解更多。][Tidelift]

## 许可证

请参阅此仓库中包含的 [LICENSE](LICENSE) 以获取 MIT 许可证的完整副本，此项目基于此许可证。

## 致谢

致谢名单见 [CREDITS](CREDITS)

---

[Telegram Bot API]: https://core.telegram.org/bots/api "Telegram Bot API"
[Composer]: https://getcomposer.org/ "Composer"
[运行他们自己的Bot API 服务器]: https://core.telegram.org/bots/api#using-a-local-bot-api-server "Using a Local Bot API Server"
[示例机器人存储库]: https://github.com/php-telegram-bot/example-bot "Example Bot repository"
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
