# Docker Node Exercise

Follow these steps to build a simple Docker app in Node. Note that Node does not need to be installed on your computer to do this exercise.

## Instructions

1. Navigate to an empty project folder.
2. Make a blank file in it called `docker-compose.yml`.
3. Make an empty folder in it called `app`
3. Make an empty file in the `app` folder called `package.json`
4. Add the following content to the `docker-compose.yml` file:
  * A top-level key called `services`, with a key under that called `api`
  * The `api` service should use the `node` image with the `17-alpine3.12` tag
  * The `api` service should have a volume that maps the `app` folder in the project to the `/app` folder inside the container
  * The `api` service should map port 443 inside the container to port 3000 on the host
  * The `api` service should establish an environment variable named `HOMETOWN` that's set to the city you live in
  * The `api` service should run the command `npm install && npm start` by default
5. Scaffold out the app with `docker-compose run -u $(id -u):$(id -g) api sh -c "cd /app && npm init -y"`
6. Install `express` and `nodemon` in the project with `docker-compose run -u $(id -u):$(id -g) api sh -c "cd /app && npm install express nodemon"`
7. Create the local file `app/index.js` and copy the data below into it.
8. Update the local file `app/package.json` to have a new `start` script under `scripts` with the value `nodemon index.js`
9. Run `docker-compose up --build`. Your API should be live on `localhost:3000`!

## `index.js`

```js
const express = require("express")

const app = express()

app.get("/", (request, response) => {
  response.json({
    message: `Hello, ${process.env.HOMETOWN}!`,
  })
})

app.listen(443, () => console.log("Server is listening on 443"))
```
