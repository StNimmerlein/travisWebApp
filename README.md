# Webapp

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 7.3.4.

## Deploy to own server

Create SSH Keys and add them to the authorized_keys of the server. Next we need to encrypt the private key with travis and commit the encrypted key.
In the git repo directory:
- `travis login --pro`
- `travis encrypt-file path/to/private/ssh/key --add --pro` (this will add a `before_install` section in the `.travis.yml` and a `.enc` file).
- Add the following lines to the `before_install` script:
  ```yaml
  - eval "$(ssh-agent -s)"
  - chmod 400 ./deploy-key
  - ssh-add ./deploy-key
  ```
- To disable strict host key checking for your server add this line as well:
  ```yaml
  echo -e "Host YOUR_SERVER\n\tStrictHostKeyChecking no\n" >> ~/.ssh/config
  ```
- Commit the changes (including the `.enc` file).

Now you can ssh to your server without having to enter a password and do everything you want.

You can do the deployment in an `after_success` step as done here in the example.

**Never commit the unencrypted private ssh key!**
