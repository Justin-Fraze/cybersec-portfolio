# Automation and API Layer Lab

## Objective

I built a daily briefing automation in Make.com that combines a weather forecast, Google Calendar events, and Google Tasks into one Slack message. The scenario runs every morning at 7:00 AM.

The goal was to put what I learned about REST APIs into practice by connecting services and turning their data into something useful.

## Workflow

<img width="786" height="444" alt="image" src="https://github.com/user-attachments/assets/bb631e92-0332-461f-973c-d5b0fc2313b0" />

The scenario follows these steps:

1. **Weather:** Retrieves the daily weather forecast.
2. **Google Calendar:** Searches for calendar events, with a filter to include only today’s events.
3. **Text aggregator:** Combines the calendar events into text for the briefing.
4. **Google Tasks:** Retrieves tasks from my connected account.
5. **Text aggregator:** Combines the tasks into text.
6. **Slack:** Sends the weather, events, and tasks as a daily message.

Make.com handles the connections between services, while data mapping lets me use the information from earlier modules in the final Slack message.

## Working with APIs

My earlier research focused on how REST APIs use requests and responses to exchange data. This lab helped me see how that information moves through a working automation.

I used Make.com’s built-in modules to retrieve data and pass it between services. This let me focus on selecting the right fields, filtering results, and formatting the output without writing each API request manually.

## What I Learned

One of the main lessons was that retrieving data is only part of the process. The results also need to be filtered and organized so the final message is useful.

I practiced:

- Mapping information from one module into another.
- Filtering calendar results to include today’s events.
- Using text aggregators to combine multiple events and tasks.
- Scheduling a workflow to run automatically.
- Bringing information from several services into one message.

## Security Considerations

This workflow connects personal accounts and moves calendar and task information into Slack. That makes account permissions and the message destination important parts of the design.

Connections should have only the access the workflow needs, and API keys or other credentials should stay out of GitHub documentation and screenshots. Any example messages should also be checked for private event names, task details, or account information before publishing.

Further improvements would include reviewing the permissions granted to each connection and adding alerts for failed runs.

## Takeaway

This lab gave me hands-on experience connecting APIs through Make.com and turning the results into a scheduled notification. It also showed me how automation introduces security decisions around access, credentials, and where data is sent.


