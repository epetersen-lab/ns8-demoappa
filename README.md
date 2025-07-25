# ns8-demoappa

This is a template module for [NethServer 8](https://github.com/NethServer/ns8-core).
To start a new module from it:

1. Click on [Use this template](https://github.com/NethServer/ns8-demoappa/generate).
   Name your repo with `ns8-` prefix (e.g. `ns8-mymodule`). 
   Do not end your module name with a number, like ~~`ns8-baaad2`~~!

1. Clone the repository, enter the cloned directory and
   [configure your GIT identity](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup#_your_identity)

1. Rename some references inside the repo:
   ```
   modulename=$(basename $(pwd) | sed 's/^ns8-//')
   git mv imageroot/systemd/user/demoappa.service imageroot/systemd/user/${modulename}.service
   git mv tests/demoappa.robot tests/${modulename}.robot
   sed -i "s/demoappa/${modulename}/g" $(find .github/ * -type f)
   git commit -a -m "Repository initialization"
   ```

1. Edit this `README.md` file, by replacing this section with your module
   description

1. Adjust `.github/workflows` to your needs. `clean-registry.yml` might
   need the proper list of image names to work correctly. Unused workflows
   can be disabled from the GitHub Actions interface.

1. Commit and push your local changes

## Install

Instantiate the module with:

    add-module ghcr.io/epetersen-lab/demoappa:latest 1

The output of the command will return the instance name.
Output example:

    {"module_id": "demoappa1", "image_name": "demoappa", "image_url": "ghcr.io/epetersen-lab/demoappa:latest"}

## Configure

Let's assume that the demoappa instance is named `demoappa1`.

Launch `configure-module`, by setting the following parameters:
- `<MODULE_PARAM1_NAME>`: <MODULE_PARAM1_DESCRIPTION>
- `<MODULE_PARAM2_NAME>`: <MODULE_PARAM2_DESCRIPTION>
- ...

Example:

    api-cli run module/demoappa1/configure-module --data '{}'

The above command will:
- start and configure the demoappa instance
- (describe configuration process)
- ...

Send a test HTTP request to the demoappa backend service:

    curl http://127.0.0.1/demoappa/

To setup the translation process:

- add [GitHub Weblate app](https://docs.weblate.org/en/latest/admin/continuous.html#github-setup) to your repository
- add your repository to [hosted.weblate.org]((https://hosted.weblate.org) or ask a NethServer developer to add it to ns8 Weblate project
