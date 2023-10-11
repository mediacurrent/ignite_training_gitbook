# Create a new D10 theme

### Mediacurrent Theme Generator

The [Mediacurrent theme generator](https://github.com/mediacurrent/theme\_generator\_10) is a scaffolding tool that has evolved with the years to provide a production-ready Drupal 10 theme that is component-based ready out of the box.

## Exercise:  Create a new D10 theme

Follow the instructions below.

1. In your Drupal 10 site, create a new folder for your theme (i.e. `/themes/custom/training_theme`).  Although you can use any name you wish, all exercises in this curriculum use **training\_theme**.
2. In your command line app, change into the newly created directory (**training\_theme**),  type the following command and press **Return**:

```bash
nvm install 16 && node -v > .nvmrc
```

_The command above will install the NVM v16 and create a new hidden file in your project called `.nvmrc` where that version of Node will be declared as the default version for this project._

* Next run this command:&#x20;

```
npm install -g libnpx
```

* Then run the following command:

```bash
npm create yo mc-d10-theme
```

#### Respond to the on-screen prompts as follows:

1. Assign a Human readable name to your theme
2. **IMPORTANT:** When the **What is your theme's machine name?** question comes up, be sure it matches the name of the directory you created above (i.e. `training_theme`).
3. Type a description for your theme
4. Type **Y** and press **Return** when **Should we update the .gitignore to ignore compiled files?** comes up.  This will hide `/dist` from git to avoid having to commit already compiled files.
5. While you can select any editorial components from the list, we recommend starting all of them, especially if you are using the generator for the first time.

{% hint style="warning" %}
**WARNING:** The theme's machine name should always match the directory you created in the first step above (i.e. `training_theme`).
{% endhint %}

* After the theme has been successfully created, run the following commands to launch Storybook:

```bash
npm install
npm run storybook
```

* Click the URL provided in the console output (e.g. [http://localhost:6006/](http://localhost:6006/)), to access Storybook.

## Resources

Project: [https://github.com/mediacurrent/theme\_generator\_10](https://github.com/mediacurrent/theme\_generator\_10/)
