<!---
  Created by TheRacingLion (https://github.com/TheRacingLion) [ 6 / 12 / 2016 ]
  -*Read LICENSE to know more about permissions*-

  Readme File. Everything there is to know about this awesome selfbot.
-->
<div align="center">
  <h1 align="center">~ Discord Selfbot ~</h1>
    **A selfbot for discord that is setup and ready to go in less than 5 min.**<br />(If you already have the required programs installed)<br /><br />
    [![Standard - JavaScript Style Guide](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/feross/standard)
</div><br />

# Before Setup

Please remember that selfbots arent fully suported by Discord and that it should only be used to make YOUR life easier and not others. Also keep in mind that discord has a set of semi-offical rules regarding selfbots:

+ A selfbot must not, under any circumstance, respond to other user's messages. This means it should not respond to commands, should not autoreply to certain keywords, etc. You must be the only one that can control it.
+ A selfbot must not, under any circumstance, do "invite scraping". This is the action of detecting server invites in chat, and automatically joining a server using that invite. That is akin to creating a virus, and it is not acceptable.
+ As selfbots run under your account they are subject to the same Terms of Service. That is to say, they should not spam, insult or demean others, post NSFW material, spread viruses or illegal material, etc. They have to follow the same rules that you follow.

IF, and only if you accept the above rules of selfbots, then you may proceed.

# SelfBot Setup

### - Install Required Programs -

Before you can download and setup the bot, there are 2 programs you need to have installed on your computer to make sure everything runs on first go:

- [**Git**](https://git-scm.com/downloads)
- [**Node JS**](https://nodejs.org/en/download/current/)

### - Download Project Files -

After you have the required programs installed, you can go ahead and download the ZIP folder that has all project files. Once you finish downloading it, unzip it and you will be ready to setup the config files.

### - Setup Config Files -

Once you download the project files you will see a folder named `config`. Inside of it will be 3 files:

- `config.json`
- `games.json`
- `paste.json`

#### `config.json`

This is the main config file. Inside you will see several options, this is what each one means:

- `token` is your discord token. (if you dont know what a discord token is, or how to get yours [**check out this tutorial made by me**](https://github.com/TheRacingLion/Discord-SelfBot/wiki/Discord-Token-Tutorial))
- `ownerID` is your discord ID
- `prefix` is the desired prefix for bot commands (can use `@mention ` if you want the prefix to be your discord mention)
- `rotatePlayingGame`, if you want your discord playing game to rotate games (from the `games.json` file)
- `rotatePlayingGameTime`, if you do want the game to rotate, this is the time interval you want for it (in milliseconds)
- `defaultStatus`, the default discord status to show on your account. Either "online", "idle", "dnd" (Do Not Disturb) or "invisible"
- `mentionNotificator` (if you want to have your mentions notified)
  + `inConsole` (as a log to console)
  + `inNotificationChannel` (as a message sent to the notification channel)
- `eventNotificator` (if you want to have events like guild creations, or friend requests notified)
  + `inConsole` (as a log to console)
  + `inNotificationChannel` (as a message sent to the notification channel)
- `notificationChannelID`, if you set `inNotificationChannel` to `true` at least once, the channel ID to make notifications in
- `defaultEmbedColor` is the hex color code for the default color for embeds
- `deleteCommandMessages` if command messages and error messages should be deleted after a bit

#### `games.json`

This is where the game names you want to use for the rotating playing game option are. To add or delete games, just follow the structure of the games that are already on it. (If you have set the `rotatePlayingGame` option in the `config.json` file to `false`, then you dont need to worry about this file)

#### `paste.json`

This file is where the meme texts are stored for the `paste` command, if you wish to add more to use with `paste` just follow the structure of the file and add them in. If an array is specified for one of the options then the bot will choose a random item from the array.

### - Start the bot -

When you have the required programs installed, have all project files, and have setup config files, you can open the `installer.bat` file. This will install the required node modules (so you dont have to do it yourself) and then start the bot up. If you did everything correctly, the bot should start up fine.

#### `installer.bat`
If for some reason you have ran `installer.bat`, it disapeared and it didnt create `run.bat`, then re-download `installer.bat` and try again. Most likely either git or node were not installed correctly. Check if they work and try again.

# Commands

All commands get logged to console, are case insensentive and are tested to see if the owner of the bot was the one who triggered the command. It should be easy to create commands if you know the basics of javascript. The library used is [**Eris**](https://abal.moe/Eris/docs/CommandClient#function-registerCommand).

### - Default Commands -

There are 13 default commands that come with the bot. (Each command is explained inside their own file.) Check out all commands and how they work [**here.**](https://github.com/TheRacingLion/Discord-SelfBot/wiki)

### - Creating Commands -

When you want to create a new command, just add a new file to the `commands` folder and name it something like `mycommand.js` and then follow this basic structure:

```js
/*
  Optional comment string to describe the command.
*/
module.exports = (self, log) => {
  self.registerCommand('mycommand', (msg, args) => {
    // Do something with msg or args
  })
}
```

If your command needs some kind of special options like permissions or you just want to set it to be used on guilds only, then you can use the pre-made command options that come with [**Eris Command Client**](https://abal.moe/Eris/docs/CommandClient#function-registerCommand), like:

```js
module.exports = (self, log) => {
  self.registerCommand('mycommand', (msg, args) => {
    // Do something with msg or args
  }, {
    guildOnly: true, // Will only work on guilds (No PM's)
    requirements: { // Requirements for the command to work
      permissions: {
        'manageChannels': true, // Will only do the command if you have the "Manage channels" permission
        'manageNicknames': true // Will only do the command if you have the "Manage Nicknames" permission
      }
    }
  })
  self.registerCommandAlias('mycmd', 'mycommand') // will make "mycmd" be an alias of "mycommand"
}
```

### - Logging -

The selfbot comes with his own logger file, which includes a few options to log things to console. If you know what you are doing, you can add many more. It uses [**Chalk**](https://www.npmjs.com/package/chalk#colors) to change the color of the logged text, so you can change the colors if you do not like them.

#### Normal Logs

If you just want to log text to console you can do:
```js
log.log('Text you want to log', 'Logger title', 'Chalk color that you want for the logger title', timed)
/*
  Logger title is optional
  Check all chalk colors at https://www.npmjs.com/package/chalk#colors
  "timed" is either true or false. Adds a timestamp to the log. (Default is false)
*/
```

#### Warning Logs

If you want to log a warning to console you can do:
```js
log.warn('Something weird but non-breaking happened', 'Warning origin')
// Warning origin means the place where the warning came from (optional)
```

#### Error Logs

If you want to log errors to console you can do:
```js
let err = 'This is an error'
log.err(err, 'Error origin')
// Error origin means the place where the error came from (optional)
```

# License

[MIT](LICENSE). Copyright (c) 2016 [TheRacingLion](https://github.com/TheRacingLion).
