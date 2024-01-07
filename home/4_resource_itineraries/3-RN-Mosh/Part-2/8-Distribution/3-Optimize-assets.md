# 3. Optimize assets
Created Sat Dec 30, 2023 at 1:56 PM

1. Remove image and other assets that can be downloaded at run time. Keep only essential assets
2. Run `npx expo-optimize` command from project root. This needs `npm i -g sharp-cli` to be installed at first though. The command will optimize all assets in the project.