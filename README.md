# Webapp

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 7.3.4.

## Deploy to heroku

In case of a webapp we need to add a server to the project.
- Add `express` and `path` to the dependencies (npm i express path --save)
- Create a `server.js` in the project root similar to the one in this example project
- Replace the `start` script in the `package.json` by `node server.js`
- Add the node and npm versions to the `package.json` (see `engines` in this example)

Create a heroku token:
- `heroku authorizations:create`

Encrypt this token with travis. In the git project dir:
- `travis login --pro`
- `travis encrypt HEROKU_KEY --add deploy.api_key --pro` (this adds the encrypted deploy key to the `.travis.yml`).

Add the following lines to the `.travis.yml`:
```yaml
deploy:
  provider: heroku
  api_key: ...should_already_be_set...
  app: stnimmerwapp
```
