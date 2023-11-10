# 7. First app
Created Tue Nov 7, 2023 at 9:54 AM

- First (optional) - set up wireless debugging on physical device (Android)
	```sh
	adb pair 192.168.0.10x
	# enter code
	adb connect 192.168.0.10x
	```
	 Needs to be done only once.

- Creating the app (code)
	```sh
	npx create DoneWithIt
	cd DoneWithIt
	npm run android # automatically starts the first simulator in AVD (in standalone mode)
	```