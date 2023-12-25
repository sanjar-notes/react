# 5. Environment variables
Created Mon Dec 25, 2023 at 9:06 PM

Video - https://youtube.com/shorts/r92aHr752Bg?si=NhM-JVkqMONeiK2W

## Vite
Vite injects the envs into `import.meta.env`.
FYI: `process.env` is just not available (error).

- Set envs. Two ways:
	- Add .env file. Make sure all key names have the `VITE_` prefix. Example: `VITE_PORT`
	- Add inline - `VITE_PORT=4000 npm run build`. Multiple are supported too `VITE_PORT=4000 VITE_PORT2=4001 npm run build`.  Make sure all key names have the `VITE_` prefix.
- Get envs - `import.meta.env.VITE_PORT`
- Works in dev, build
Confirmed works for both cases.
## Create-react-app
CRA simply injects the envs passed into the `process.env` object

- Set envs. Two ways:
	- Add a .env file. Make sure all key names have the `REACT_APP_` prefix. Example: `REACT_APP_PORT`
	- Add inline - `REACT_APP_PORT=4000 npm run build`. Multiple are supported too `REACT_APP_PORT=4000 REACT_APP_PORT2=4001 npm run build`
- Get envs - `process.env.SOME_ENV_KEY`. Example: `process.env.REACT_APP_PORT`

- Works in dev, build
- since React is an SPA library, the build process happens just once, and the env variables get hardcoded into the bundle. So, if the env file changes, you'll need to rebuild.
Confirmed works for both cases. (react-scripts 5.0.1)