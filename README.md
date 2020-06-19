# Corona-School Development Environment

A zoo of Docker containers that contains all backends and frontends,
as well as a Docker Compose config which additionally sets up redis and postgres.

To set up, clone this repository (`dev-env`) into the same folder as all the other repositories (`backend`, `backend-screening`, `web-screening-app`, `web-screening-admin`). Then install docker and run `docker-compose up` in this folder. To rebuild, use `docker-compose build`, then run up again. Don't worry, the first run will take quite a while, but further ones will be significantly faster (as most steps can be cached).

You might want to disable CORS in your browser to make the webapps work.

This will reveal the following ports on your host:
- 4001 - The Screening Admin
- 4002 - The Screening App
- 3000 - The Backend
- 3001 - The Screening Backend
- 6379 - Redis 
- 5432 - PostgreSQL (username: dev_corona_school password: test)

There are the following test accounts (email / password):
- Screener: maxi-screening@example.org / screener
- Student: leon-jackson@t-online.de / authtokenS1
- Student: mel-98@gmail.com / authtokenS2
- Pupil: max@gamil.com / authtokenP1
- Pupil: müller@hotmail.de / authtokenP2