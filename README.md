# space bot list api wrapper for node.js

[Bot List Link](https://www.spacebotlist.xyz/)


*Installation*

`npm install spacebotlist.js --save`

<hr>

**Posting Servers Count & Shards Count** `POST`

`You can post once every 5 minutes (ratelimits)`

<hr>

**Response**

[ Error ] 429 : `[SBL] (429): Your are being ratelimited, 1 request per 5 mins.`

[ Error ] 404 : `[SBL] (404): Can't find server_count.`

[ Error ] 404 : `[SBL] (404): Authorization header not found.`

[ Error ] 400 : `[SBL] (400): server_count not integer.`

[ Error ] 404 : `[SBL] (404): Bot not found!`

[ Error ] 400 : `[SBL] (400): Incorrect authorization token.`

[ Error ] 404 : `[SBL] (404): Go generate auth token for your bot!`

[ Error ] 400 : `[SBL] (400): shard_count not integer.`


[ Success ] 200 : **[200]: Your Stats Has Been Posted.**

```js
const Discord = require("discord.js")
const client = new Discord.Client()
const prefix = "!";
const SBL = require("spacebotlist.js")
const sbl = new SBL.get(client.user.id,"bot-auth-token")

client.on("ready", () => {
console.log(`Logged in as ${client.user.tag}.`)
setInterval(() => {
    sbl.post(client.guilds.cache.size)
    //sbl.post(client.guilds.cache.size, client.shard.count)
    //to post shard count!
})

client.on("message", message => {
    if(message.author.bot) return
    if(message.content == prefix + "ping"){
        message.reply(`Pong! it took ${client.ws.ping}`)
    }
})

client.login("token")

```
