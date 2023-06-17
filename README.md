# tiltify-donation-bot
A bot that sends a message in Twitch chat when a new Tiltify donation is detected. Updated to support the Tiltify V5 API.

![Screenshot of Twitch bot](https://i.imgur.com/Y4VWpZ2.png)

## Installation
> **NOTE:** Your Python 3 instance may be installed as simply `python` — if that's the case, swap out the references of `python3` below with `python`.

First, clone or download this repository and open the directory created in your terminal. Ensure Python 3.7 or later is installed (`python3 -V`). Install all dependencies by running `python3 -m pip install -r requirements.txt`.

Then, open `credentials-example.json`, and add your Tiltify and Twitch credentials to it. Here's what you need:

| Name | Description |
| --- | --- |
| `tiltify_client_id` | Generated by creating an application on your Tiltify dashboard. [Refer to this link to find out how.](https://developers.tiltify.com/docs/getting-started/create-an-application) |
| `tiltify_client_secret` | Generated by creating an application on your Tiltify dashboard. [Refer to this link to find out how.](https://developers.tiltify.com/docs/getting-started/create-an-application) |
| `tiltify_user_slug` | The username of the Tiltify account with the campaign you want to set up alerts for. For example, [in this campaign](https://tiltify.com/@gamingforglobalchange/level-up-campaign) it's `gamingforglobalchange`. |
| `tiltify_campaign_slug` | The part of the campaign URL that refers to the name of the campaign itself. For example, [in this campaign](https://tiltify.com/@gamingforglobalchange/level-up-campaign) it's `level-up-campaign`. |
| `twitch_access_token` | Can be easily obtained by logging in with your bot's Twitch account [here](https://twitchtokengenerator.com/) and requesting a Bot Chat Token. |
| `twitch_channel_names` | The usernames of the Twitch channels you want to send the alerts to. If you're only sending to one channel, this should equal `["yourchannel"]`. If you're sending to multiple, the formatting is `["channel1", "channel2", "channel3"]` and so on.|

Save your changes, and rename the file to `credentials.json`. Finally, run the bot with `python3 bot.py` and you should be up and running!

## Customizable variables
In `bot.py`, you can edit the following variables at the top of the file:

- `DONATION_CURRENCY`: The currency the Tiltify campaign is raising money in. Used for formatting the chat alert. For example, if you are fundraising in euros, this should be `'€'`.
- `MININUM_DONATION`: The minimum donation amount needed for an alert to show up in chat. This will use the currency that is set on the Tiltify campaign. For example, if you want to set the minimum donation to 10 USD (and the campaign is in USD), this should be set to `10`.
- `API_POLL_RATE`: The amount in seconds the Tiltify API is called to check for new donations. By default, this is set to `5`. Lowering this number is not recommended and you are the only one responsible if you get blacklisted.

## Limitations
This bot was developed with edge cases in mind, however there are still some extreme situations to consider. Since the bot relies on calling external APIs, it may be subject to any rate limiting done on the part of the API maintainers. 

As far as I can tell, there is no formal rate limit with the Tiltify API established. Based on an employee's response [here,](https://github.com/Tiltify/api/issues/9) it is called every 5 seconds by default — you can change this if you wish, but you are the only one responsible if you get blacklisted. 

Twitch's v5 API rate limit is very generous at 800 calls per minute (with OAuth), meaning you can effectively send 800 donation alerts per minute before getting limited. This should be more than enough for practically every use case, and I have not implemented any limit in the code because of this, however please keep this in mind if you are using this for an extremely high volume fundraiser.
