<a  href="https://www.twilio.com">
<img  src="https://static0.twilio.com/marketing/bundles/marketing/img/logos/wordmark-red.svg"  alt="Twilio"  width="250"  />
</a>
 
# Park and Transfer Flex Plugin

The Park and Transfer Flex plugin facilitates pausing and transferring of [Flex Conversations](https://www.twilio.com/docs/flex/conversations) tasks. 

## Set up

Please see the Flex Conversations [Prerequisites](https://www.twilio.com/docs/flex/admin-guide/setup/conversations/prerequisites) page to prepare your Flex account for testing.

### Twilio Account Settings

Before we begin, we need to collect
all the environment variables we need to run the application:
- **FLEX_APP_ACCOUNT_SID** - Your primary Twilio account identifier or username - find this [in the Console](https://www.twilio.com/console)
- **FLEX_APP_AUTH_TOKEN** - Your Twilio account auth token or password - find this [in the Console](https://www.twilio.com/console)
- **FLEX_APP_WORKSPACE_SID** - Your Twilio TaskRouter workspace. Named "Flex Task Assignment" by default.
- **FLEX_APP_WORKFLOW_SID** - Your Twilio TaskRouter Workflow that you want to use for task pauses and transfers.
- **FLEX_APP_INTERACTION_URL** - The Interactions API Endpoint. Set this to `https://flex-api.twilio.com/v1/Interactions`.
- **FLEX_APP_URL** - Your publicly accessible ngrok domain (in https) if you do not have a public server. Note that you will need to create an ngrok account and add your authtoken. See the [ngrok setup guide](https://dashboard.ngrok.com/get-started/setup) for more details. The app in this plugin uses port 9000 by default. To start, run `ngrok http 9000`.

In the root directory of your repository clone, copy `.env.template` to `.env.` Update the file with your Twilio account settings.

Copy .env.template to .env to the root of the project in the root of the project 
Update the values in the .env (If you dont have a public server, use ngrok, port 9000 by default, and use the fqdn as the APP_URL in the .env file)
Start node /bin/www


### Test the plugin

After the above requirements have been met, do the following:
1. Change into the server directory.
    `cd server`
2. Run `npm install` to install the package dependencies.
3. Run `npm start`.
4. In a different tab, run `twilio flex:plugins:start` in the root directory of the repo. This should start up your Flex application on localhost.
5. To test, send an SMS or a WhatsApp message to your Twilio Flex number with a Conversations address. You should see the Pause and Transfer buttons in the Flex Task Canvas. 

```
git clone git@github.com:twilio-labs/plugin-queued-callbacks-and-voicemail.git
```

2. Change into the `public` subdirectory of the repo and run the following:

```
cd plugin-queued-callbacks-and-voicemail/public && mv appConfig.example.js appConfig.js
```

3. Install dependencies

```bash
npm install
```

4. [Deploy your Twilio Functions and Assets](#twilio-serverless-deployment)

5. Run the application

```bash
twilio flex:plugins:start
```

See [Twilio Account Settings](#twilio-account-settings) to locate the necessary environment variables.

7. Run the application

```bash
npm start
```

Alternatively, you can use this command to start the server in development mode. It will reload whenever you change any files.

```bash
npm run dev
```

8. Navigate to [http://localhost:3000](http://localhost:3000)

That's it!

#### Pre-deployment Steps

1. From the root directory of your copy of the source code, change into `serverless` and rename `.env.example` to `.env`.

```
cd serverless && mv .env.example .env
```

2. Open `.env` with your text editor and modify TWILIO_WORKSPACE_SID with your Flex Task Assignment SID.

```
TWILIO_WORKSPACE_SID=WSxxxxxxxxxxxxxxxxxxxxxx`
```

3. To deploy your Callback and Voicemail functions and assets, run the following:

```
$ twilio serverless:deploy --assets

## Example Output
Deploying functions & assets to the Twilio Runtime
Env Variables
⠇ Creating 4 Functions
✔ Serverless project successfully deployed

Deployment Details
Domain: plugin-queued-callbacks-voicemail-functions-xxxx-dev.twil.io
Service:
  plugin-queued-callbacks-voicemail-functions 
Functions:
  https://plugin-queued-callbacks-voicemail-functions-xxxx-dev.twil.io/inqueue-callback
  https://plugin-queued-callbacks-voicemail-functions-xxxx-dev.twil.io/inqueue-utils  
  https://plugin-queued-callbacks-voicemail-functions-xxxx-dev.twil.io/queue-menu
  https://plugin-queued-callbacks-voicemail-functions-xxxx-dev.twil.io/inqueue-voicemail

Assets:
  https://plugin-queued-callbacks-voicemail-functions-xxxx-dev.twil.io/assets/alertTone.mp3
  https://plugin-queued-callbacks-voicemail-functions-xxxx-dev.twil.io/assets/guitar_music.mp3
```

_Note:_ Copy and save the domain returned when you deploy a function. You will need it in the next step. If you forget to copy the domain, you can also find it by navigating to [Functions > API](https://www.twilio.com/console/functions/api) in the Twilio Console.

> Debugging Tip: Pass the -l or logging flag to review deployment logs. For example, you can pass `-l debug` to turn on debugging logs.

### Deploy your Flex Plugin 

Once you have deployed the function, it is time to deploy the plugin to your Flex instance.

Run the following commands in the plugin root directory. We will leverage the Twilio CLI to build and deploy the Plugin.

1. Rename `.env.example` to `.env`.
2. Open `.env` with your text editor and modify the `REACT_APP_SERVICE_BASE_URL` property to the Domain name you copied in the previous step. Make sure to prefix it with "https://".
	
	```
	plugin-queued-callbacks-and-voicemail $ mv .env.example .env
	
	# .env
	REACT_APP_SERVICE_BASE_URL=https://plugin-queued-callbacks-voicemail-functions-4135-dev.twil.io
	```

3. When you are ready to deploy the plugin, run the following in a command shell:
	
	```
	plugin-queued-callbacks-and-voicemail $ twilio flex:plugins:deploy --major --changelog "Updating to use the latest Twilio CLI Flex plugin" --description "Queued callbacks and voicemail"
	``` 

4. To enable the plugin on your contact center, follow the suggested next step on the deployment confirmation. To enable it via the Flex UI, see the [Plugins Dashboard documentation](https://www.twilio.com/docs/flex/developer/plugins/dashboard#stage-plugin-changes).


Update the values in the .env (If you dont have a public server, use ngrok, port 9000 by default, and use the fqdn as the APP_URL in the .env file)
Start node /bin/www
Start the server - see README in server director
Update the server URL in actions.js
start the plugin

## License

[MIT](http://www.opensource.org/licenses/mit-license.html)

## Disclaimer

No warranty expressed or implied. Software is as is.

[twilio]: https://www.twilio.com
