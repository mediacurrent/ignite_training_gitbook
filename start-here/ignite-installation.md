# Ignite Installation

Once you have configured your local environment for Drupal, it is time to proceed with the installation of the Ignite Demo project. This serves as the foundation for our training program.

### Clone this repository into your DDEV folder (e.g. '\~/ddev/') <a href="#markdown-header-clone-this-repository-into-the-directory-of-your-choice" id="markdown-header-clone-this-repository-into-the-directory-of-your-choice"></a>

* `$ git clone git@bitbucket.org:mediacurrent/ignite_training.git`

### Build and start the local environment <a href="#markdown-header-build-and-start-the-local-environment" id="markdown-header-build-and-start-the-local-environment"></a>

* `$ cd ignite_training`
* `$ ddev start`
* `$ ddev . composer install`
* `$ ./scripts/build.sh`

**This script automates the following steps:**

* Runs composer install
* Installs the project Drupal site

After installing the demo site you should be able to view the site at mctraining.ddev.site.
