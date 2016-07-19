# Overview Local Environment Set up
---

## Assumptions
- The document presumes the base Canvas Application to be https://hbs-dev.instructure.com. The same steps could be followed the test and the production instances.

## 1. Developer Access
The user will need a admin access to the base Canvas application. 

### 1.1 Access Token
The below steps describe the procedure to create a access token that will be needed by the Overview application to integrate to base Canvas application. 

1. Login into the base Canvas app.
2. Navigate to *Account* > *Settings*.
3. Scrolldown to *Approved Integrations*.
4. Click on ***New Access Token***
5. On the popup appearing, provide a purpose (say Development) and expiry date and click on ***Generate Token***
6. Copy the token from the popup. Please note that the same access token will not be available for copy again. Hence make sure to copy it.

### 1.2 Developer Keys and Id

The below stpes describe the procedure to create developer keys and id that will be needed by the Overview application to integrate to the base Canvas application. 

1. Login into the base Canvas app.
2. Navigate to *Admin* > *Harvard Business School-Dev* > *Developer Keys* 
3. Click on ***Add Developer Key***
4. In the popup provide values for *Key Name* (some name so that you can identify that it is your key), *Owner Email* (your email) and *Redirect URL* (your local application url).
5. Once saved, the key will show up in the list and will have your **ID** and **Key**.
6. Copy the ID and Key.

## 2. Create Web Hooks

1. Open a terminal (in Linux or Mac) or Cygwin window in PC.
2. Change the directory to the root folder of the Overview application.
3. Create a new file named *webhook.json* and enter the below data into it. You may provide any URL in the call back URL.
```javascript
{
    "webhook": {
      "callback_url": "http://localhost:3000/",
      "event_types": [
        "assignment_group",
        "assignment"
      ]
  }
}
```
4. Now run the below command to get the Canvas Web Hook token from the terminal. Use the access token generated in step 1.1.
```
curl https://hbs-dev.instructure.com/api/v1/webhooks \
    -X POST \
    -H "Authorization: Bearer <Access Token>" \
    -H "Content-Type: application/json" \
    --data-binary "@webhook.json"
```
5. The repsonse will be something like below.
```javascript
{
	"webhook":{
    	"id":8,
        "callback_url":"http://localhost:3000/",
        "account_id":1,
        "event_types":["assignment_group","assignment"],
        "token":"7b9496c94825b8d16765784ea9a4a72d",
        "created_at":"2016-07-19T17:35:45Z",
        "updated_at":"2016-07-19T17:35:45Z","user_id":52
        }
}
```
6. Copy the ***token*** and ***account_id*** fields from the response. 

## 3. Create Account

1. From the terminal or Cygwin window, run the command ```rails c```. This will open up the rails console.
2. From the IRB prompt, set the variable named *settings* as provided below.
```Ruby
settings = {
  account_admin_api_token: '<Access Token>',
  base_url: 'https://hbs-dev.instructure.com', #replace with domain where the tool will be installed
  canvas_hook_key: '<Canvas Hook Key from step 2>' # Webhook shared secret for validating signed JWT requests
} 
```
3. Run the command as below from the IRB prompt.
```ruby
Account.create name: '<Any Name>', key: '<Any Unique Number, like 12345>', secret: '<Any Unique Number, like 123456>', oauth2_client_id: '<Developer Id from step 1.2>', oauth2_client_key: '<Developer Key from 1.2>', canvas_account_id: '<account_id from step 2>', settings:settings
```
4. This will create the account object for the application to registered with Canvas.

## 4. Generate the application XML
1. Navigate the URL https://www.edu-apps.org/build_xml.html. The XML needed to register any LTI application can be generated from this website.
2. In the text boxes provided, enter the data as described below:
|Field | Value|
|------|------|
|Name|Provide any valid name for the application|
|Id|Provide the value of the *key* attribute provided while creating the account in section 3|
|Description| Provide any valid description for the application.|
3. 