Setting up a welcome message with quick replies in twitter dm.
-- Heather Nolis/Heather Wensler --


CREATE A BASIC WELCOME MESSAGE.

1 - Create the message.

		See:
		https://dev.twitter.com/rest/reference/post/direct_messages/welcome_messages/new

		SET-UP:
		1. Owner must allow DMS from anyone.
		2. Owner must have permissions to send DMS, read, and write

		Post to: 
		https://api.twitter.com/1.1/direct_messages/welcome_messages/new.json

		Authorization:
		OAuth 1.0
		Signature method: HMAC-SHA1
		Make sure "Add params to header" is checked.

		Send and recieve json.

		Body:
		{
		  "welcome_message" : {
			"message_data": {
			  "text": "Check - 1, 2. Check - 1, 2.",
			}
		  }
		}

		Response:
		{
			"welcome_message": {
				"id": "##################",
				"created_timestamp": "1498767082377",
				"message_data": {
					"text": "Check - 1, 2. Check - 1, 2.",
					"entities": {
						"hashtags": [],
						"symbols": [],
						"user_mentions": [],
						"urls": []
					}
				}
			}
		}

2- Create a rule for the welcome message.

		Post the following to
		https://api.twitter.com/1.1/direct_messages/welcome_messages/rules/new.json

		Send and recieve json.

		Body:
		{
		  "welcome_message_rule": {
			"welcome_message_id": "############"
		  }
		}

		Response:
		{
			"welcome_message_rule": {
				"id": "##############",
				"created_timestamp": "1498767794023",
				"welcome_message_id": "#################"
			}
		}

At this point, if you go to DM the account associated with this bot then you should automatically see a response!

CREATING WELCOME MESSAGE WITH QUICK RESPONSE:

1. Read everything above.
2. Post to https://api.twitter.com/1.1/direct_messages/welcome_messages/new.json
		See: https://dev.twitter.com/rest/direct-messages/quick-replies/options

		Body:
		{
		  "welcome_message" : {
			"message_data": {
				"text": "ULTIMATE SHOWDOWN! WHO ARE YOU VOTING FOR?",
				"quick_reply": {
				  "type": "options",
				  "options": [
					{
					  "label": "🙀Clark🙀",
					  "description": "SNACKSSSSSSSSSSSSS",
					  "metadata": "external_id_1"
					},
					{
					  "label": "💅Lewis💅",
					  "description": "YOL9X",
					  "metadata": "external_id_2"
					},
					{
					  "label": "🏂Honeydew Melon🏂",
					  "description": "anything u can do I can do better",
					  "metadata": "external_id_3"
					}
					]
				}
				}
			}
		}

		Response:
		{
			"welcome_message": {
				"id": "############",
				"created_timestamp": "1498768954113",
				"message_data": {
					"text": "VOTE:",
					"entities": {
						"hashtags": [],
						"symbols": [],
						"user_mentions": [],
						"urls": []
					},
					"quick_reply": {
						"type": "options",
						"options": [
							{
								"label": "Clark",
								"metadata": "external_id_1",
								"description": "SNACKSSSSSSSSSSSSS"
							},
							{
								"label": "Lewis",
								"metadata": "external_id_2",
								"description": "YOL9X"
							},
							{
								"label": "Honeydew Melon",
								"metadata": "external_id_3",
								"description": "Anything u can do I can do better"
							}
						]
					}
				}
			}
		}

3. Delete old welcome message (if applicable).
		See: https://dev.twitter.com/rest/reference/del/direct_messages/welcome_messages/destroy
		
		Note: You must install twurl (unless you can find a workaround but I did not).
		
		Install twurl on Windows:
			http://sgomez.blogspot.com/2015/10/running-twurl-on-windows.html
			Note: do this all as admin
		
			1. install chocolatey: https://chocolatey.org/install#install-with-cmde
		
			2. cmd: choco install ruby
			
			3. cmd: gem install twurl 
			
			4. Authorize twurl.
				twurl authorize -consumer-key {API-KEY} --consumer-secret {API-SECRET}
				
				Go to provided URL. Copy and paste pin into CMD.
			
			5. cmd: twurl -X DELETE /1.1/direct_messages/welcome_messages/destroy.json?id=########
			NOTE: ############ is the returned welcome_message_id from when you created the id.

4. Make new message the welcome message (see above section, #2

DO THIS ALL WITH A LINK:
https://twitter.com/messages/compose?recipient_id=##########&welcome_message_id=#####
		

