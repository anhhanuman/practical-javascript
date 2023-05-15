```js
(async () => {
    try {
        const data = escapeUnicode(replaceAllMentions(replacer(inputSlackJson)));
        if (!data) throw 'There is nothing to send! Please check your slack_json parameter!'
        const result = await sendMessage(data);

        if (result !== 'ok') {
            if (result === 'invalid_payload') {
                core.setFailed('Could not send notification with invalid payload: ' + data);
            } else {
                core.setFailed('Could not send notification: ' + result);
            }
        }
    } catch (error) {
        core.setFailed(error.message);
    }
})();

```
