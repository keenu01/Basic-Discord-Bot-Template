#imports
import openai
import time
import spacy
import time
import json
from discord import app_commands
import os
import json
import discord
from discord.ext import commands
import datetime 
import random as r
from music_cog import music_cog
import json
from rule34Py import rule34Py
from PIL import Image
from PIL import ImageFont
from PIL import ImageDraw
from io import BytesIO
from time import ctime
from datetime import datetime

"""
Configurations
--------------
The Language,
Name,
Api-Key,
and discord.py variables.
"""
intents = discord.Intents.default()
intents.message_content = True
bot = commands.Bot(command_prefix="!",intents = discord.Intents.all())
language = "en"
#api key setter
name = "Hitori"
api_key = "ENTER-YOUR-OWN-API-KEY"
"""
@Bot.event
-----------
Syncs the Slash Commands.
"""
@bot.event
async def on_ready():
     try:
        sycned = await bot.tree.sync()
        print(f"Sync has been succesfull on the {len(sycned)} commands")
        await bot.change_presence(activity=discord. Activity(type=discord.ActivityType.listening, name='Lofi.'))
        
        
     except Exception as e:
         print(e)

#Lore. Characteristics for Bocchi!-Change Name,Anime Series and adjectives to your own character (if you wish)
lore = "You are Hitori Gotoh aka Bocchi from the Anime Series Bocchi the Rock! .Hitori Gotoh is a Timid ,love strucked and introverted Girl. You must use the same vocabulary,manner and tone as Hitori Gotoh. You are very blunt and say 20 words or less.You lack physical boundaries."

"""
RPS Function
------------
Function used in the RPS Slash Command
"""

                                                                                                                                                                                         
breaker = "========================================================================================"   
slogan = "In Hitori-chan we trust :3"
print(breaker)
                                                                                  
print(slogan)
time.sleep(0.1)
print(breaker)
print("Hitori is online!")
responce = "" 
host = "127.0.0.1"   
port = "50021"
openai.api_key = api_key
nlp = spacy.load("en_core_web_sm")
#chat simplfy|| allows megumin to see complicated sentences in its most basic form >:3
def simplify_text(text):
    doc = nlp(text)
    simplified_text = " ".join([token.lemma_ for token in doc])
    return simplified_text
#defining stuff
active = True
slore = simplify_text(lore)
uzer = ""
cwd = os.getcwd()
files = os.listdir(cwd)
with open("hit.json","r") as clogra:
    x = json.load(clogra)
    x =  x["history"] 
    message =[{"role": "user", "content":uzer},{"role":"system","content":lore}]+x

def write_json(new_data, filename='hit.json'):
    with open(filename,'r+') as file:
          # First we load existing data into a dict.good
        file_data = json.load(file)
        # Join new_data with file_data inside emp_details
        file_data["history"].append(new_data)
        # Sets file's current position at offset.
        file.seek(0)
        # convert back to json.
        json.dump(file_data, file, indent = 4)
resp = ""

def chat_looper(uzer,writer):
    """
    Configuartions
    """
    max_tokens=200
    temperature=0.8
    top_p=1
    frequency_penalty=1
    presence_penalty=2
    


    """
    OPENAI Request
    Writes to a JSON FILE, for history and appends to the message array for conversations
    (ik crazy)
    """
    #the auto complete block (it was pain)
    uzmem = {"role":"user", "content":f"{writer}:{uzer}"}
    
    write_json(uzmem) 
    message.append(uzmem)
    completion = openai.ChatCompletion.create (model="gpt-3.5-turbo-0613" ,messages=message,max_tokens = max_tokens ,temperature = temperature ,top_p=top_p,frequency_penalty=frequency_penalty,presence_penalty=presence_penalty)
    

    responce = completion.choices[0].message.content
    global resp
    resp = responce
    
    megmem = {"role":"assistant", "content":responce}
    write_json(megmem) 
    message.append(megmem)

def rps():
    ROCK = "rock"
    PAPER = "paper"
    SCICORS = "scissors"
    #input
    rang = r.randint(0,2)
    global randomz
    if rang == 0:
            randomz = ROCK
    elif rang == 1:    
        randomz =  PAPER
    else:  
        randomz = SCICORS



"""
The following code are for the slash commands used by the discord bot.
The Code is really not that hard to understand(i think anyway)
have fun understading what poor life decisions i made while thinking of ideas..
-Keenu.
Notes:These are SLASH COMMANDS...(I like them cuz they are foncy)
"""


#offsets
@bot.tree.command(name="off_set")
@app_commands.describe(off_setx="put x offset for images")
@app_commands.describe(off_sety="offset for y")
async def setter(interaction:discord.Interaction,off_setx:int,off_sety:int):
    global ofsx 
    ofsx = off_setx
    global ofsy 
    ofsy = off_sety
    await interaction.response.send_message(f"Succesfully Off-Set Change!")

#offset testing.
@bot.tree.command(name="grave_stone",description="A grave_stone with u on it!")
@app_commands.describe(tag="Put a users tag in")
async def img(interaction:discord.Interaction,tag:discord.Member,):
    lofi = Image.open("tomb_stone.jpeg")
    asset= tag.avatarcc34
    data = BytesIO(await asset.read())
    pfp = Image.open(data)
    pfp = pfp.resize((177,177))
    lofi.paste(pfp,(ofsy,ofsy))
    lofi.save("nstone.jpg")
    await interaction.response.send_message(file=discord.File("nstone.jpg"))


#THE BOCH CARD!?-Makes a relaxing looking user card to look at 
@bot.tree.command(name="boch_card",description="A bocchi card with u on it!")
@app_commands.describe(tag="Put a users tag in")
async def img(interaction:discord.Interaction,tag:discord.Member):
    lofi = Image.open("bochi_card.png")
    draw = ImageDraw.Draw(lofi)
    font = ImageFont.truetype("junegull rg.otf",70)
    font2=ImageFont.truetype("junegull rg.otf",20)
    draw.text((250,100),f'{tag.display_name}',(255,255,255),font=font)
    asset= tag.avatar
    data = BytesIO(await asset.read())
    pfp = Image.open(data)
    # draw.text((x, y),"Sample Text",(r,g,b))
    draw.text((250,50),f"{[y.name.lower() for y in tag.roles]}",(255,255,255),font=font2)
    pfp = pfp.resize((210,210))
    lofi.paste(pfp,(0,0))
    lofi.save("lofa.png")
    file = discord.File("lofa.png")
    embed=discord.Embed(title="**Succesfully Generated Your Card**")
    
    await interaction.response.send_message(f"Succesfully Made!({tag})",file=discord.File("lofa.png"))



#rr34 Command-Makes.. images.. for the wrong people..(its weird ik i was tired)
@bot.tree.command(name="rr34",description="Get a random image from the R34 Website..")
@app_commands.describe(tag="put in a tag!")
async def rmond(interaction:discord.Interaction,tag:str):
    await interaction.response.defer()
    print(f"NERD ALERT!!! {interaction.user.display_name} WANTED TO SEE {tag} PORN!")
    try:
        r34 = rule34Py()
        new = r34.search([tag],page_id=2, limit=60)
        new = r.choice(new)
        check = new.content_type
        if check == "video":
          await interaction.followup.send(f"``Tags:{tag}\nURL:{new.video}\n|| ID:{new.id}``\n{new.video}")
        else:
          await interaction.followup.send(f"``Tags:{tag}\nURL:{new.image}\n|| ID:{new.id}``\n{new.image}")
    except:
        await interaction.followup.send("There is nothing in this field :pensive:")
    print("Succesfull..")

#Views the chat-log of everybody who uses the BOT!!
@bot.tree.command(name="see_clog",description="See the chat_log hayori had read!")
async def read(interaction:discord.Interaction):
    global x
    mzg = []
    c=0
    for i in x:
        if c!= 1800:
            mzg.append(i)
            c += 1
        else:
            pass
    await interaction.response.send_message(mzg)

#Main Chat Command!-lets me chat 
@bot.tree.command(name="chat", description="Talk to Hayori!")
@app_commands.describe(messages = "Talk to Me!")
#async def konata(ctx,*,message):
async def chat(interaction: discord.Interaction, messages: str):
    await interaction.response.defer()
    author = interaction.user.display_name
    try:
        chat_looper(messages,author)
        print(f"{author} said:{messages}")
        print("Hayori is answering..")
        embed = discord.Embed(title="Bocchi!",description=resp,colour=discord.Color.from_rgb(255,202,229))
        embed.set_footer(text=f"This message was said on the {ctime()}")
        await interaction.followup.send(embed=embed)
        print(f"Hayori has answered:{resp}")
    except:
        await interaction.followup.send("An error has occured...:pensive:")


#Info Command!-Displays the Bot's Info!!(wow so cool ik used embeds to do it im so proud it looks so proud!!! anyway)
@bot.tree.command(name="info",description="Information about me :fire:")
async def info(interaction:discord.Interaction):
    await interaction.response.defer()
    emebed = discord.Embed(title="Info",description=":heart: developed by @keenu",colour=discord.Color.from_rgb(255,202,229))
    emebed.add_field(name="General Commands",value=" /chat- Chat to Hayori!\n/dice- Roles a Dice!\n/rps- Play rock paper scicors with hayori!\n/setup_music- Sets up the music cog!")
    emebed.add_field(name="Music Commands",value="!play- Plays music and adds to the queue(Be in a VC first!)\n!pause- Pauses the music\n!skip- Skips to the next song in the queue\n!clear- Clears all songs in the queue :fire:\n!stop- Makes the bot leave the vc\n!remove- Removes the last song from the queue(helps when hayori kills her self)")
    emebed.add_field(name="NSFW CMDS",value="/rr34-Random R34 image from tags\n")
    await interaction.followup.send(embed=emebed)

#Dice command!-it rollz dice so sigma
@bot.tree.command(name="dice",description="Rolls a dice!")
async def roller(interaction:discord.Interaction):
     x = r.randint(1,6)
     await interaction.response.send_message(f"**You have rolled**:*{x}*")


#Sets up music cog cmds are displayed when activated
@bot.tree.command(name="setup_music",description="Set up da music")
async def setup(interaction : discord.Interaction):
    try:
            await interaction.response.defer()
            await bot.add_cog(music_cog(bot))
            print(f"{interaction.user.display_name},has set up the music cog!")
            embedz = discord.Embed(title="**Music has been Set Up!**",colour=discord.Color.from_rgb(255,202,229))
            embedz.add_field(name='Commands',value='!play-Plays Music\n!pause-Pauses Music\n!stop-Hayori Disconnects.\n!skip-Skip music in the queue\n!clear-Clear the queue.')
            await interaction.followup.send(embed=embedz)
    except:
            await interaction.followup.send("Well... I think somebody has already set it up...")


#RPS Command!-Play rock paper scicors/.
@bot.tree.command(name="rps",description="Play Rock Paper Scicors!")
@app_commands.describe(pick="Pick an item!")
async def check(interaction: discord.Interaction,pick:str):
        rps()
        print(f"{interaction.user.display_name} is playing RPS with hayori: {randomz} and {pick} was chosen(randomz and pick)")
        if randomz == "rock" and pick == "paper":
            await interaction.response.send_message(f"I have picked **{randomz}**\n You picked **{pick}**\n... **Hayori Loses..!:pensive:**")

        elif randomz == "paper" and pick == "rock":
            await interaction.response.send_message(f"I have picked **{randomz}**\n You picked **{pick}**\n...**Hayori WINS!**:fire:")

        elif randomz == "rock" and pick == "scicors":
            await interaction.response.send_message(f"I have picked **{randomz}**\n You picked **{pick}**\n... **Hayori Loses..**:sob:")

        elif randomz == "scicors" and pick == "paper":
            await interaction.response.send_message(f"I have picked **{randomz}**\n You picked **{pick}**\n...**Hayori WIN!**:smiling_imp:")

        elif randomz == "scicors" and pick == "rock":
            await interaction.response.send_message(f"I have picked **{randomz}**\n You picked **{pick}**\n...**Hayori Loses..**:pensive:")

        elif randomz == pick:
            await interaction.response.send_message(f"WE DREW :sob: \n(I picked {randomz},You picked**{pick}**)")

        elif randomz == "paper" and pick == "scicors":
            await interaction.response.send_message(f"I have picked **{randomz}**\n ,You picked **{pick}**\n...**I Lose**:rage:")

        else:
            await interaction.response.send_message("Blud what did you even type in :skull: (You might have misspelt)")  
guild = ''
#guild id linker-litteraly does nothing
@bot.tree.command(name="guild_id",description='give the bot the discord guild id(does not do anything lol)')
@app_commands.describe(id="Your ID")
async def get_channels(interaction:discord.Interaction,id : str):
    try:
        global guild
        guild = await bot.fetch_guild(id)
        embed= discord.Embed(title="Guild ID",description="Guild ID stored!!",colour=discord.Color.from_rgb(255,202,229))
        await interaction.response.send_message(embed=embed)
    except:
        await interaction.response.send_message("I do not have access to that guild or it doesn't exist.")
#Guild_ID displayer!-Dispaly the Id of the Guild
@bot.tree.command(name="display_guild_id",description="displays guild id!!")
async def display_guild_id(interaction:discord.Interaction):
    embedr = discord.Embed(title=" ",colour=discord.Color.from_rgb(255,202,229))
    embedr.add_field(name='Guild ID',value= f"Your Guild ID is, **{interaction.guild_id}**")
    embedr.set_footer(text=f"Succesfuly given Guild ID!")
    await interaction.response.send_message(embed=embedr)

p_count = 0

@bot.tree.command(name="serverinfo",description="see the stats of this server!!")
async def serverinfo(interaction:discord.Interaction):
    total_count=0
    for guild in bot.guilds:
        for member in guild.members:
            total_count = total_count + 1
    creation_date = interaction.guild.created_at
    today = datetime.date.today()
    embed = discord.Embed(title="**Server Stats**:",colour=discord.Color.from_rgb(255,202,229))
    embed.set_author(name=f"**{interaction.guild.name}**")
    embed.set_thumbnail(url=interaction.guild.icon)
    embed.add_field(name="Owner",value= interaction.guild.owner, inline = False)
    embed.add_field(name="Current Population:",value=f"The population of the server is, **{interaction.guild.member_count}**")
    embed.add_field(name="Boosts",value=f"This server has **{interaction.guild.premium_subscription_count}** Boosters!!({interaction.guild.premium_subscribers})",inline=False)
    embed.add_field(name="Channels",value=f"Text Channels:{len(interaction.guild.text_channels)}\n Voice Channels:{len(interaction.guild.voice_channels)}",inline=False)
    embed.add_field(name="Roles",value=f" Total Roles:{len(interaction.guild.roles)}\nRole list:{[str(r.name) for r in interaction.guild.roles]}")
    embed.set_footer(text=f"Created on the {creation_date},||ID: {interaction.guild_id}||")
    print(f"Hayori has just sent an embedding to the server:{interaction.guild.name},||ID: {interaction.guild_id}||")
    await interaction.response.send_message(embed=embed)

#Exactly how it sounds...
@bot.tree.command(name="i_came",description="get the top 100 'came on characters':vomit:")
async def i_came(interaction: discord.Interaction):
    r34 = rule34Py()
    icame = r34.icame()
    icamez = []
    for i in icame:
        x =icamez.append(i)
    await interaction.response.send_message(f"Characters:{x}")


#Displays an invite_code for the Bot!
@bot.tree.command(name="invite_code",description="invite me to your server!")
async def random(interaction:discord.Interaction):
    await interaction.response.defer()
    embed = discord.Embed(title="Invite Link!")
    embed.add_field(name="Link:",value="REPLACE-WITH-YOUR-OWN-BOT-INVITE-LINK")
    
    await interaction.followup.send(embed = embed)



      
#Cflip is real(coin goes boing)
@bot.tree.command(name="cflip",description="coin flip!")
@app_commands.describe(side="pick a side (heads or tails)")
async def flip(interaction:discord.Interaction,side :str):
    side = side.lower() 
    coin = r.randint(0,100)
    if coin > 50:
        end = "tails"
    else:
        end = "heads"
    if side == end:        
        await interaction.response.send_message(f"You Win!(It was {side})")
    else:
        await interaction.response.send_message(f"You lost..(It was {side})")

#Makes hayori say stuff (it can be racist!!)
@bot.tree.command(name="force_say",description="Make me say something!")
@app_commands.describe(query="write smth idk nothing racist plz")
async def said(interaction:discord.Interaction,query:str):
    await interaction.response.send_message(query)



bot.run("Enter your own discord bot token here")
