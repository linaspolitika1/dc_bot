import discord
import datetime
from var import *
from datetime import timedelta
from googletrans import Translator

TOKEN = "OTY1NTUwOTc0NzAzOTIzMjQw.Gy5tH0.QYbpciMirdle69tnfRH_4EYVP79UIUISRRdzhU"
client = discord.Client()

dict = {
    "1": "Combat Pistol",
    "2": "Tazer",
    "3": "Machine Pistol",
    "4": "Assault Rifle",
    "5": "SMG",
    "6": "Assault SMG",
    "7": "Micro SMG",
    "8": "MG",
    "9": "Revolver",
    "10": "Double Action Revolver",
    "11": "Sawed-Off Shotgun",
    "12": "Special Carabine Rifle",
    "13": "Combat MG",
    "14": "Carabine Rifle",
    "15": "7250(Varpinė)",
    "16": "8026(Tunelis prie statybų aikštelės)",
    "17": "8198(Senas koksas)",
    "18": "8818(Siuvykla)",
    "19": "7310(Tunelys prie Casio)",
    "20": "9006(Arena)",
    "21": "9000(Laužynas)",
    "22": "9023(Netoli išardymo)",
    "23": "10100(Vežliukai)",
    "24": "10112(Bunkeris)",
    "25": "(Karinis laivas)",
    "26": "3009(Senas acetonas)",
    "27": "(Urvas prie archeologinių)",
    "28": "(Urvas netoli kasyklų)",
    "29": "(HumanLabs - Po vandeniu)"
}


@client.event
async def on_ready():
    print("We have logged in as {0.user}".format(client))


@client.event
async def on_message(message):
    username = str(message.author).split("#")[0]
    user_message = str(message.content)
    channel = str(message.channel.name)
    data_ir_laikas = datetime.datetime.now()
    print(f'{data_ir_laikas.strftime("%x %X")}:{username}: {user_message}: ({channel})')

    if message.author == client.user:
        return

    if message.channel.name == "ginklai":

        for x in list(user_message.lower().split(",")):
            a = user_message.split(",")
            sarasas = []

            for c in a:
                if x == a[0]:
                    sarasas.append(c.replace(c, dict[c]))

                if x == a[1]:
                    sarasas.append(c.replace(c, dict[c]))

            if x == "1" or "2" or "5" or "6":
                ginklo_laikas = data_ir_laikas + timedelta(hours=2)
                await message.channel.purge(limit=1)
                await message.channel.send(
                    f'{sarasas[0]} bus paruostas naudojimui {sarasas[1]} - ({ginklo_laikas.strftime("%X")})')

            elif x == "7" or "11":
                ginklo_laikas = data_ir_laikas + timedelta(hours=2.5)
                await message.channel.purge(limit=1)
                await message.channel.send(
                    f'{sarasas[0]} bus paruostas naudojimui {sarasas[1]} - ({ginklo_laikas.strftime("%X")})')

            elif x == "4" or "9":
                ginklo_laikas = data_ir_laikas + timedelta(hours=3)
                await message.channel.purge(limit=1)
                await message.channel.send(
                    f'{sarasas[0]} bus paruostas naudojimui {sarasas[1]} - ({ginklo_laikas.strftime("%X")})')

            elif x == "3" or "10":
                ginklo_laikas = data_ir_laikas + timedelta(hours=4)
                await message.channel.purge(limit=1)
                await message.channel.send(
                    f'{sarasas[0]} bus paruostas naudojimui {sarasas[1]} - ({ginklo_laikas.strftime("%X")})')
            return

    if message.channel.name == "turgus":
        if user_message.lower().startswith("perku" or "parduodu" or "free") == False:
            await message.channel.purge(limit=1)
            await message.channel.send(f'{username}, turite sakinio pradzioi rasyti (perku, parduodu, free)')

    if message.channel.name == "vertejas":
        if user_message == user_message:
            trans = Translator()
            out = trans.translate(user_message, dest="en")
            await message.channel.send(out.text)

client.run(TOKEN)
