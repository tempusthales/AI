<p><h1 align="center">ChatGPT, iOS and Shortcuts walked into a bar</h1>
  <h3 align="center">or how to replicate Tony Stark's Jarvis</h3>
</p>
<br>


<p align="center">
  
  <a href="/j4rv1s/home_assistant/documentation/automations_list_v2.md"><img src="https://img.shields.io/badge/Automations%20List-purple" alt="A part of me lives here"></a>
  <a href="/j4rv1s/home_assistant/documentation/hardware.md"><img src="https://img.shields.io/badge/Hardware%20Specifications-purple" alt="This is what runs everything"></a> 
  <a href="/j4rv1s/home_assistant/documentation/zigbee.md"><img src="https://img.shields.io/badge/Zigbee%20Devices-green" alt="This is what runs everything"><img src="https://img.shields.io/badge/Lovelace%20Interfaces-orange" alt="Actually my .storage folder, but eh!"></a>
  <a href="/j4rv1s/home_assistant/documentation/indoor_localization.md"><img src="https://img.shields.io/badge/Indoor%20Localization-blue" alt="They know where you are..."></a> 
  <a href="/j4rv1s/home_assistant/documentation/software.md"><img src="https://img.shields.io/badge/Software%20Usage-cyan" alt="Some deets on the softs"></a> <a href="/documentation/wifi.md"><img src="https://img.shields.io/badge/Networking-violet" alt="Some deets on the network"></a> <a href="/documentation/general_thoughts.md"><img src="https://img.shields.io/badge/My Thoughts-red" alt="Some thoughts"></a> <br></p>



ChatGPT, iOS and Shortcuts walked into a bar — How to build Jarvis with HomeKit Voice Assistant

Ever since I started using ChatGPT and GPT-3, every other “smart” assistant—Siri, Alexa, Google Home—feels like they’re running on dial-up while I’m cruising on fiber optics. It’s like comparing a TI-83 calculator to a quantum computer.

And here’s the plot twist worthy of a sci-fi novel: you can build your own GPT-powered assistant in less time than it takes for Google Home to “search the web” for something it clearly didn’t understand. Mind = blown.


### Background
I’ve got a fully tricked-out HomeKit smart home—dozens of lights, thermostats, underfloor heating, ventilation units, cameras, and more. Basically, it’s a tech lover’s paradise. But here’s the kicker: I thought, “Wouldn’t it be awesome if I could replace Siri with GPT-3?” Because let’s face it, Siri tries her best, but she’s like a C student in a class full of valedictorians.

Here’s why GPT-3 (and especially ChatGPT) feels like the upgrade my smart home deserves: these language models are trained on conversational data, making them freakishly good at understanding and responding to human instructions. No more yelling the same command five times, only to have Siri misinterpret it as “Call Mom” (sorry, Mom).

If you’ve tried any of these chatbots, you already know how they make interacting with tech feel more like talking to a really smart (and slightly nerdy) friend. The challenge, though, is that smart homes aren’t like general conversations. You’ve got super-specific devices to control, each with its own quirks and commands. So, how do you bridge that gap?

Well, here’s the exact prompt I used to pull this off:

(Image 1)

As you can see, I kept it super simple—just explained everything in plain English. I laid out the kinds of requests I’d be making, the exact structure I wanted for the responses, and even asked GPT-3 to play the part of a sentient AI (because who doesn’t want their smart home assistant to have some personality?). Bonus points: I even asked it to handle personal questions, like giving me life advice when I’m stuck on whether to order pizza or sushi. Priorities, right?

I also threw in a few extra details, like the time, location, and a full rundown of the devices and rooms in my house. From just that, GPT-3 churns out perfectly structured, human-like responses every single time. No fuss, no code.

And that’s all it takes to program it! No PhD in computer science required—just a good prompt and a little imagination.

:: Command action

When GPT-3 detects that you’re trying to control some part of the smart home, it switches gears and responds with an action category labeled as “command.” Super smart, right?

Here’s an example of how it works in action:

####Request:
"Just noticed that I’m recording this video in the dark in the office. Can you do something about that?"

####Response:
```
{
  "action": "command",
  "location": "office",
  "target": "light",
  "value": "on",
  "comment": "Turning the light on for you.",
  "scheduleTimeStamp": ""
}
```
Boom—GPT-3 doesn’t just turn on the lights, it knows exactly what you’re aiming for: better lighting for recording. It’s like having an AI assistant that actually gets you, rather than making you spell out every little detail.

And the best part? It even includes context in the response, which means it’s not just blindly following orders—it’s thinking ahead, so you don’t have to.

Honestly, when I saw this response, I almost fell out of my chair. It worked so well, I had to double-check that I wasn’t secretly living in a sci-fi movie.

Here’s the thing: my request wasn’t your standard, robotic, “Switch the lights on in the office.” Nope, I phrased it in the most convoluted, roundabout way possible—something that would’ve sent Siri, Alexa, or Google Home into a full-on existential crisis. And yet, GPT-3 didn’t even blink. It got it. Perfectly.

What’s even cooler? The comment in the response is always unique and tailored to your exact request. It’s like GPT-3 is trying to flex its conversational charm while still getting the job done.

With this response, we know exactly what needs to happen next, and we’ll handle the action later using a Siri Shortcut.

Oh, and did you notice the scheduleTimeStamp in the response? If it’s empty, that means the action should happen immediately. But GPT-3 is clever enough to populate it with a future timestamp if your command is time-sensitive.

For example, take this request:
“I sent my son to bed to read for another 20 minutes. Can you switch off the lights in his room when it’s time to sleep?”

GPT-3 absolutely nailed it. It understood that the “bedroom” was the room in question and added a scheduleTimeStamp for 20 minutes from the current time. Here’s what that response might look like:

```
{
  "action": "command",
  "location": "bedroom",
  "target": "light",
  "value": "off",
  "comment": "Switching the lights off in your son's bedroom.",
  "scheduleTimeStamp": "Mon Jan 16 2023 12:16:31 GMT+0000"
}
```

And just like that, you’ve got a smart assistant that doesn’t just follow orders—it understands the context and timing behind them. It’s like having a butler who reads between the lines!


Another fun example of GPT-3’s brilliance is how it made a decision for me about the bedroom temperature:

Request:
"I’m going to trust you with this one! Set the bedroom to a temperature you think would help me sleep better."

Response:

```
{
"action": "command",
"device": "thermostat",
"location": "bedroom",
"command": "set temperature",
"value": "66",
"context": "optimize temperature for better sleep"
}
```
It decided on a cozy 19°C based on its vast knowledge of ideal sleeping conditions. Honestly, it’s like having a super-smart roommate who reads sleep studies for fun.

####Query Action
When GPT-3 detects you’re trying to read the state of a smart home device rather than controlling it, it switches to an action category called "query".

Here’s an example:

Request:
"I just finished cooking a nice big meal in the kitchen. Can you check what’s the temperature there?"

Response:

```
{
  "action" : "query",
  "location" : "kitchen",
  "target" : "thermostat",
  "property" : "temperature"
}
```
It doesn’t just give you a number—it includes context so you can make sense of the response right away. This makes the interaction feel intuitive and personal, something Siri, Alexa, or Google Home can only dream of doing.

Perfect! The action type changed to a query so we can go ahead and fetch the temperature of the kitchen thermostate. Again, we will do this later in the Siri Shortcut.

####Answer Action
When GPT-3 figures out that your request has absolutely nothing to do with your smart home—like when you’re just asking it for general advice or information—it switches to an action category labeled "answer." Think of it as GPT-3 slipping out of its smart-home-operator hat and putting on its all-knowing-guide cap.

Example Request:
"We are going to head out for a short walk into the town center.
Can you recommend a few things to see?"

Response:

{
  "action": "answer",
  "answer": "Austin, TX, offers a fantastic mix of history and modern attractions. The Texas State Capitol is a must-see with its stunning architecture and rich history. Zilker Park is another popular destination, perfect for exploring with its beautiful gardens and the iconic Barton Springs Pool. For a taste of Austin's vibrant culture, visit the Bullock Texas State History Museum or catch a live performance at the Moody Center."
}

Here’s the cool part: because I included the location of the smart home in the request—Austin, Texas—GPT-3 already knows exactly what to recommend! It pulls out relevant, local suggestions like a travel guide that’s lived there its whole life.

This makes it feel less like a faceless AI and more like a friendly local who always has the perfect answer ready. And the response? It’s personalized, engaging, and loaded with practical advice, not just some generic “top 10 tourist attractions” list you could find on a search engine.

####Clarify Action
If GPT-3 isn’t quite sure what you’re asking—maybe your request was too vague or didn’t fit neatly into one of the three actions (command, query, or answer)—it defaults to a "clarify" action. Instead of making a wild guess, it’ll politely ask you to repeat or rephrase your question, like a diligent assistant that really wants to get it right.

Example Request:
"Hmm, I’m thinking about… well, you know… can you… um, help?"

```
{
"action": "clarify",
"response": "I didn’t quite understand your request. Could you rephrase it or provide a bit more detail so I can help you out?"
}
```
GPT-3 doesn’t just say, “I don’t get it”—it gently nudges you toward a clearer question. It’s like the AI equivalent of saying, “Sorry, what was that again?” but without the annoying tone.

Handling the Data in Siri Shortcuts
Once GPT-3 has given you the action and response, the real magic happens in Siri Shortcuts.

Open the Shortcuts app on iOS, macOS, or iPadOS.
Create a new shortcut or edit an existing one to integrate the GPT-3 response.
Add in the details of your request, using the response data (e.g., action type, device, location, etc.) to trigger the appropriate smart home action.
For example:

If GPT-3 gives you a command action to turn on the lights in the living room, your Shortcut would use that information to trigger HomeKit to execute the command.
If GPT-3 sends back a query action, you can display the response data in a notification or run additional actions based on it.
And if GPT-3 comes back with an answer, you can display that as a voice response or text output, making it feel like the perfect AI assistant.
This workflow bridges GPT-3’s natural language understanding with the automation power of Siri Shortcuts, giving you a seamless way to control your smart home—or get general advice—with just your voice or a tap. It’s like having the best of both worlds: Siri’s integration with your devices and GPT-3’s insane conversational smarts!

(image2)

One trick to remember is that to run your shortcut, you can simply say the name of your shortcut to Siri. So “Okay Smart Home” seemed like a good idea.

Next, using the “Ask for <Text>…” action, we get the response from the user. This will be spoken out loud if you start the shortcut with Siri, or a type input field if you run by clicking the shortcut tile.

We are now ready to send our request to OpenAI. For this, you will need to register an account and get your API token. It’s unders “View API keys” menu item after loggin in.

Using the API will cost around $0.014 per request, so you could perform over 70 requests for $1. Bear in mind that this is considered expensive because our request is very long, so with shorter ones you will pay proportionally less. Maybe something to remember as you experiment.

(Image3)

Once you have your API token ready, fill our the details of the request:
— model: text-davinci-003
— prompt: <Text> Request: <Provided Input> Response:
— max_tokens: 1000

In the headers section, add:
— Content-Type: application/json
— Authorization: Bearer <addYourAPIToken>

Once we have the response data from the API, we need to dig it out as it’s nested in the JSON response. Once we have it, we assign it to a JSON variable, then we also extract the action category value:

(Image4)

With this, we are now ready to check the value of the action category in an if statement:

(Image5)

Once we know the action was a “command”, we can add further if statements to check the location, target and value fields and trigger the action: switching the office light on in our first example:

(Image6)

Outside the condition and after the “End If” blocks, we also show/announce the comment GPT-3 sent along with the request:

(Image7)

The query commands also work similarly with the built-in HomeKit actions:

(Image8)

Finally, the answer and clarify actions simply show/announce the returned value without any processing:

(Image9)

And that is all

Now I know this sounds like a lot of if else statements, and to perfectly honest, I haven’t actually done my whole house. However, I know that is possible to abstract your logic into further smaller shortcuts with input parameters and they can return with a value (similar to functions in coding). I’m going to look into that and see if I can simplify things. Let me now if you have any ideas around that!

Link to my Shortcut for you to try and adapt: https://www.icloud.com/shortcuts/e5d4033cf8024b5796e270c8fed9e478

Conclusion
How cool is this?? Being able to create your own smart assistants by simply defining it in plain English is simply mind blowing.

But this is just one example. Imagine all the different prompts you could send to GPT-3 and then all the different actions you could perform in Siri Shortcuts.

I’m almost certain you already have a few ideas around this so please let me know as I’m really interested!

  