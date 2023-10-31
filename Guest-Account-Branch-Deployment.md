Given the recent changes in Twitter and its API access a new method for accessing Twitter anonymously was devised, this method involves using temporary guest accounts created when going through the onboarding process with the Android app. This guide will teach you how to get basic functionality on a fresh deploy of Nitter, all of the dependency requirements can be found in the readme for the [repository] (https://github.com/zedeus/nitter) also this guide will not diverge far from the normal deployment routine.

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

From this point edit your nitter.conf to the configuration that you want. After this is completed we will be creating a guest_account using a [shell script](https://gist.github.com/Salastil/f66a098d408c8c74adcf2210d4d33435)

When this shell script is run it will output json that looks similar to this:
```json
[
  {
    "user": {
      "id": 1719004241518317568,
      "id_str": "1719004241518317568",
      "name": "Open App User",
      "screen_name": "_LO_1030qDMfQYH",
      "user_type": "Soft"
    },
    "next_link": {
      "link_type": "subtask",
      "link_id": "next_link",
      "subtask_id": "OpenAppFlowStartAccountSetupOpenLink"
    },
    "oauth_token": "1719004241518317568-viSa1DHHnW1xLN45Cl59IfHp4CX6oq",
    "oauth_token_secret": "N5aVkXlqO3nHarwaNtbM6h1oqRglyK8kF7GST53NFI3hq",
    "attribution_event": "signup"
  }
]
```
The two keys we need are oauth_token and oauth_token_secret. 

If the file guest_accounts.jsonl does not exist, create it. Within the file place the two keys in the following format

```jsonl{"oauth_token":"1719004241518317568-viSa1DHHnW1xLN45Cl59IfHp4CX6oq","oauth_token_secret":"N5aVkXlqO3nHarwaNtbM6h1oqRglyK8kF7GST53NFI3hq"}```

Save the file and launch Nitter. Each guest account is only valid for 30 days and gives approximately 500 API requests every 15 minutes before it is rate limited. Twitter restricts each IP to creating a single guest account per day, thus generating guest accounts in bulk is a tedious affair beyond the scope of this instruction set. 