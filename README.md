const Eris = require('eris');
var bot = new Eris("NTY1MzU4ODg4NDAxMjQwMDc0.XK6iUQ.8cg0KTHsnZurgN-TbsZXPkKGD9Q")
var prefix = ":"


bot.on("ready", () => {
    console.log("Ready!");
        bot.editStatus("online", {name: "with the members! | type :help"}); 
     });
     bot.on("messageCreate", (msg) => {
        if(msg.content === prefix + "ping") {
            console.log(msg.author.username + "#" + msg.author.discriminator, "| User ID:" + msg.author.id, "| Command: " + msg.content + " | Guild:", msg.channel.guild.name, "| ID:", msg.channel.guild.id, "| Channel ID:", msg.channel.id);
            let start = Date.now(); bot.createMessage(msg.channel.id, ':ping_pong: **Grabbing the ping-pong paddle...**').then(msg => { let diff = (Date.now() - start); return msg.edit(`:ping_pong: **Pong! Bot Latency:** \`${diff}ms\``); });
        }
    });
    bot.on("messageCreate", (msg) => { //=LCYM
        if(msg.content === prefix + "help") {
            console.log(msg.author.username + "#" + msg.author.discriminator, "| User ID:" + msg.author.id, "| Command: " + msg.content + " | Guild:", msg.channel.guild.name, "| ID:", msg.channel.guild.id, "| Channel ID:", msg.channel.id);
            bot.createMessage(msg.channel.id, ":mailbox: *You've received a DM!*")
            bot.getDMChannel(msg.author.id).then(channel => {
            bot.createMessage(channel.id, {
                embed: {
                    color: 0x8cd9ff,
                    fields: [
                        {
                            name: ":wave: Commands",
                            value: "`=ping` ~~--~~ *Shows the bot's latency*\n`=kick` `userid` `reason(optional)` ~~--~~ *Kicks a user from the server*\n`=ban` `userid` `reason(optional)` ~~--~~ *Permanently bans a user.*\n`=unban` `userid` `reason(optional)`",
                            inline: true
                        },
                    ],
                    footer: {
                    }
                }
            });
            });
        }
    });
     bot.on("messageCreate", msg => {
        if(msg.channel.guild.members.get(bot.user.id).permission.has("kickMembers") == false){    
        let args = msg.content.split(/ +/);
        let command = args.shift();
        const msgContent = msg.content.toString().toLowerCase();     
        if(command.toLowerCase() === prefix+"kick") {
         const toSay = args.join(" ");
         bot.createMessage(msg.channel.id, "I am missing the `Kick Members` permission!");
            }
        }
    });
    bot.on("messageCreate", msg => {
        if(msg.channel.guild.members.get(msg.author.id).permission.has("kickMembers") == false){    
        let args = msg.content.split(/ +/);
        let command = args.shift();
        const msgContent = msg.content.toString().toLowerCase();     
        if(command.toLowerCase() === prefix+"kick") {
         const toSay = args.join(" ");
         bot.createMessage(msg.channel.id, "You are missing the `Kick Members` permission!");
            }
        }
    });
    bot.on("messageCreate", msg => {
        if(msg.channel.guild.members.get(msg.author.id).permission.has("kickMembers") == true){    
            if(msg.channel.guild.members.get(bot.user.id).permission.has("kickMembers") == true){    
            if(!msg.content.startsWith(prefix) || msg.author.bot) return;
        let args = msg.content.split(/ +/);
        let command = args.shift();
        const msgContent = msg.content.toString().toLowerCase();     
        if(command.toLowerCase() === prefix+"kick") {
         const toSay = args.join(" ");
         let thatUser = args[0]         
         let theReason = toSay.slice(thatUser.length)
         bot.getDMChannel(thatUser).then(channel => {
            bot.createMessage(channel.id, ":boot: **You've been `kicked` from " + msg.channel.guild.name + " for:**" + theReason);
         bot.kickGuildMember(msg.channel.guild.id, thatUser, theReason)
         bot.createMessage(msg.channel.id, ":boot: I have kicked <@" + thatUser + ">!");    
                });
            }
        }
    }
    });
    bot.on("messageCreate", msg => {
        if(msg.channel.guild.members.get(bot.user.id).permission.has("banMembers") == false){    
        let args = msg.content.split(/ +/);
        let command = args.shift();
        const msgContent = msg.content.toString().toLowerCase();     
        if(command.toLowerCase() === prefix+"ban") {
         const toSay = args.join(" ");
         bot.createMessage(msg.channel.id, "I am missing the `Ban/Unban Members` permission!");
            }
        }
    });
    bot.on("messageCreate", msg => {
        if(msg.channel.guild.members.get(msg.author.id).permission.has("banMembers") == false){    
        let args = msg.content.split(/ +/);
        let command = args.shift();
        const msgContent = msg.content.toString().toLowerCase();     
        if(command.toLowerCase() === prefix+"ban") {
         const toSay = args.join(" ");
         bot.createMessage(msg.channel.id, "You are missing the `Ban/Unban Members` permission!");
            }
        }
    });
    bot.on("messageCreate", msg => {
        if(msg.channel.guild.members.get(msg.author.id).permission.has("banMembers") == true){    
            if(msg.channel.guild.members.get(bot.user.id).permission.has("banMembers") == true){    
            if(!msg.content.startsWith(prefix) || msg.author.bot) return;
        let args = msg.content.split(/ +/);
        let command = args.shift();
        const msgContent = msg.content.toString().toLowerCase();     
        if(command.toLowerCase() === prefix+"ban") {
         const toSay = args.join(" ");
         let thatUser = args[0]
         let theReason = toSay.slice(thatUser.length)
         bot.getDMChannel(thatUser).then(channel => {
            bot.createMessage(channel.id, ":hammer: **You've been `banned` from " + msg.channel.guild.name + " for:**" + theReason);
         bot.banGuildMember(msg.channel.guild.id, thatUser, 7,  theReason)
         bot.createMessage(msg.channel.id, ":hammer: I have banned <@" + thatUser + ">!");      
                });
            }
        }
    }
});
    bot.on("messageCreate", msg => {
        if(msg.channel.guild.members.get(bot.user.id).permission.has("banMembers") == false){    
        let args = msg.content.split(/ +/);
        let command = args.shift();
        const msgContent = msg.content.toString().toLowerCase();     
        if(command.toLowerCase() === prefix+"unban") {
         const toSay = args.join(" ");
         bot.createMessage(msg.channel.id, "I am missing the `Ban/Unban Members` permission!");
            }
        }
    });
    bot.on("messageCreate", msg => {
        if(msg.channel.guild.members.get(msg.author.id).permission.has("banMembers") == false){    
        let args = msg.content.split(/ +/);
        let command = args.shift();
        const msgContent = msg.content.toString().toLowerCase();     
        if(command.toLowerCase() === prefix+"unban") {
         const toSay = args.join(" ");
         bot.createMessage(msg.channel.id, "You are missing the `Ban/Unban Members` permission!");
            }
        }
    });
    bot.on("messageCreate", msg => {
        if(msg.channel.guild.members.get(msg.author.id).permission.has("banMembers") == true){    
            if(msg.channel.guild.members.get(bot.user.id).permission.has("banMembers") == true){    
            if(!msg.content.startsWith(prefix) || msg.author.bot) return;
        let args = msg.content.split(/ +/);
        let command = args.shift();
        const msgContent = msg.content.toString().toLowerCase();     
        if(command.toLowerCase() === prefix+"unban") {
            const toSay = args.join(" ");
            let thatUser = args[0]
            let theReason = toSay.slice(thatUser.length)
         bot.unbanGuildMember(msg.channel.guild.id, thatUser, theReason)
         bot.createMessage(msg.channel.id, ":wave: I have unbanned that user!");      
            }
        }
    }
    });
    bot.on("messageCreate", (msg) => {
        if(msg.content === prefix + "ban") {
            console.log(msg.author.username + "#" + msg.author.discriminator, "| User ID:" + msg.author.id, "| Command: " + msg.content + " | Guild:", msg.channel.guild.name, "| ID:", msg.channel.guild.id, "| Channel ID:", msg.channel.id);
            bot.createMessage(msg.channel.id, "*" + msg.author.mention + " you need to provide a user id to ban someone\n`=ban userid reason(optional)`*")
        }
    });
    bot.on("messageCreate", (msg) => {
        if(msg.content === prefix + "kick") {
            console.log(msg.author.username + "#" + msg.author.discriminator, "| User ID:" + msg.author.id, "| Command: " + msg.content + " | Guild:", msg.channel.guild.name, "| ID:", msg.channel.guild.id, "| Channel ID:", msg.channel.id);
            bot.createMessage(msg.channel.id, "*" + msg.author.mention + " you need to provide a user id to kick someone\n`=kick userid reason(optional)`*")
        }
    });
    bot.on("messageCreate", (msg) => {
        if(msg.content === prefix + "unban") {
            console.log(msg.author.username + "#" + msg.author.discriminator, "| User ID:" + msg.author.id, "| Command: " + msg.content + " | Guild:", msg.channel.guild.name, "| ID:", msg.channel.guild.id, "| Channel ID:", msg.channel.id);
            bot.createMessage(msg.channel.id, "*" + msg.author.mention + " you need to provide a user id to unban somoene\n`=unban userid reason(optional)`*")
        }
    });

//Note: These are developmental commands meaning they have specific requirements that must be filled to function correctly
//Commands developed by Skyfenfury#7477

bot.connect();
