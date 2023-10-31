Given the recent changes in Twitter and its API access a new method for accessing Twitter anonymously was devised. This method involves using temporary guest accounts created when going through the onboarding process with the Android app. This guide will teach you how to get basic functionality on a fresh deployment of Nitter. All of the dependency requirements can be found in the readme for this [repository] (https://github.com/zedeus/nitter), and this guide will not diverge far from the normal deployment procedure.

### [Dependencies](https://github.com/zedeus/nitter#dependencies)

    libpcre
    libsass
    redis


### Installation Guide

```bash
useradd -m nitter
su nitter
cd /opt/
git clone https://github.com/zedeus/nitter
cd /opt/nitter
git checkout guest_accounts
nimble build -d:release
nimble scss
nimble md
cp nitter.example.conf nitter.conf
```

From this point edit your nitter.conf to the configuration that you want.

### Guest Accounts
After this is completed we will be creating a guest_account using the following shell script:

```bash
#!/bin/bash

guest_token=$(curl -s -XPOST https://api.twitter.com/1.1/guest/activate.json -H 'Authorization: Bearer AAAAAAAAAAAAAAAAAAAAAFXzAwAAAAAAMHCxpeSDG1gLNLghVe8d74hl6k4%3DRUMF4xAQLsbeBhTSRrCiQpJtxoGWeyHrDb5te2jpGskWDFW82F' | jq -r '.guest_token')

flow_token=$(curl -s -XPOST 'https://api.twitter.com/1.1/onboarding/task.json?flow_name=welcome' \
          -H 'Authorization: Bearer AAAAAAAAAAAAAAAAAAAAAFXzAwAAAAAAMHCxpeSDG1gLNLghVe8d74hl6k4%3DRUMF4xAQLsbeBhTSRrCiQpJtxoGWeyHrDb5te2jpGskWDFW82F' \
          -H 'Content-Type: application/json' \
          -H "User-Agent: TwitterAndroid/10.10.0" \
          -H "X-Guest-Token: ${guest_token}" \
          -d '{"flow_token":null,"input_flow_data":{"flow_context":{"start_location":{"location":"splash_screen"}}}}' | jq -r .flow_token)

curl -s -XPOST 'https://api.twitter.com/1.1/onboarding/task.json' \
          -H 'Authorization: Bearer AAAAAAAAAAAAAAAAAAAAAFXzAwAAAAAAMHCxpeSDG1gLNLghVe8d74hl6k4%3DRUMF4xAQLsbeBhTSRrCiQpJtxoGWeyHrDb5te2jpGskWDFW82F' \
          -H 'Content-Type: application/json' \
          -H "User-Agent: TwitterAndroid/10.10.0" \
          -H "X-Guest-Token: ${guest_token}" \
          -d "{\"flow_token\":\"${flow_token}\",\"subtask_inputs\":[{\"open_link\":{\"link\":\"next_link\"},\"subtask_id\":\"NextTaskOpenLink\"}]}" | jq -c -r '.subtasks[0]|if(.open_account) then {oauth_token: .open_account.oauth_token, oauth_token_secret: .open_account.oauth_token_secret} else empty end'
```

When this shell script is run it will output JSON that looks similar to this:
```json
{"oauth_token":"1719213587296620928-BsXY2RIJEw7fjxoNwbBemgjJhueK0m","oauth_token_secret":"N0WB0xhL4ng6WTN44aZO82SUJjz7ssI3hHez2CUhTiYqy"}
```

If the script outputs nothing, it's possible you're running it from an IP that already got an account within the last 24 hours, or something else may be broken. Remove `| jq -c ...` from the last command, and `-s` from the `curl` commands to get more info for troubleshooting.

If the file guest_accounts.jsonl does not exist, create it containing just the script output. JSONL is a line-based format with one JSON object (like the output above) per line, without needing to wrap everything in an array. If you get more tokens, simply add then to the file on separate lines.

Save the file and launch Nitter. Each guest account is only valid for 30 days and gives approximately 500 API requests every 15 minutes before it is rate limited. Twitter restricts each IP to creating a single guest account per day, thus generating guest accounts in bulk is a tedious affair beyond the scope of this guide.  