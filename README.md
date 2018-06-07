# alexa-helper

Utilities for working with Alexa skills.
- Cleaning up SSML.
- Getting slot values for intents.
- Converting arrays into readable strings.
- Building options for external API calls and calling them easily.

Example: 
```javascript
const helper = require('alexa-helper');

const api = {
    hostname: 'data.example.org',
    resource: '/resource/example.json'
};

const MyIntentHandler = {
    canHandle(handlerInput) {
        // your criteria
    },
    async handle(handlerInput) {
        const filledSlots = handlerInput.requestEnvelope.request.intent.slots;
        const slotValues = helper.ssmlHelper.getSlotValues(filledSlots);
        const params = [
            ['MyParam', `${slotValues.MySlot.resolved}`]
        ];

        const options = helper.httpsHelper.buildOptions(params, api, process.env.APP_TOKEN);

        try {
            const response = await helper.httpsHelper.httpGet(options);
        } catch (error) {
            // handle error
        }
    }
};
```