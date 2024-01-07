# 5. Error reporting
Created Sat Dec 30, 2023 at 1:57 PM

Client side apps (especially) mobile are used in the fields.
And it's usually hard for you or the user to debug/report.

Therefore, using a error reporting Sentry is helpful.

These platforms usually have an SDK that can be added to our app, and we can log errors with our license key. We can then see errors and analytics for runtime issues as experienced by users.

This way, we get to know errors remotely. This includes the device id, our app version, platform and other information labelled with each error.

Optionally, during install an SDK can be configured to upload "source maps" too, so we on dev side can debug the bug files with our "real" source code.

Make sure you create a wrapper around the SDK and use that in the app code. Makes migration easy. Example:
```js
import Bugsnag from '@bugsnag/expo';

const log = (error) => Bugsnag.notify(error);
const start = () => Bugsnag.start();

export default { log, start };
```

Usage wise, we need to initialize this SDK once. Usually done in App.js and outside the component. We can now use the log wrapper in our try catches.