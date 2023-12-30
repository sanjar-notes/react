# 12. Sending images
Created Sat Dec 30, 2023 at 1:55 PM

## Payload creation
- Axios automatically sets proper "Content-Type" (multipart/form-data) when its given a FormData object. So headers are not an issue.
- One thing is important - when sending files, or a mixture of files and normal data, make sure everything is inside FormData, and that's given as is as payload to axios. Don't spread it, or do anything else with it. It's an inflexible/problematic thing. Also, one has to sequentially add keys to FormData via `.append`, fine, just do a `Object.entries.forEach` for the normal data.
- Since we're dealing with images, which is a file, we'll use FormData.

```js
const payload = new FormData();

payload.append('name', 'Sanjar');
payload.append('age', 25);

imgArray.forEach((img, index) => {
  payload.append('images', {
    name: 'img' + idx, // this is enough to indcate that `images` is an array
    type: `image/jpeg`,
    uri: img // as returned by picker
  })
});

axios.post('/endpoint-here', payload, { params: {} });
```