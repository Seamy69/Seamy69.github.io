
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <title>Ohbot</title>
    <meta name=viewport content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="main.css" />
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Ohbot</h1>
            <div class="nav">
                <a href="/">Info</a><a href="/status.html">Status</a><a href="/commands.html" class="current">Help</a>
            </div>
        </div>
        <div class="info">
            <h2>Instructions</h2>
            <p>
                Commands are entered in chat or via whispers.
                Command prefix is customizable and must be added before all commands in the table when used in chat.
                By default it is <code>!</code>.
                <code>!bot</code> will always reply with the current version of the bot as well as the channel's command prefix regardless of the prefix.
                <code>!permit</code> will also always reply for compatibility with other moderation bots that may be running at the same time.
            </p>
            <p>
                Optional parameters are greyed out.
            </p>
            <h2>Commands</h2>
            <table>
                <thead>
                    <tr>
                        <th style="width:120px">
                            Default<br />
                            Required<br />
                            Access<br />
                            Level
                        </th>
                        <th style="width:100px">
                            Command
                        </th>
                        <th>
                            Parameters
                        </th>
                        <th>
                            Notes
                        </th>
                    </tr>
                </thead>
                <tbody id="commands">
                    
                </tbody>
            </table>
            <h2>
                String Replacements
            </h2>
            <table>
                <thead>
                    <tr>
                        <th>
                            Syntax
                        </th>
                        <th>
                            Notes
                        </th>
                    </tr>
                </thead>
                <tbody id="replacements">

                </tbody>
            </table>
            <h2>
                Common Commands
            </h2>
            <ul>
                <li>Uptime <code>[uptime [0|your_name]]</code></li>
                <li>Roulette <code>[random "/timeout [user] 1" "You survived the roulette!"]</code></li>
                <li>8ball <code>[random "It is certain" "It is decidedly so" "Without a doubt" "Yes definitely" "You may rely on it" "As I see it, yes" "Most likely" "Outlook good" "Yes" "Signs point to yes" "Reply hazy try again" "Ask again later" "Better not tell you now" "Cannot predict now" "Concentrate and ask again" "Don't count on it" "My reply is no" "My sources say no" "Outlook not so good" "Very doubtful"]</code></li>
                <li>How long has been following <code>Time [0|[user]] has been following [1|[channel]]: [datediff [customapi https://api.twitch.tv/kraken/users/[urlencode [0|[user]]]/follows/channels/[urlencode [1|[channel]]]?client_id=YOU_NEED_TO_GET_ONE_AND_REPLACE_THIS $.created_at|]|Not following :(]</code></li>
            </ul>
            <h2>
                Filters
            </h2>
            <p>
                Users with access level above 25 are always immune to all channel filters.
                <ul>
                    <li>caps</li>
                    <li>symbols</li>
                    <li>links</li>
                    <li>repeats (repeated similar phrases within the same message)</li>
                    <li>actions (/me)</li>
                    <li>emotes</li>
                    <li>singles (single emotes)</li>
                    <li>longs (message length in characters)</li>
                    <li>solospam (repeated similar messages from the same person)</li>
                    <li>zalgo</li>
                    <li>bytes (message length in bytes)</li>
                    <li>bttv (global betterttv emotes)</li>
                    <li>r9k (with customizable character limit, unlike Twitch's locked at 9)</li>
                    <li>cheer (for cheering/bits emotes)</li>
                    <li>toxic (a machine-learning toxicity filter powered by <a href="https://www.perspectiveapi.com/#/" rel="external">Perspective</a> - high percentage settings recommended)</li>
                </ul>
                <br />
            </p>
            <h2>
                Access Levels
            </h2>
            <table>
                <thead>
                    <tr>
                        <th>
                            Level
                        </th>
                        <th>
                            Detected Role
                        </th>
                    </tr>
                </thead>
                <tbody id="access">

                </tbody>
            </table>
        </div>
        <div class="header">
            <p>
                <a href="/terms.txt">Terms of Use</a> - <a href="/privacy.txt">Privacy Policy</a>
            </p>
            <p><a href="http://3v.fi/">3v.fi</a></p>
        </div>
    </div>

    <script src="//code.jquery.com/jquery-2.1.4.min.js"></script>
    <script src="common.js"></script>
    <script>
        var commands = [
            [0, "help", "", "Posts a link to this help page."],
            [0, "join", "", "Joins your channel. Only available in <a href=\"http://www.twitch.tv/ohbot\">ohbot's chat</a>."],
            ["Broadcaster", "part", "", "Leaves the current channel."],
            [0, "bot", "", "Posts the bot's name, version and current command prefix on the channel."],
            [30, "test", "<span class=\"optional\">[anything]</span>", "Posts the current time and echoes the optional parameters."],
            [30, "permit", "[username]", "Allows username to post one message with links."],
            [30, "check", "<span class=\"optional\">[username]|all</span>", "Posts your or specified access level(s)."],
            [30, "filtertest", "[channel] [message]", "Test if a message would be timed out and by which filters. Note: you need access to this command on both the channel you're on and the target channel."],
            [30, "filters", "", "Posts current moderation filter status."],
            [30, "level", "[command] [level]", "Changes required access level for a command that you have permission to modify."],
            [30, "set", "mode [access level]", "Changes the minimum access level required to use any command."],
            [30, "set", "subwelcome|subwelcomeback [message]", "Sets a new subscriber welcome message. String replacements supported. Additionally, $lastsub and $months may be used."],
            [30, "set", "prefix [new prefix]", "Changes the command prefix. Defaults to <code>!</code>."],
            [30, "set", "timeout [duration in seconds]", "Changes the default timeout duration for moderation filters."],
            [30, "set", "warning [duration in seconds]", "Changes the default warning timeout duration for moderation filters."],
            [30, "set", "slowmultiplier [multiplier]", "Sets scaling to use for timeout duration and slow mode."],
            [30, "set", "charstowords on|off", "Sets whether space-separated W O R D S are combined to WORDS before regex checks."],
            [30, "set", "replacelookalikes on|off", "Sets whether unicode characters that look like English alphabet characters are replaced before regex checks."],
            [30, "set", "prependname on|nodelim|off", "Prepends the user/display name to the message for regex checks. <code>on</code> results in <code>RocketLeague:message</code> (if display name case-insensitively matches login name) or <code>Riot Games (riotgames):message</code> (if display name does not match login name). <code>nodelim</code> results in <code>riotgamesmessage</code>, uses login name regardless of display name matching."],
            [30, "set", "globalnamecheck on|off", "Sets whether or not the global username filter is used. Default ON."],
            [30, "set", "timezone [name]", "Changes the default timezone for the channel."],
            [30, "set", "timeformat [format]", "Changes the default time output format. <code>U</code> recommended. <a href=\"https://msdn.microsoft.com/en-us/library/az4se3k1%28v=vs.110%29.aspx\" rel=\"external help\">What's this?</a>"],
            [30, "set", "culture [culture]", "Changes the default culture for the channel (e.g. en-US, fi-FI). Affects date outputs with default format"],
            [30, "set", "killpyramids on|off", "Posts a Kappa when people attempt to post emote pyramids in chat."],
            [30, "set", "linkinfo on|off", "Posts additional information about known links, such as Nexus Mods, when seen in chat."],
            [30, "set", "userlevel [username] [new level]", "Changes the user's access level on the channel."],
            [30, "set", "hidechannel on|off", "Hides the channel name from the status page."],
            [30, "set", "league [region] [summoner name]", "Saves your League of Legends account for string replacements. Don't include spaces in your summoner name."],
            [30, "set", "steamid [Steam ID 64]", "Saves your Steam ID for commands that use it."],
            [30, "filter", "[filter] on|off|nosubs", "Changes the moderation filter's status. Nosubs makes subscribers immune."],
            [30, "filter", "[filter] timeout [seconds]", "Changes the filter's timeout duration."],
            [30, "filter", "[filter] reason [message]", "Changes the filter to use a custom timeout message."],
            [30, "filter", "[filter] amount [number]", "Modifies the amount of characters/emotes/symbols/caps/repeats/bytes/messages needed to trigger the filter based on the filter."],
            [30, "filter", "[filter] %|percentage [0-100]", "Modifies the percentage required to match the filter."],
            [30, "filter", "solospam minlength [number]", "Modifies the minimum length of the message to check it."],
            [30, "filter", "solospam seconds [seconds]", "Modifies the duration the filter remembers messages. Max 30 minutes."],
            [30, "filter", "solospam maxmessages [number]", "Sets the maximum allowed amount of messages between a person's spam before the spam is forgotten."],
            [30, "filter", "presets list", "Lists presets in use."],
            [30, "filter", "presets enable [preset]", "Enable a preset on the channel."],
            [30, "filter", "presets disable [preset]", "Disable a preset on the channel."],
            [30, "filter", "findpreset [preset]", "Find enabled nested presets."],
            [30, "filter", "lookalikes list", "Lists lookalike presets in use."],
            [30, "filter", "lookalikes enable [preset]", "Enable a lookalike preset on the channel."],
            [30, "filter", "lookalikes disable [preset]", "Disable a lookalike preset on the channel."],
            [30, "filter", "regexlevel [level]", "Skip regex filter checks for users at or above this level."],
            [30, "command", "add|edit <span class=\"optional\">[required access level]</span> [command name] [reply]", "Adds or edits a command. See string replacements to customize the reply."],
            [30, "command", "remove [id]", "Removes a command."],
            [30, "command", "list", "Lists all commands."],
            [30, "command", "show [command name]", "Shows command output without replacing string replacements."],
            [30, "command", "owner [command name] [username]|off", "Assigns the command to username so no-one else can trigger the command."],
            [30, "command", "repeat [command name] [seconds] [messages]", "Makes the command repeat in chat when the desired amount of seconds and messages have passed in chat since last repeat."],
            [30, "command", "repeat [command name] off", "Stops repeating the command."],
            [30, "whitelist", "add [pattern]", "Whitelists a link. Wildcard partially supported."],
            [30, "whitelist", "remove [id]", "Removes a link pattern from the whitelist."],
            [30, "whitelist", "list", "Lists all whitelisted patterns."],
            [30, "imp (alias r)", "[#channel] <span class=\"optional\">[#msgchannel]</span> [!command] <span class=\"optional\">[params]</span>", "Triggers a command remotely. If msgchannel is specified, the replies will be sent to that channel, otherwise in the channel !imp was used in. You must have permission to use the this command in all affected channels, and the triggered command in the target channel"],
            [30, "persist", "[command]|off", "Persistent command for use with !imp. I.E. &quot;!persist !imp 3ventic&quot; and you only have to type !test for the bot to do !imp 3ventic !test. Persists until turned off."],
            [30, "rooms", "", "Joins all the rooms ohbot can access on the current channel."],
            [32, "banphrase", "add [expression]", "Adds a banned phrase or word. * for wildcard."],
            [32, "banphrase", "add REGEX:[expression]", "Equivalent to !regexp add [expression], see below."],
            [32, "banphrase", "edit [id/name] [expression]", "Edits a banned phrase or word. * for wildcard."],
            [32, "banphrase", "edit [id/name] REGEX:[expression]", "Equivalent to !regexp edit [expression], see below."],
            [32, "regexp", "add [expression]", "Adds a blacklisted pattern, <a href=\"https://msdn.microsoft.com/en-us/library/az24scfc%28v=vs.110%29.aspx\" rel=\"external help\">reference</a>."],
            [32, "regexp", "edit [expression]", "Edits a blacklisted pattern."],
            [32, "regexp (alias banphrase)", "name [id/name] [name]", "Sets a friendly name for the pattern."],
            [32, "regexp (alias banphrase)", "remove [id/name]", "Removes a blacklisted pattern."],
            [32, "regexp (alias banphrase)", "list", "Lists all blacklist patterns."],
            [32, "regexp (alias banphrase)", "timeout [id/name] [duration]", "Modifies the timeout duration caused by this filter, in seconds."],
            [32, "regexp (alias banphrase)", "reason [id/name] [message]", "Modifies the reason message sent to chat when the filter is triggered."],
            [32, "preset", "add [preset]", "Creates a new preset with the current channel as base. The name must be globally unique."],
            [32, "preset", "[preset] timeout [duration]", "See !set timeout"],
            [32, "preset", "[preset] slowmultiplier [multiplier]", "See !set slowmultiplier"],
            [32, "preset", "[preset] warning [duration]", "See !set warning"],
            [32, "preset", "[preset] regex [...]", "See !regex"],
            [32, "preset", "[preset] whitelist [...]", "See !whitelist"],
            [32, "preset", "[preset] filter [...]", "See !filter"],
            [32, "preset", "[preset] filters", "See !filters"],
            [32, "preset", "[preset] charstowords on|off", "See !set charstowords"],
            [32, "preset", "[preset] replacelookalikes on|off", "See !set replacelookalikes"],
            [32, "preset", "[preset] prependname on|nodelim|off", "See !set prependname"],
            [32, "preset", "[preset] remove", "Removes the preset."],
            [32, "preset", "[preset] clone [new preset]", "Clone a preset's settings to a new one, or overwrite an old preset you have access to."],
            [32, "preset", "list", "Lists presets created on the current channel."],
            [32, "lookalikes", "add [name]", "Creates a new lookalike preset. The name must be globally unique."],
            [32, "lookalikes", "[name] define [character or word] [space-separated list of characters or words]", "Defines replacements to do before running regex checks."],
            [32, "lookalikes", "[name] undefine [character or word] [space-separated list of characters or words]", "Undefines replacements."],
            [32, "lookalikes", "[name] remove", "Removes the lookalike preset."],
            [32, "lookalikes", "[name] list", "Lists the replacements in the lookalike preset."],
            [32, "lookalikes", "[name] list [replacement]", "Lists the phrases resulting in the specified replacement in the lookalike preset."],
            [33, "enforce", "slow [min] <span=\"optional\">[max]</span>", "Enforces slow mode between given values. Set min to a negative number to disable."],
            [33, "enforce", "subs|r9k|emote on|off|disable", "Enforces sub-only, r9k or emote-only mode to be enabled or disabled. Set to disable to disable enforcing."],
            ["Broadcaster", "resetohbotentirelyinthischannel", "", "Resets the bot on the channel as if it had never been there before."],
            [0, "query", "[expression]|help", "Evaluates a mathjs expression or links the help page."],
            [0, "define", "[word or phrase]", "Posts the definition for the word or phrase from Wiktionary."],
            [0, "hostlist", "<span class=\"optional\">[channel name]</span>", "Posts hosting channels. Permission \"hostlistother\" governs the optional parameter."],
            [30, "rngmid", "[emote]", "Posts an emote pyramid in chat...or not."]
        ];
        
        var admin_commands = [
            ["Bot Admin / Twitch Staff", "join", "[#channel]", "Sends the <span id=\"admin\">bot</span> to a channel on the chat cluster the channel is currently on. Needs to be rejoined if the cluster changes."],
            ["Bot Admin / Twitch Staff", "botstatus", "<span class=\"optional\">list</span>", "Posts limited status information in chat. For full information, see the status page. Optionally lists joined channels."],
            ["Bot Admin / Twitch Staff", "check", "[#channel]", "Check if the bot is on a specific channel."],
            ["Bot Admin / Twitch Staff", "clone", "[#from] [#to]", "Copy EVERYTHING from the first channel to the second. Never use on channels where !set usechannel is enabled."],
            ["Bot Admin", "echo", "[command reply]", "Send a message in chat. This is passed through the command reply processor so string replies do work here."],
            ["Bot Admin", "hostlist", "[#channel] -f", "Same as hostlist, but posts the whole list in chat no matter how long it is. Please use responsibly."],
            ["Bot Admin", "query", "enable", "Enable the query command again, if it got automatically disabled due to failure."],
            ["Bot Admin", "urlcheck", "[full URL http://...]", "Sends the URL to VirusTotal to be scanned and returns the scan URL. Don't use on public channels. Prefer using the site directly to keep my API limits down."],
            ["Bot Super Admin", "botstate", "[message]", "Change the status message on the status page."],
            ["Bot Super Admin", "command", "global [...]", "Access global commands. See the normal entry for !command for usage."],
            ["Bot Super Admin", "global", "[...]", "Global regex filters, see the normal entry for !regex for usage. Append f to command for file filters (e.g. add -&gt; addf)"],
            ["Developer", "addmin", "[username] [level]", "Set a user's global access level. -1 = banned from the bot."],
            ["Developer", "deladmin", "[username]", "Unset a user's global access level."],
            ["Developer", "spam", "[count] [message]", "Repeat message count times. See !echo."]
        ];
        
        if (window.location.hash == "#admin") {
            for (var i = 0; i < admin_commands.length; ++i) {
                commands.push(admin_commands[i]);
            }
        }
        
        document.getElementById('commands').innerHTML = generateDomForTable(commands);
        document.getElementById('replacements').innerHTML = generateDomForTable([
            ["[user]", "User, who used the command."],
            ["[alias &lt;command&gt; <span class=\"optional\">&lt;command parameters&gt;</span>]", "Output from another command."],
            ["[countdown &lt;date|time part of RFC3339 date format&gt;]", "Time until desired date or time of day."],
            ["[params]", "Everything the user entered after the command."],
            ["[&lt;number&gt; <span class=\"optional\">&lt;number&gt;</span>]", "Specific parameters, 0-indexed. Quotes can be used to group params."],
            ["[customapi &lt;URL&gt; <span class=\"optional\">&lt;JSONPath&gt; &lt;...&gt;</span>]", "Output from a website. JSONPath supported for extracting variables from JSON APIs. JSONPath only processed if it starts with $, so you can insert normal text in between variables"],
            ["[urlencode &lt;text&gt;]", "URL encodes text for use with customapi"],
            ["[htmldecode &lt;text&gt;]", "Decode HTML-encoded text for use with customapi"],
            ["[equals &lt;first string&gt; &lt;second string&gt; &lt;replacement for true&gt; &lt;replacement for false&gt;]", "Compares first string to the second. If the strings are the same, replacement for true is used, otherwise the replacement for false is used."],
            ["[datediff <span class\"optional\">&lt;date string&gt;</span> &lt;date string&gt;]", "Time difference between two dates. The first date defaults to current time."],
            ["[uptime <span class=\"optional\">&lt;channel name&gt;</span>]", "Time a stream has been live. Convenience replacement for <code>[0|[channel]] uptime: [datediff \"[customapi https://api.twitch.tv/kraken/streams/[urlencode [0|[channel]]] $.stream.created_at]\"|Offline]</code>"],
            ["[time <span class=\"optional\">&lt;timezone&gt;</span>]", "Current time in specified or channel's default timezone."],
            ["[random &lt;option 1&gt; <span class=\"optional\">&lt;option 2&gt; &lt;...&gt;</span>]", "A random option verbatim."],
            ["[league rank|lastgame|currentgame <span class=\"optional\">&lt;region&gt; &lt;summoner name&gt;</span>]", "League of Legends info lookup. Examples below:<br />rank - "],
            ["[channel]", "Current channel name"],
            ["[nuclearthrone &lt;game's stream key&gt;]", "Current run information in Nuclear Throne. Stream key can be found in game settings.<br /><strong>NOT YOUR TWITCH STREAM KEY!</strong>"],
            ["[cute]", "A cute* unicode emoticon. *may vary"]
        ]);
        document.getElementById('access').innerHTML = generateDomForTable([
            [0, "Normal"],
            [20, "Subscriber"],
            [30, "Channel Moderator"],
            [40, "Broadcaster"],
            [50, "Twitch Staff"],
            ["&ge;60", "Bot Admin"],
            ["&ge;100", "Bot Super Admin"]
        ]);
    </script>
    <script src="/analytics.js" async></script>
</body>
</html>
