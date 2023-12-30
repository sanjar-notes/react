# 14. Progress
Created Sat Dec 30, 2023 at 1:55 PM

The axios request config argument has a `onUploadProgress` key, which runs multiple times until the upload finishes.

We can use `useState` and update it, indicating the realtime progress in the UI!

```js
const [uploadedRatio, setUploadedRatio] = useState(0);

return axiosClient.post(endpoint, data, {
  onUploadProgress: (progress) => {
    setUploadedRatio(progress.loaded / progress.total);
    console.log(progress.loaded / progress.total);
  }
})
```