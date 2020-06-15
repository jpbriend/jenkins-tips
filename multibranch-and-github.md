## Jenkins Multibranch jobs and GitHub

In order to create a Multibranch job with Github webhooks and to use a Personal Access Token in order to avoid hitting the API rate limit, here are the mandatory steps:
* Create a [Personal Access Token](https://github.com/settings/tokens) in Github.
* Create a first Jenkins Credential which will be used to interact with Github (checkout, etc...) except creating Webhooks:
  * **Kind**: `Username with Password`
  * **Username**: the username of the Github you want to use
  * **Password**: the Personal Access Token you have just created
 
* Create a second Jenkins Credential which will be used to register Github Webhooks automatically when creating the Multibranch job:
  * **Kind**: `Secret text`
  * **Secret**: the Personal Access Token you have just created

* Declare a GitHub Server in your Jenkins Master:
  * Go to **Manage Jenkins** - **Configure System**
  * Scroll down to section **GitHub** / **GitHub Servers**
  * Add a GitHub Server. If you are using `github.com`, just use the provided value (`https://api.github.com`)
  * Add a name
  * Select the 2nd Credential we created in the previous step (it should show in the dropdown list)
  * **Save** the configuration

* Create a Multibranch job
  * **Add source** `GitHub` 
  * **Credentials**: Select the 1st Credential created in the first step (it should appear in the dropdown list)
  * Complete the creation of the multibranch job, it's pretty straightforward.

Once created, the Multibranch job will scan the GitHub repository and create a WebHook. You can check it has been created at [this URL](https://github.com/cloudbees-guru/my_project/settings/hooks).
