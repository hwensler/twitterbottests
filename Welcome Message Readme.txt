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
