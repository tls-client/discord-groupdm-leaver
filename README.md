# GroupDM-Leaver
1. ```pip install discord.py-self python_dotenv```
1. ```python main.py```
1. `ユーザー名 is online`と表示されたら自動退出が開始します

### すべてのグループDMから脱退する場合

```python
import discord  
import os
from dotenv import load_dotenv
load_dotenv()

client = discord.Client()

TOKEN = os.getenv("TOKEN")

@client.event
async def on_ready():
    print(f"{client.user} is online")
    group_dms = [dm for dm in client.private_channels if isinstance(dm, discord.GroupChannel)]
    left_count = 0
    for dm in group_dms:
            await dm.leave()
            left_count += 1
    print(f"{left_count}件のグループDMからの退出が完了しました")

client.run(TOKEN)
```
### 一部のグループDMから脱退しない場合

```python
DM_IDS = ["12345678", "23456789"]

@client.event
async def on_ready():
    print(f"{client.user} is online")
    group_dms = [dm for dm in client.private_channels if isinstance(dm, discord.GroupChannel)]
    left_count = 0
    for dm in group_dms:
        if str(dm.id) not in DM_IDS:
            await dm.leave()
    print(f"{left_count}件のグループDMからの退出が完了しました")
```
