# Simple-Pycord-Cog-User-Install-Command-Example
An example bot of user install slash command + cog. Using Pycord 2.6.1

What can this bot do?
-----------------
1. Use slash command in public server, private server and DM. You don't need to have bot installed in the server to use the command, you can use command everywhere!
2. Using your bot command by App Launcher.
![rec](https://github.com/user-attachments/assets/fdf22832-c2ba-416c-b1c7-1e8436de75f0)


Quickstart
-----------------
1. Download or `git clone` this repository.

2. Run `pip install -r requirements.txt` to install required Python library.

3. Run `python main.py` to start the bot.

Detailed Guide
-----------------
1. To run this bot, first you need to create a bot at [Discord Developer Portal](https://discord.com/developers/applications). I assume you are already very familiar with this step. If you don't know how to do this, go watch some tutorial videos on YouTube.

2. Since we are making a bot that supports *user install commands*, we need to make enable `User Install` option and some other configuration at dev portal, as below image shown.
![img](https://github.com/user-attachments/assets/033a103c-352b-49a0-bbb6-5468d26a6b3b)

3. Now, invite your bot to your test server. Mention the bot, open its profile and click `Add App`.
![img](https://github.com/user-attachments/assets/423bd044-7b2a-4f73-9318-596b1d8a9867)

Click `Add to My Apps`.
![img](https://github.com/user-attachments/assets/1b65dc01-1a27-43c4-b309-d6a5718cc52d)

Click `Authorize`.
![img](https://github.com/user-attachments/assets/2228ff51-bb7d-43ed-ba47-e8d936ed4134)

After you authorized the bot, you will see a nice little pop up at bottom right corner tells you `App Added!`
![img](https://github.com/user-attachments/assets/41acd646-a395-4c5b-85f2-b29f5eaa6e29)

We can now open App Launcher and check our bot. Of course, you won't see any commands because you haven't run the code. You can see the `/ping` command in the image because I ran the code earlier.
![img](https://github.com/user-attachments/assets/8e1dc29a-3fff-4991-a9e5-6ddef5d729c1)

4. Here comes the coding part. I assume you are familiar with these steps too, so I'll keep it simple.
- Download or `git clone` this repository.
- Run `pip install -r requirements.txt` to install required Python library.
- Create a .env file and enter `DISCORD_BOT_TOKEN = 'THE_BOT_TOKEN_YOU_GET_FROM_DISCORD_DEV_PORTAL'`
- Run `python main.py` to start the bot.

5. You can see that `/ping` command works without any problem in servers with/wthout bot installed and in DM :)
![rec](https://github.com/user-attachments/assets/c3c8a81b-dc3a-49ac-9499-4a9a56471e77)


FAQ
-----------------
## I want to create another command, how do I do this?
1. Copy `ping.py` in `cogs` folder and rename it to the name you like.
2. 2. Rename every 'ping' in `ping.py` to the name you like.
3. Open `main.py`, you can see:
```python
    extensions = [
        'cogs.ping',

    ]
```
now add `'cogs.another_command_name',` under `'cogs.ping',`
4. Restart main.py

## What's the difference between user install command and regular guild install command in code?

`ping.py`
```python
class ping(commands.Cog):
    def __init__(self, bot):
        self.bot = bot

    @commands.slash_command(
        name='ping',
        description='Check bot latency',
        integration_types=[
            IntegrationType.user_install, # This line shows that the command is a user install command
            IntegrationType.guild_install,
        ],
        contexts=[
            InteractionContextType.guild,
            InteractionContextType.bot_dm, # This line shows that the command can be used in DM
            InteractionContextType.private_channel, # This line shows that the command can be used in private channel
        ],
    )
```
