# Weyer

Simple web player using Spotify API on Vue

## TODO List

- Create other views
- _REMOVE JUNK CODE_
- Connect with Spotify API
- Fetch data for tracks & albums
- Create user login ?
- ...

## Project setup

In order to use Backend server to receive/update token use `export` command to add URL's. Otherwise it will use https://localhost:8888

#### Note: Used [<img src="https://www.freeiconspng.com/uploads/github-logo-icon-5.png" style="width: 25px; vertical-align:middle;">](https://github.com/Fecony/weyer-nodejs-server) as backend server hosted on Heroku.

```
npm install
export VUE_APP_BASE_URL=[URL TO BACKEND SERVER]

- Compiles and hot-reloads for development -
npm run serve
```

> Or create `.env` file and add:

```
VUE_APP_BASE_URL=[URL TO BACKEND SERVER]
```
