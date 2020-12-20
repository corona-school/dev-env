# Corona-School Development Environment

A zoo of Docker containers that contains all backends and frontends,
as well as a Docker Compose config which additionally sets up redis and postgres.

# Possible Setups

## Local Web-User-App using Heroku's DEV deployment

Usually when working on the frontend it is sufficient to run against the development backend, which safes the work of setting up the backend locally. To do so:

1. Install [NodeJS](https://nodejs.org) 
2. Install Git (You can use [Github Desktop](https://desktop.github.com), cli only works too for sure)
3. Install [Yarn](https://yarnpkg.com/getting-started/install)
4. Clone the [Frontend](https://github.com/corona-school/web-user-app) via Git (best into the folder ./corona-school/web-user-app). 
5. Checkout a feature branch (or create one)
6. Run `yarn install`
7. Create a file named `.env` in the web-user-app folder with the following content:

```env
PORT=3000
REACT_APP_BACKEND_URL="https://corona-school-backend-dev.herokuapp.com/api"
```

8. Use `npm run dev` to start the frontend development server. To login into the frontend see [Testaccounts](#testaccounts)

## Local Web-User-App with custom Heroku Deployment

This variant is pretty useful for small backend changes. 

1. Clone the backend (into corona-school/backend), checkout a branch and make your changes
2. [Create a Pull Request](https://github.com/corona-school/backend/pulls) (possibly also a "Draft")
3. The branch will automatically be deployed to Heroku, and a Link will appear in the PR.
4. Change the `.env` file of the frontend to point to the backend in the PR.
5. Restart the frontend with `npm run dev`

## Local Web-User-App and Backend

This variant is useful for larger changes to the backend.

1. Clone the frontend, backend and the dev-env (into ./corona-school/dev-env)
2. Install Docker and docker-compose
3. Run `docker-compose up web-user-app` in the dev env.

Alternatively one can also only start the backend in the container (`docker-compose up -d backend`), and let the local web-user-app run on it (adapt the `.env` to point to `localhost:5000`). 

# Setting up the Docker Environment

To set up, clone this repository (`dev-env`) into the same folder as all the other repositories (`backend`, `backend-screening`, `web-screening-app`, `web-screening-admin`). Copy the .dockerignore file into the parent directory `cp /root/dev-env/.dockerignore /root/.dockerignore`. Then install docker and run `docker-compose up` in this folder. To rebuild, use `docker-compose build`, then run up again. Don't worry, the first run will take quite a while, but further ones will be significantly faster (as most steps can be cached).

You can also only build / start parts of the landscape e.g. `docker-compose build backend && docker-compose up web-user-app` to rebuild the backend and start the user frontend on top of it.

You might want to disable CORS in your browser to make the webapps work.

This will reveal the following ports on your host:
- 3000 - The Web User App 
- 3000 - The Screening Admin (yeah, these two are on the same port unfortunately. Only run one of them at the same time)
- 3002 - The Screening App
- 5000 - The Backend
- 3001 - The Screening Backend
- 6379 - Redis 
- 5432 - PostgreSQL (username: dev_corona_school password: test)

# Testaccounts

There are the following test accounts (email / password):
- Screener: maxi-screening@example.org / screener
- Student: leon-jackson@t-online.de / authtokenS1
- Student: mel-98@gmail.com / authtokenS2
- Pupil: max@gamil.com / authtokenP1
- Pupil: müller@hotmail.de / authtokenP2

To log in into the user section use http://localhost:3000/login?token=[user password here]

