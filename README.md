# Twilio Flex Plugin - Inbound call ring and alert

This twilio Flex Plugin is based on the [plugin-select-ringing-device
 Plugin](https://github.com/twilio-professional-services/plugin-select-ringing-device). It implements two enhancements to alert agents to an incoming call:
1. Alert agents with by ringing their device with a configurable ringtone
2. With permission, notify them of an incoming task using the operating system's standard notification mechanism using the [Notifications web API](https://developer.mozilla.org/en-US/docs/Web/API/Notifications_API/Using_the_Notifications_API) 

## Pre-Requirements

- An active Twilio account with Flex provisioned. Refer to the [Flex Quickstart](https://www.twilio.com/docs/flex/tutorials/setup) to create one.
- MP3 file you would like to use as a ringtone for incoming Flex calls
- npm version 5.0.0 or later installed (type `npm -v` in your terminal to check)
- Node.js version 12 or later installed (type `node -v` in your terminal to check)
- [Twilio CLI](https://www.twilio.com/docs/twilio-cli/quickstart#install-twilio-cli) along with the [Flex CLI Plugin](https://www.twilio.com/docs/twilio-cli/plugins#available-plugins) and the [Serverless Plugin](https://www.twilio.com/docs/twilio-cli/plugins#available-plugins). Run the following commands to install them:
  ```bash
  # Install the Twilio CLI
  npm install twilio-cli -g
  # Install the Serverless and Flex as Plugins
  twilio plugins:install @twilio-labs/plugin-serverless
  twilio plugins:install @twilio-labs/plugin-flex
  ```
## Functions & Flex Plugin Setup

1. Clone this repo:

  ```bash
  git clone https://github.com/randyjohnston/plugin-inbound-call-ring-alert
  ```

2. Install the dependencies

  ```bash
  # Install the dependencies of the Flex Plugin
  npm install
  ```

3. Copy the `.env.example` file in the root directory:

  ```bash
  cp .env.example .env
  ```

4. Copy the `public/appConfig.example.js` over:

  ```bash
  cp public/appConfig.example.js public/appConfig.js
  ```

5. Upload your ringtone MP3 file as a Twilio asset, replacing the :

  ```bash
  twilio assets:init 
  twilio assets:upload ~/Downloads/ringtone.mp3
  ```
The resulting Twilio asset URL will return in the format of: `https://hello-world-0000.twil.io/ringtone.mp3`. Record this URL for the next step.

6. Edit `.env`:

  ```bash
  REACT_APP_RINGTONE_URL=Link to audio file to pay when an inbound call is reserved to agent
  ```

## Development

In order to develop locally, you can use the Webpack Dev Server by running (from the root plugin directory):

  ```bash
  # Start Flex Plugin
  twilio flex:plugins:start
  ```

This will automatically start up the Webpack Dev Server and open the browser for you. Your app will run on `http://localhost:3000`. If you want to change that you can do this by setting the `PORT` environment variable:

When you make changes to your code, the browser window will be automatically refreshed.

## Deploy

When you are ready to deploy your plugin, deploy your Flex Plugin:

```bash
twilio flex:plugins:deploy --major --changelog "Notes for this version" --description "Functionality of the plugin"
```

For more details on deploying your plugin, refer to the [deploying your plugin guide](https://www.twilio.com/docs/flex/plugins#deploying-your-plugin).