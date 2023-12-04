Hand written notes done. See [OneNote](https://onedrive.live.com/redir?resid=1AFE2D221CFD3E54%21137&page=Edit&wd=target%287-forms.one%7C3df3c2cf-33e8-6746-a1f1-2d6d057a4b01%2F%29&wdorigin=717)

## Formik and Yup
- Formik is available for RN
- Yup can be used for validation. Works since it's just a JS validation library


## Error message
Instead of rendering an error message after every form component, i.e. coding the error message in the feature, just add an error UI in every input element. so only `error` prop needs to be set, in addition to `value` and `handleChange`.

## Touched state
When making a form, in addition to 'value', 'error' and 'handleChange'. Keep a 'touched' boolean state too (initially false).

This avoids the form showing errors when it loads first, which is an annoying feeling.

When the form is initialized, don't show errors until the user has touched the input element once, i.e. touched is true. Of course, touched stays true ones it becomes true.

To set it, use `onBlur => setTouched(true)`