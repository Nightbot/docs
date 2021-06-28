/*
Title: Eval
*/

The Eval variable is used to evaluate JavaScript code. The timeout length of the script execution is 1 second. 

## Usage

> $(eval `javascript`)

#### Example Usage

> $(eval 2 + 2)

would result in

> 4

### Example Usage

> $(eval for(;;){}) `(infinite loop)`

would result in

> Script execution timed out.

## A warning about command input

Variables substituted inside of the Eval variable are treated as raw JavaScript. 
Because of this, extra care should be taken when using variables inside of Eval.

> !addcom !upper $(eval "@$(user), " + "$(query)".toUpperCase())

At first glance, this command works as expected:

> User: !upper lulw
Nightbot: @User, LULW

However, a malicious user could use this command in combination with Nightbot's moderator level privileges to perform unintended actions.
This can be especially risky when Nightbot is used in combination with other twitch bots.

> User: !upper ";"!settitle Last stream ever!"//

> Nightbot: !settitle Last stream ever!

> OtherBot: @Nightbot, the title has been updated to "Last stream ever!"

In order to avoid this, make use of the [QueryString](https://docs.nightbot.tv/variables/querystring) variable and JavaScript's [decodeURIComponent](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/decodeURIComponent):

> !addcom !upper $(eval "@$(user), " + decodeURIComponent("$(querystring)").toUpperCase())

Or, if substituting a different variable, such as an [argument](https://docs.nightbot.tv/variables/arguments):

> !addcom !upper $(eval "@$(user), " + decodeURIComponent("$(querystring $(3))").toUpperCase())

## Examples

#### Generate a random number between 1 to 100

> !commands add !random The Random Number is: $(eval Math.floor((Math.random() * 100) + 1))

#### Make an 8ball command

> !commands add !8ball 🎱 $(eval const responses = ['All signs point to yes...', 'Yes!', 'My sources say nope.', 'You may rely on it.', 'Concentrate and ask again...', 'Outlook not so good...', 'It is decidedly so!', 'Better not tell you.', 'Very doubtful.', 'Yes - Definitely!', 'It is certain!', 'Most likely.', 'Ask again later.', 'No!', 'Outlook good.', 'Don\\'t count on it.']; responses[Math.floor(Math.random() * responses.length)];)
