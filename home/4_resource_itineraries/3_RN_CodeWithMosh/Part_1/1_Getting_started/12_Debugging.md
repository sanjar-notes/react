# 12. Debugging
Created Tue Nov 7, 2023 at 9:03 AM

## Debug daemon - start and end
- Starting the debug daemon - press Ctrl + M on the emulator, or shake the device (physical). Select 'Debug' from the options.
- The default interface of daemon is the browser.
- Closing - open developer options on device (emulator or physical), and select 'Stop Debugging'.

## Browser
RN has a debugger that can run in the browser

1. Start the debug daemon, by press Ctrl + M on the emulator, or shake the device (physical). Select 'Debug' from the options
2. Metro (`npm start`) terminal will now say that "logs will be displayed elsewhere". And a webpage will open.
3. The webpage opens usually at "localhost:8081". Open the JS console of this page. Logs can now be seen here.

- So console is one thing
- The "Sources" tab also works in the browser, so `debugger;` statements and watch on exceptions can be used.
- The network tab doesn't work, unfortunately

The webpage also shows the daemon connection status.

To end the browser debug session, click 'Stop debugging' from the webpage (localhost:8081).


## Vscode
Install 'react-native-tools' vscode extension. This gives us Vscode debug configs for RN that we can use directly.

To use the debugger:
1. Start the debug daemon, by press Ctrl + M on the emulator, or shake the device (physical). Select 'Debug' from the options
2. Add some breakpoints in the code.
3. Open 'Debug' from vscode Command Palette, select React Native > Attach to packager.
4. If there's no debug config, a file will be created automatically with the config we selected. Just save it.
5. In the Debug sidepanel, click the Play button. The app should now start and get stuck on the breakpoint (this might require some interaction with the app - via emulator/physical device).
6. The Output panel of vscode should now be open. Logs, variables can be tracked, and code can be run.

To end the vscode debug session, click the detach (red plugs) icon in the debug toolbar (beside re-run icon). Control will now be back at the Metro terminal.

## One at a time - browser or editor
- The RN debug daemon can only work with one interface at once - either use the browser, or vscode, but not both. Fix: just detach the unnecessary interface via the browser or vscode detach.