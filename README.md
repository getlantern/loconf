Changes to `desktop-ui.json` affects only Lantern desktop clients. The corresponding sections in `messages.json` are ignored by new desktop clients. All Android related configurations are in `messages.json`.

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

Desktop also support the special "ANY" flag indicating all users reporting any issue at all, as in:

```json
"survey": {
  "ANY-en-US": {
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

*NOTE:*
Version and subscription matching have been added to the desktop UI, but because of backwards compatibility concerns, the implementation is a little hacky and so there are some serious 🐍s an 🐉s.
Version matching only applies to objects whose property already matches the language-location key.
Additionally, because older clients won't understand version matching, if you create a survey with a version constraint, you must set `enabled` to false so that older clients won't attempt to display it 🙁.
Also, because the surveys use object property keys to match on and an object can only have a single key, there's not a straightforward way to have a survey for the same language/region group with different version constraints.
It *is* possible to use a kind of hack as shown in the [desktop-ui-staging.json](./desktop-ui-staging.json) file and have one survey use `en-US` and the other use `-en-US`, but it's obviously hairy and not ideal...

