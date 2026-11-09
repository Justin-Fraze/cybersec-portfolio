# Automation & API Layer
Goal: Understand how data moves between systems and build your first no-code automation.

Research how REST APIs work (GET, POST requests, JSON payloads). Watch short documentation explainers on Make.com or Zapier.

Sign up for a free Make.com account. Build a simple 3-step scenario (e.g., when a Google Form is filled out, send an automated notification).

Project: Connect an LLM API (like OpenAI or Anthropic) into a Make.com workflow. Build a micro-automation where an email comes in, an LLM categorizes its urgency, and it posts a summary to a test Slack/Teams channel.

## REST APIs
Representational State Transfer Application Program Interface

### Introduction to API's
An API can be thought of as a gateway that allows the client to communicate with a server resource. The restaurant analogy is often used to describe how this works.

The request-response cycle is the key part of how API's work. A request from the client will need to have certain components, such as an HTTP method, a payload, URL/URI, and other information in the header and parameters. The response normally includes an HTTP status code, a payload (usually in JSON format), and additional header information.

<img width="1920" height="819" alt="image" src="https://github.com/user-attachments/assets/86bab158-fceb-4367-acf1-678da8913837" />

### No-code automation
As always, learning tech is 20% content and 80% doing. Let's see how basic automation works using a popular no-code platform: make.com. You can sign up for free on their website.

To get started, let's take a task that can be automated. I would like an automated text message every morning telling me the weather, the events on my Google Calendar, and an integration with a baseline routine I usually keep for my weekdays and weekends. In other words, I want to automate to-do lists and daily planning.

With our task now defined, you might see that make.com offers a prompt to speak with Maia, an AI coworker. Very funny to me that her name includes AI in it. I will start there and give my task as previously defined.

<img width="557" height="348" alt="image" src="https://github.com/user-attachments/assets/b1e5d75f-b1a9-46f7-b0f2-4b4ab2c11de8" />

The first response from Maia is asking how we would like to define the weather, with an offer to connect to the API for OpenWeather. Very cool--we are already seeing how API's work in automations by being the tool that allows us to view information from a separate database. Click though some of the other options that Maia will give, like how you want to send the SMS. I will be using Twilio for this example.

<img width="230" height="319" alt="image" src="https://github.com/user-attachments/assets/6c5706ae-4276-4bfc-b7d6-e581f79585b4" />

Eventually, you should see that Maia wants to create a connection to the OpenWeatherMap, and that it is asking for an API key.

<img width="559" height="325" alt="image" src="https://github.com/user-attachments/assets/2353374f-636f-4404-ba1e-19ffdf04c8b0" />

This part of the process should be highlighted. Why can't our automation just pull directly from web data to get the weather? Why do we need an API key? - We will revisit this.

make.com will integrate with Google Calendar, and Google Sheets (where I put a daily routine) next. Once we get all the connections going, we'll be good to go!

Making the Google Sheets routine can be quickly made by asking Gemini to look at the sheet and prompting it to write it for you. It's not lazy - it's using the tools as intended.





