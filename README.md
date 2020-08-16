# Govhack2020:Citizen-In-Touch

This Application aims to bring the authorities and the local residents in touch.
The local residents can register through the portal and take up the responsibility to alert the authorities about the potential emergency.
Also the interested residents can subscribe to the portal to be informed about the emergency incidents around them.
The authorities can review and react on the emergency incidents reported by the volunteers and can notify the local residents using the Telstra Messaging API.

On a higher level the application's notify module integrates with Telstra Messaging API to deliver the messages to the subscribed residents.
The Notify Module Uses following Endpoints from Telstra Messaging API.

Authentication: 
var settings = {
  "url": "https://tapi.telstra.com/v2/oauth/token",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "Content-Type": "application/x-www-form-urlencoded"
  },
  "data": {
    "client_id": "<<Client_Id>>",
    "client_secret": "Client_Secret",
    "grant_type": "client_credentials",
    "scope": "NSMS"
  }
};

$.ajax(settings).done(function (response) {
  console.log(response);
});


Subscription:
var settings = {
  "url": "https://tapi.telstra.com/v2/messages/provisioning/subscriptions",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "Authorization": "Bearer" + Token,
    "Content-Type": "application/json"
  },
  "data": JSON.stringify({"activeDays":20}),
};

$.ajax(settings).done(function (response) {
  console.log(response);
});


var settings = {
  "url": "https://tapi.telstra.com/v2/messages/sms",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "Authorization": "Bearer "+Token,
    "Content-Type": "application/json"
  },
  "data": JSON.stringify({"to":"<Number>","validity":"10","body":"Emergency Notification: Bushfires Alert","from":"Disaster Response Team"}),
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
