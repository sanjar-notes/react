# 8. 1 Navigate on notification
Created Sat Dec 30, 2023 at 1:56 PM

This not possible at the root level (and we can't keep the notification listener in a screen since that could be unmounted). useNavigation is also not possible since that's for leaf component not top level components.

The fix is to create a "service" file - which is just a fancy name for a simple trick. 
We create a Recat ref in a JS file and export it. Yes a ref can be created without a component. Then we set this ref as the ref prop for top most react Navigation provider. See PKB react node. Already noted.

Now, we can import and read/write to the exported thing's `.current` property.
And can navigate from anywhere.

In our case when the listener detects a notification, it can check if it contains some navigation param, and navigate accordingly. And since notifications can have payload, even parameterized navigation is possible. Wow.

Btw. With local navigation, this can absolve the problem of opening a large app quicker.