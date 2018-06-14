# Bitbucket Webhook Bridge for Mattermost

This repository is contains a Python Flask application that accepts webhooks from [Bitbucket
Server](https://www.atlassian.com/software/bitbucket/server) and forwards them to the specified
channel in a [Mattermost](https://mattermost.com) server via an incoming webhook. The bridge application
supports a number of usage scenarios including:

* One Bitbucket repository to one Mattermost incoming webhook (one to one);
* Many Bitbucket repositories to many Mattermost incoming webhooks (many to many) and;
* Many Bitbucket repositories to one Mattermost incoming webhook (many to one).

Information on setting up for the different usage scenarios can be found below.
 
 **Import Notes**:
 * This application has only been tested with Bitbucket Server 5.10.1. 
 * This application is an example of how to bridge Bitbucket webhooks to Mattermost and is not 
 meant to be used in a production environment.
 
 # Supported Bitbucket Events
 
 The following events are supported and **tested** in the current version of this application:
 
* Pull request comment added
* Pull request comment deleted
* Pull request comment edited
* Pull request declined
* Pull request deleted
* Pull request merged
* Pull request modified
* Pull request opened
* Repository commit comment added
* Repository commit comment deleted
* Repository commit comment edited
* Repository forked
* Repository refs updated

## Setup the Flask Application

The following steps

1. Log into the machine that will host the Python Flask application;
2. Clone this repository to your machine: `git clone https://github.com/cvitter/mattermost-bitbucket-bridge.git`;
3. Make a copy of `config.sample`: `cp config.sample config.json`
4. Edit `config.json` to update the following fields as needed:
   * Application host address and port (generally debug should be left set to `false`;
   * Mattermost server_url and the user name or icon to override the webhook with if desired;
   * And the base url of your Bitbucket server.
5. Run the Flask application - there are a number of ways to run the application but I use the following command that runs the application headlessly and captures output into a log file for troubleshooting:

```
sudo python bitbucket.py >> bitbucket.log 2>&1 &
```

# Configure Mattermost

To use this application you will need to create one or more `Incoming Webhooks` in Mattermost. These incoming webhooks will be the endpoints that the application will post the events received from Bitbucket. Webhooks are created by navigating to `Integrations` in the `Main Menu`, clicking on ` Incoming Webhooks`, and clicking on `Add Incoming Webhook`. After creating the incoming webhook you will need to copy the webhook's code at the end of its URL which will be needed when configuring the webhook in Bitbucket.

**Note**: You can have all Bitbucket events post to a single webhook or, or setup incoming webhooks in Mattermost for each Bitbucket repository.

# Configure Bitbucket

Within Bitbucket webhooks are configured and managed at the individual repository level. From within a repository click on the `Repository Settings` icon (cog) in the left hand side bar and then click on Webhooks under repository settings. To create a new webhook click on the `Create webhook` button. In the `Create webhook` form fill in the new webhook's `Name` and `URL`. The URL will look like:

```
http://flask-application-url:port/hooks/[hookcode]
```
**Note**: The hook code is the unique hook identifier generated by Mattermost and is found at the end of your Mattermost's incoming webhook URL, ex: `https://mymattermostserver.com/hooks/5iz1k8j8rewrjyu3anbw4u66qe`.

Then select the `Repository` and `Pull request` events you want to be notified about and click on `Create` to create the webhook.


# Make this Project Better (Questions, Feedback, Pull Requests Etc.)

**Help!** If you like this project and want to make it even more awesome please contribute your ideas,
code, etc.

If you have any questions, feedback, suggestions, etc. please submit them via issues here: https://github.com/cvitter/mattermost-bitbucket-bridge/issues

If you find errors please feel to submit pull requests. Any help in improving this resource is appreciated!

# License
The content in this repository is Open Source material released under the MIT License. Please see the [LICENSE](LICENSE) file for full license details.

# Disclaimer

The code in this repository is not sponsored or supported by Mattermost, Inc.

# Authors
* Author: [Craig Vitter](https://github.com/cvitter)

# Contributors 
Please submit Issues and/or Pull Requests.
