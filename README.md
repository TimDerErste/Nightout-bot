# Nightout-bot

from discord import Embed

import SECRETS
import STATICS
from commands import cmd_ping

client = discord.Client ()




commands = {

    "ping": cmd_ping,

}


@client.event
@asyncio.coroutine
def on_ready () :
   print("Bot is logged in successfully. Running on servers:\n")
    for s in client.servers:
        print(" - %s (%s)" % (s.name, s.id))
     yield from client.change_presence(game=Game(name="This is just for fun."))


@client.event
@asyncio.coroutine
def on_message(message)
    if message.content.startswith(STATICS.PREFIX) :
        invoke = message.content[len(STATICS.PREFIX):].split(" ")[0]
        args = message.content.split(" ")[1:]
        print("INVOKE: %s\nARGS: %s" % (invoke, args.__str__()[1:-1].replace("'","")))
        if commands.__contains__(invoke):
            commands.get(invoke).ex(args, message, client, invoke)
         else:
             from discord import Color
             yield from client.send_message(message.channel, ambed=Embed(color=Color.red(), description=("The command `%s` is not valid!" % invoke)))



client.run(SECRETS.TOKEN)
