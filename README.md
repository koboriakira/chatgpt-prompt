# ChatGPT Prompt

## Usage

```shell
OPENAI_API_KEY=sk-*******
YAML_FILENAME=name-branch.yaml
USER_INPUT="#1 タスク作成機能"

# OpenAI APIが読み取れる形に変換したうえでcurlを実行
OPENAI_RESPONSE=$(sed "s/USER_INPUT/$USER_INPUT/" $YAML_FILENAME | \
  yq eval -o json | curl https://api.openai.com/v1/chat/completions \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d @- | jq -r '.choices[0].message.content')

# レスポンスがJSONである場合は、さらにjqコマンドで取得できる
echo $OPENAI_RESPONSE | jq -r '.branch_name'
```
