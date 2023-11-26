# 6. Development setup
Created Tue Nov 7, 2023 at 9:45 AM

- Make sure `node` version >=18 (Tested with 18), and use `npm` only
- Visit React Native official [set-up page](https://reactnative.dev/docs/environment-setup) and do the steps.
- ~~Install [Expo](https://docs.expo.dev/get-started/installation/) on computer: `npm install -g expo`~~ `npx create-expo-app AppName` is enough
- Install Expo on real phone - it's available on [app stores](https://play.google.com/store/apps/details?id=host.exp.exponent&pcampaignid=web_share)

- vscode is fine as an editor. Helpful vscode plugins
	- React Native tools by [Microsoft](https://marketplace.visualstudio.com/items?itemName=msjsdiag.vscode-react-native)
	- React snippets by [EQuimper](https://marketplace.visualstudio.com/items?itemName=EQuimper.react-native-react-redux-snippets-for-es6-es7-version-standard)

## General info
- API levels vs Android version chart
- Expo (especially Expo Go - i.e. device/emulator app) needs Internet by default. But can work [offline](https://stackoverflow.com/questions/50423562/running-expo-in-development-offline) by passing `--offline`