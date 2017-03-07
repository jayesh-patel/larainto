# Frontuser API References
<p>Each API request is authenticated by an authentication token in the request header and use <code><b>application/json</b></code> for request and response data. The access [i.e. authorization] token and content type should be sent through request headers same as below:</p>
<code><strong>Authorization</strong>: Bearer ACCESS_TOKEN</code><br /><code><strong>Content-Type</strong>: application/json</code><br />
<p>Each authorized token is valid for <b>3600</b> <i>ms(milisecond)</i>, you can revoke expired token with the help of <b>refresh_token</b> through <b>Refresh Access Token</b> api call.</p>


## Pre-request
<p>User must have:</p>
- ***client_id*** 
- ***client_secret***

## Response Code
<table>
<thead>
<tr>
<th>Response Code</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>200</td>
<td>Success</td>
</tr>
<tr>
<td>400</td>
<td>Invalid or missing parameter, invalid or missing HTTP header</td>
</tr>
<tr>
<td>401</td>
<td>Invalid Authorization header</td>
</tr>
<tr>
<td>404</td>
<td>Invalid end point</td>
</tr>
<tr>
<td>500</td>
<td>Invalid parameter</td>
</tr>
<tr>
<td>502</td>
<td>Invalid parameter content</td>
</tr>
<tr>
<td>503</td>
<td>Server encounter some error please try again</td>
</tr>
<tr>
<td>504</td>
<td>Data not found</td>
</tr>
</tbody>
</table>

# Authorization [/auth]
<p>These API is use for retrieve authorization token to API call. The resources in this section are generate Access Token and Refresh Access Token:</p>

## Generate Access Token [POST /v1/auth/accessToken]
<p>Obtain an access token for API calls.</p>
+ Request (multipart/form-data)
    
    + Body

            {
                "grant_type": "client_credentials",
                "client_id": "YOUR_SECRET_ID",
                "client_secret": "YOUR_SECRET"
            }

+ Response 200 (application/json)
    + Body

            {
                "access_token": "mq2dyCmqqzmQUrRqogTtx0QWeoUszFUVJXT0KyNF",
                "token_type": "Bearer",
                "expires_in": 3600,
                "refresh_token":"ZXef3W3jNcGqV57dGP59MNw765200I1JHlHmZHcm"
            }

## Refresh Access Token [POST /v1/auth/refreshToken]
<p>Refreshing an Expired Access Token. Revoke an expired access token for through its <b>refresh_token</b>. Each <b>refresh_token</b> has been expired after <b>7 days</b> of its generated datetime, in cases if your referesh token is expired then you need to regenerate access token using <b>Generate Access Token</b> API call instead of refreshing.</p>

+ Request (multipart/form-data)
    + Body

            {
                "grant_type": "refresh_token",
                "client_id": "YOUR_SECRET_ID",
                "client_secret": "YOUR_SECRET",
                "refresh_token": "ZXef3W3jNcGqV57dGP59MNw765200I1JHlHmZHcm"
            }

+ Response 200 (application/json)
    + Body

            {
                "access_token": "mq2dyCmqqzmQUrRqogTtx0QWeoUszFUVJXT0KyNF",
                "token_type": "Bearer",
                "expires_in": 3600,
                "refresh_token":"ZXef3W3jNcGqV57dGP59MNw765200I1JHlHmZHcm"
            }
            
# Subscribers [/v1/subscriber]            
<p>The Subscribers is primary resource for every push notifications. You can list all those subscribers and assign/delete from your website segmentation. Subscribers can be viewed individually or as a list.</p>

## Get Subscribers Details [POST /v1/subscribers/list]
<p>Retrieves a subscriber's basic details including their unique id, browser notification subscription id, active/inactive state, etc.</p>
+ Request (application/json)
    + Headers

            Authorization: Bearer ACCESS_TOKEN
    + Body

            {
                "body": {
                    "website_id": "WEB_HASH",
                    "limit":5,
                    "offset":0,
                    "filters_match":"any",
                    "filters":{
                        "browser":["chrome","firefox"],
                        "device":["desktop","mobile"],
                        "push_status":["active","inactive","both"],
                        "timezone":["Asia/Kolkata","America/Chicago"],
                        "country_code":["IN","US"]
                    }
                }
            }
            
+ Response 200 (application/json)
    + Body

            {
                "status": "success",
                "total_items":3,
                "offset":0,
                "limit":5,
                "items": [
                {
                    "id":"58342836ab4f774d5d8b456f",
                    "registration_id":"e-Eal6subL0:APA91bG9HGIQ0oMyFgN76dM1yjHYp8_uUQIczeG4yXdBwwoRxTrf-BDTc284CpSa47rpZJ1mlfps3DSIt1VJlPgLO1pkbFraPROaE1_-VJxo8bQ1VPfZd29U_ADY1KKl6GHPPxJCKUE6",
                    "browser":"Chrome",
                    "device":"desktop",
                    "push_notification_status":"active",
                    "subscribed_on":"2016-12-25 00:00:10 +05:30",
                    "timeZone": "Asia/Kolkata",
                    "country_code": "IN"
                },
                {
                    "id":"582ab059ab4f77505d8b456d",
                    "registration_id":"gAAAAABYE0f1wuFfSOAr03z4TxoFy9fJ1jJ6QxPiNxF-YuuIWwNvFgiNTWvrvwKNJZmp2OFKTegZqBMU7bqKx2OLN32beoNg9jqbkytIXpUJ6Oz6oaQy5qfWG266S0DuxKpQDjQEFZzm",
                    "browser":"Firefox",
                    "device":"desktop",
                    "push_notification_status":"active",
                    "subscribed_on":"2016-11-20 03:15:10 +05:30",
                    "timeZone": "Asia/Kolkata",
                    "country_code": "IN"
                },
                {
                    "id":"58085d13ab4f77ad688b4569",
                    "registration_id":"ehaGPctDV1k:APA91bGPlG9fFp2GZSyiDH1e9KfnusTfVSr_NTlaDFaz-2LYjMa2GTOvTr4vJRugcU8lDS4BcyKHOocECz-0BJlmseS_DmbLddsOjE-g0pv8S2q36rzaRjir4Fg-BSCnRXQRf3kBg3dw",
                    "browser":"Chrome",
                    "device":"mobile",
                    "push_notification_status":"active",
                    "subscribed_on":"2016-12-25 00:00:10 +05:30",
                    "timeZone": "Asia/Kolkata",
                    "country_code": "IN"
                }
                ],
                "code": "200"
            }

## Get Individual Subscriber Details [POST /v1/subscriber/detail]
<p>Retrieves overall details for particular subscriber.</p>
+ Request (application/json)
    + Headers

            Authorization: Bearer ACCESS_TOKEN
    + Body

            {
                "body": {
                    "website_id": "WEB_HASH",
                    "subscriber_id":"58342836ab4f774d5d8b456f"
                }
            }
+ Response 200 (application/json)
    + Body

            {
                "status": "success",
                "data": 
                {
                    "id":"58342836ab4f774d5d8b456f",
                    "registration_id":"e-Eal6subL0:APA91bG9HGIQ0oMyFgN76dM1yjHYp8_uUQIczeG4yXdBwwoRxTrf-BDTc284CpSa47rpZJ1mlfps3DSIt1VJlPgLO1pkbFraPROaE1_-VJxo8bQ1VPfZd29U_ADY1KKl6GHPPxJCKUE6",
                    "website":"Frontuser",
                    "device":"desktop",
                    "browser":"Chrome",
                    "browser_ver":"53",
                    "language": "en_US",
                    "os": "Mac",
                    "user_agent": "Mozilla/5.0 (Linux; Android 6.0.1; ONEPLUS A3003 Build/MMB29M) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/54.0.2840.68 Mobile Safari/537.36",
                    "timeZone": "Asia/Kolkata",
                    "country_code": "IN",
                    "country": "India",
                    "city": "Mumbai",
                    "state": "Maharashtra",
                    "postal_code": "400099",
                    "lat": "19.0144",
                    "lon": "72.8479",
                    "push_notification_status":"active",
                    "subscribed_on":"2016-12-25 00:00:10 +05:30"
                },
                "code": "200"
            }

   
# Segmentation [/v1/segment]
<p>Segmentation is the process of dividing a broad subscribers into sub-group of subscribers (known as segments) based on some type of shared characteristics. For example, here are some common segments to explore:</p>
- ***Browser type*** 
- ***Mobile, desktop or by device***
- ***Geographical regions (City, State/Province, Country)***
- ***Language***
- ***Timezone***
- ***Many more....***
<p>Segmenting your results gives you valuable insights about different groups of subscribers, instead of simply analyzing the results across your entire subscribers base. With the help Segmentation API's you can <i><b>add new</b></i> segments, <i><b>list/delete</b></i> existing segments, <i><b>adding/removing</b></i> subscribers <i><b>to/from</b></i> the segment.</p>

## Create New Segment [POST /v1/segment]
<p>To create new segment, send POST request to this method.</p>

+ Request (application/json)
    + Headers

            Authorization: Bearer ACCESS_TOKEN
    + Body

            {
                "body": {
                    "website_id": "WEB_HASH",
                    "name": "Foo Name"
                }
            }

+ Response 200 (application/json)
    + Body

            {
                "status": "success",
                "segment_id":"58143883ab4f776a5c8b456e",
                "message": "Segment created successfully.",
                "code": "200"
            }
            
## Delete Segment [DELETE /v1/segment]
<p>This method is used to delete existing segment.</p>
<p><strong>Please note:</strong> deleting a segment will also remove all the subscribers from that particular segment. The subscribers will not be deleted you may be added to more segments later on.</p>

+ Request (application/json)
    + Headers

            Authorization: Bearer ACCESS_TOKEN
    + Body

            {
                "body": {
                    "website_id": "WEB_HASH",
                    "segment_id": "58143883ab4f776a5c8b456e"
                }
            }

+ Response 200 (application/json)
    + Body

            {
                "status": "success",
                "message": "Segment deleted successfully.",
                "code": "200"
            }

## Add Subscribers To Segmentation [POST /v1/segment/subscribers]
<p>This API is used for adding subscribers list to particular segment.</p>
+ Request (application/json)
    + Headers

            Authorization: Bearer ACCESS_TOKEN
    + Body

            {
                "body": {
                    "website_id": "WEB_HASH",
                    "segment_id": "58143883ab4f776a5c8b456e",
                    "subscriber_ids":["58342836ab4f774d5d8b456f", "582ab059ab4f77505d8b456d"]
                }
            }

+ Response 200 (application/json)
    + Body

            {
                "status": "success",
                "message": "Subscribers successfully added to segmentation.",
                "successfully_added":1,
                "skipped":1,
                "skipped_ids":["582ab059ab4f77505d8b456d"],
                "code": "200"
            }

## Delete Subscribers From Segmentation [DELETE /v1/segment/subscribers]
<p>Use this API to remove subscribers from particular segment.</p>
+ Request (application/json)
    + Headers

            Authorization: Bearer ACCESS_TOKEN
    + Body

            {
                "body": {
                    "website_id": "WEB_HASH",
                    "segment_id": "58143883ab4f776a5c8b456e",
                    "subscriber_ids":["58342836ab4f774d5d8b456f", "582ab059ab4f77505d8b456d"]
                }
            }

+ Response 200 (application/json)
    + Body

            {
                "status": "success",
                "message": "Subscribers successfully removed from segmentation.",
                "successfully_deleted":1,
                "skipped":1,
                "skipped_ids":["582ab059ab4f77505d8b456d"],
                "code": "200"
            }

## Get The List Of Segments [GET /v1/segment/{webHash}]
<p>This API is used to get the list of segmentation.</p>
+ Parameters
    + webHash (required, string) - You website unique hash
+ Request
    + Headers

            Authorization: Bearer ACCESS_TOKEN
            
+ Response 200 (application/json)
    + Body

            {
                "status": "success",
                "list": [
                    {"id":"0", "name":"All users", "created_from": "System Default"}, 
                    {"id":"580da56cab4f776b5c8b4569", "name":"New Users", "created_from": "Dashboard"}, 
                    {"id":"581440a7ab4f776a5c8b456f", "name":"Chrome Users", "created_from": "API"}
                ],
                "code": "200"
            }
            
# Send Notification [/api/v1/send]
<p>These API will use for sending notification to users. The resources in this section are send notification to segment subscriber, and send notification to particular subscriber:</p>

## Send Notification To Segment Subscribers [POST /v1/send]
<p>Send notification to all those subscribers which fulfill segmentation rule criteria for particular website.</p>

+ Request (application/json)
    + Headers

            Authorization: Bearer ACCESS_TOKEN
    + Body

            {
                "body": {
                    "website_id": "WEB_HASH",
                    "name": "Foo Name",
                    "title": "Sample Title",
                    "message": "Sample Message",
                    "target_url": "http://www.example.com",
                    "logo": "http://example.com/image.png",
                    "segment_id": "58143883ab4f776a5c8b456e",
                    "utm_params": {
                        "utm_params": "params",
                        "utm_param": "value"
                    },
                    "time_to_live":{
                        "expired_after": 10,
                        "expiration_unit": "hours"
                    }
                }
            }

+ Response 200 (application/json)
    + Body

            {
                "status": "success",
                "notification_id": "581443f6ab4f77b0688b4569",
                "total_sent": 10,
                "success_count": 8,
                "failed_count":2,
                "total_subscribers": 15,
                "code": "200"
            }

## Send Notification To Individual Subscriber [POST /v1/send/subscriber]
<p>Send notification to specific subscriber for particular website.</p>

+ Request (application/json)
    + Headers

            Authorization: Bearer ACCESS_TOKEN
    + Body

            {
                "body": {
                    "website_id": "WEB_HASH",
                    "name": "Foo Name",
                    "title": "Sample Title",
                    "message": "Sample Message",
                    "target_url": "http://www.example.com",
                    "logo": "http://example.com/image.png",
                    "subscriber": "582ab059ab4f77505d8b456d",
                    "utm_params": {
                        "utm_params": "params",
                        "utm_param": "value"
                    },
                    "time_to_live":{
                        "expired_after": 10,
                        "expiration_unit": "hours"
                    }
                }
            }

+ Response 200 (application/json)
    + Body

            {
                "status": "success",
                "notification_id": "581443f6ab4f77b0688b4569",
                "code":"200"
            }

## Send Notification To Subscribers [POST /v1/send/subscriber/list]
<p>Send notification to multiple subscribers for particular website.</p>

+ Request (application/json)
    + Headers

            Authorization: Bearer ACCESS_TOKEN
    + Body

            {
                "body": {
                    "website_id": "WEB_HASH",
                    "name": "Foo Name",
                    "title": "Sample Title",
                    "message": "Sample Message",
                    "target_url": "http://www.example.com",
                    "logo": "http://example.com/image.png",
                    "subscriber_ids": [
                        "582ab059ab4f77505d8b456d", 
                        "58342836ab4f774d5d8b456f"
                    ],
                    "utm_params": {
                        "utm_params": "params",
                        "utm_param": "value"
                    },
                    "time_to_live":{
                        "expired_after": 10,
                        "expiration_unit": "hours"
                    }
                }
            }

+ Response 200 (application/json)
    + Body

            {
                "status": "success",
                "notification_id": "581443f6ab4f77b0688b4569",
                "total_sent": 10,
                "success_count": 8,
                "failed_count":2,
                "total_subscribers": 15,
                "code": "200"
            }
            
## List Of Sent Notification [POST /v1/sent/list]
<p>To retrieve a list of sent notifications, submit a POST request to this method: </p>

+ Request (application/json)
    + Headers

            Authorization: Bearer ACCESS_TOKEN
    + Body

            {
                "body": {
                    "website_id": "WEBSITE_HASH",
                    "limit":5,
                    "offset":0
                }
            }

+ Response 200 (application/json)
    + Body

            {
                "status": "success",
                "total_items":7,
                "offset":0,
                "limit":5,
                "items": [
                {
                    "id":"581443f6ab4f77b0688b4569",
                    "segment_id":"58143883ab4f776a5c8b456e",
                    "name":"Notification Demo",
                    "title":"My First Notification",
                    "message":"Welcome to Frontuser",
                    "icon_url":"https://www.example.com/logo.png",
                    "redirect_url":"https://frontuser.com/",
                    "utm_params":{
                        "source":"direct",
                        "medium":"search engine",
                        "campaign":"Discount Promo"
                    },
                    "sent_datetime":"2016-12-25 00:00:10 +05:30",
                    "created_datetime":"2016-12-24 12:50:00 +05:30",
                    "schedule_datetime":"2016-12-25 00:00:00 +05:30"
                },
                {
                    "id":"581443f6ab4f77b0688b4569",
                    "segment_id":"58143883ab4f776a5c8b456e",
                    "name":"Notification Demo",
                    "title":"My First Notification",
                    "message":"Welcome to Frontuser",
                    "icon_url":"https://www.example.com/logo.png",
                    "redirect_url":"https://frontuser.com/",
                    "utm_params":{
                        "source":"direct",
                        "medium":"search engine",
                        "campaign":"Discount Promo"
                    },
                    "sent_datetime":"2016-12-25 00:00:10 +05:30",
                    "created_datetime":"2016-12-24 12:50:00 +05:30",
                    "schedule_datetime":"2016-12-25 00:00:00 +05:30"
                }
                ],
                "code": "200"
            }

## Notification Status [POST /v1/notification/status]
<p>To get the sending status of notifications, submit a POST request to this method.</p>
+ Request (application/json)
    + Headers

            Authorization: Bearer ACCESS_TOKEN
    + Body

            {
                "body": {
                    "website_id": "WEBSITE_HASH",
                    "notification_id": "581443f6ab4f77b0688b4569"
                }
            }      
+ Response 200 (application/json)
    + Body

            {
                "status": "success",
                "notification_id": "581443f6ab4f77b0688b4569",
                "sending_status": "sent",
                "sent_datetime": "2016-12-25 03:00:00 +05:30",
                "code": "200"
            }
 
## Notification Report Statistics [POST /v1/notification/stats]           
<p>You can used this API to analyze the effectiveness of your push notifications.</p>
+ Request (application/json)
    + Headers

            Authorization: Bearer ACCESS_TOKEN
    + Body

            {
                "body": {
                    "website_id": "WEBSITE_HASH",
                    "notification_id": "581443f6ab4f77b0688b4569"
                }
            }            
+ Response 200 (application/json)
    + Body

            {
                "status": "success",
                "status": "sent",
                "sent_datetime": "2016-12-25 03:00:00 +05:30",
                "success":15,
                "failed":1,
                "clicked_count":7,
                "clicked_rate":"46.66%",
                "code": "200"
            }
 
[Markdown site][df1]

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

[df1]: <./license.html>