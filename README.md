To verify the JSON on new configurations, please use:

https://jsonlint.com/

We currently can display messages (aka "surveys" but they're really more general than that) to users on desktop according to issue types they've reported, if we like. The odd thing about that is it relies on the translated issue type for the user's locale. Those translated strings are at:

https://github.com/getlantern/lantern-desktop-ui/blob/master/locale/en-US.json#L206
https://github.com/getlantern/lantern-desktop-ui/blob/master/locale/zh-CN.json#L138
https://github.com/getlantern/lantern-desktop-ui/blob/master/locale/fa_IR.json#L205

So, for example, a key for a message for users reporting being blocked running in english in the US would be:

```json
"survey": {
  "Cannot access blocked sites-en-US": {
    "enabled": true,
    "probability": 1.0,
    "campaign": "890318",
    "url": "https://www.google.com",
    "message": "Check out the beta group for US-en!!!",
    "thanks": "",
    "button": "Go Beta!"
  },
}
```
