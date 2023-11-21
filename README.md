# norbit-homework-client

The frontend part of the solution for the Web developer homework for Norbit Hungary.

The backend part can be found [here](https://github.com/hawser86/norbit-homework-server).

## Prerequisites

In order to run the application locally install
- [nvm](https://github.com/nvm-sh/nvm)

## Setup

Execute the following commands

```shell
# set proper node version
nvm use

# install dependencies
npm ci
```

## Run the app
Start the [backend](https://github.com/hawser86/norbit-homework-server) first.

Start the client
```shell
npm run dev
```

Open the http://localhost:5173/ url in you browser (on multiple tabs).

## Known issues, improvement ideas
- there are some hard coed strings, which should be coming from config / environment variable
  - backend URL
  - initial state of the map (center position, zoom level)
- there is no error handling
- there are no tests
- application state should be stored using a state management solution
  - now the [App](./src/App.vue) component does many things, which should be handled by e.g. Vuex or Pinia
- UX could definitely be better :)
- with a deeper knowledge of OpenLayers I believe the [MapContainer](./src/components/MapContainer.vue) can be simplified
  and probably optimised
