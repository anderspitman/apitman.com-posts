Somehow I never heard about [json.tool](https://docs.python.org/3/library/json.html#module-json.tool)
until just now. It's built in to Python and provides a simple way to pretty-print JSON on the CLI:

```bash
echo '{"og": "hi there"}' | python -m json.tool
```

```
{
    "og": "hi there"
}
```

This is a nice alternative if you have Python installed and don't want to take the time to install
[jq](https://github.com/stedolan/jq).