# 12. Debug
Created Tue Nov 7, 2023 at 9:03 AM

## Browser
RN has a debugger that can run in the browser

To start the debugger, press Ctrl + M on the simulator, or shave the device (if debugging on real physical device). A RN daemon should be running now, and a tab should open on the browser.

## Vscode
Go to `App.js` and start the debugger.
- May need to create a config, verify it's like so:
	```json
	FIXME
	```
- May need to set the port to be the same as RN debugger daemon

## One at a time - browser or editor
The RN debug daemon can only work with one interface at once - so you can either use the browser, or vscode, but not both.