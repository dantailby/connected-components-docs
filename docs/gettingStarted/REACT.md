# Getting started with React

This guide covers how to get started with Connected Components for React and React Native components.

## 1. Prepare configuration file

The first thing we'll do is to create a JSON configuration file in our repository that maps components in our codebase to the components in Zeplin.

You can either prepare the configuration file:

- Manually
- Use [Zeplin Visual Studio Code extension](https://zpl.io/vscode-extension) _(Recommended)_

In this guide, we'll prepare the file manually, while also mentioning how you can use the extension to simplify all of the steps.

### Create configuration file

We recommend creating your Zeplin configuration file under the `.zeplin` folder in your repository, so let's create that folder first. Within the folder, also create a file called `components.json` and paste the JSON below:

```json
{
    "projects": [],
    "styleguides": [],
    "components": []
}
```

If you use the Visual Studio Code extension, it should prompt you to create the configuration file. You can also use the “Create Zeplin Configuration File” command by pressing “Command/Ctrl + Shift + P”. After creating the configuration file, make sure to click the “Login” link on top of the file to authenticate with your Zeplin account.

In a bit, we'll start filling out the configuration file:

- `projects` and `styleguides` keys are the identifiers of projects and styleguides we'll use components from.
- `components` are the React component files in our codebase.

### Add projects or styleguides

Now, let's add Zeplin projects or styleguides to the configuration file. If you're using [Global Styleguides](https://blog.zeplin.io/announcing-global-styleguides-connecting-design-systems-to-engineering-65ad22bd0076), adding your styleguide(s) will be enough. If instead your components are under projects, you can add all your projects as well. In this example, we'll only add one styleguide.

To add projects or styleguides, we need their identifiers. If you're not using the Visual Studio Code extension, the easiest way to find the identifier of a Zeplin project or a styleguide is to open them in Zeplin's [Web app](https://app.zeplin.io). Look for the URL in the address bar, which should look like so: `https://app.zeplin.io/styleguide/5cd486b18a64c1414be004fb`. The identifier after `styleguide/` (or `project/`) is the identifier we're looking for.

If you're using the Visual Studio Code extension, simply click “Add styleguide” or “Add project” and you'll be presented with a list.

After adding projects or styleguides to our configuration file, it should look like so:

```json
{
    "projects": [],
    "styleguides": [
        "5cd486b18a64c1414be004fb"
    ],
    "components": []
}
```

☝️ _If you have a styleguide tree and want to connect to all the components in the tree, adding a child styleguide to the configuration should be enough._

### Add component from codebase

Adding a component from your codebase to the configuration file is pretty straightforward—we'll add an object to the `components` list.

In this example, we'll go with a `Button.jsx` file under `src/components`. Pick a reusable React component file from your codebase and let's update our configuration file to look like so:

```json
{
    "projects": [],
    "styleguides": [
        "5cd486b18a64c1414be004fb"
    ],
    "components": [
        {
            "path": "src/components/Button.jsx",
            "zeplinNames": []
        }
    ]
}
```

If you're using the Visual Studio Code extension, click the “Add component” link which will list all the files in your repository. Pick the one you want and your configuration file should look like above.

Next up, we'll populate the `zeplinNames` key.

### Connect to component from Zeplin

Now it's time to connect the React component we just added, to a component in Zeplin. We'll do that by adding the name of the component to the `zeplinNames` list.

Let's open the styleguide (or the project) we added and copy the name of the component in Zeplin. In our example, our component's name is “Controls / Button / Primary”. Here's how it looks like in Zeplin:

<img src="../../img/zeplinComponents.png" alt="Components in Zeplin" width="800" />

Let's add this name to the `zeplinNames` list:

```json
{
    "projects": [],
    "styleguides": [
        "5cd486b18a64c1414be004fb"
    ],
    "components": [
        {
            "path": "src/components/Button.jsx",
            "zeplinNames": [
                "Controls / Button / Primary"
            ]
        }
    ]
}
```

Notice that in the screenshot above, we have two more states of the same button. It's possible connect a component in our codebase to multiple components in Zeplin—let's do that:

```json
{
…
            "zeplinNames": [
                "Controls / Button / Primary",
                "Controls / Button / Primary, Hover",
                "Controls / Button / Primary, Pressed"
            ]
…
}
```

If you're using the Visual Studio Code extension, you can simply click “Connect to Zeplin component” and search for a component in Zeplin, directly within Visual Studio Code.

**Congratulations, we just connected our first component!** 🎉

Next up, we'll install and use Zeplin's CLI tool so that these connected components are visible in Zeplin to our team.

## 2. Install Zeplin CLI

Zeplin CLI runs in your terminal and communicates the configuration file with Zeplin.

Let's start by installing it. Zeplin CLI runs on Node.js, if you don't have it installed already, see [Node.js website](https://nodejs.org/en/).

To install Zeplin CLI from npm, run the following command on your Terminal/Command Prompt:

```sh
npm install -g @zeplin/cli
```

Alternatively, if you're using npm in your project, you can add `@zeplin/cli` as a `devDependency`.

## 3. Install CLI React plugin

Zeplin CLI uses plugins to generate documentation, snippets and links from components—check out our [list of plugins](/README.md#Plugins).

Since we're using React, we'll install the official React plugin from npm, by running the following command:

```sh
npm install -g @zeplin/cli-connect-react-plugin
```

Now, we'll update our configuration file to use the plugin. We can do that by adding it under the `plugins` list, like so:

```json
{
    "plugins": [
        {
            "name": "@zeplin/cli-connect-react-plugin"
        }
    ],
    "projects": [],
    "styleguides": [
        "5cd486b18a64c1414be004fb"
    ],
    "components": [
        {
            "path": "src/components/Button.jsx",
            "zeplinNames": [
                "Controls / Button / Primary",
                "Controls / Button / Primary, Hover",
                "Controls / Button / Primary, Pressed"
            ]
        }
    ]
}
```

Next up, we'll run the CLI tool!

## 4. Run Zeplin CLI

It's time! Let's **run the CLI tool and see Connected Components in action** within Zeplin. 🎉

Run the following command—if it's your first time, you'll need to login to Zeplin first:

```sh
zeplin connect
```

Now head back to Zeplin and click on one of the components you connected. You should see an output similar to this:

<img src="../../img/zeplinConnectedComponent-react.png" alt="Connected component in Zeplin" width="600" />

For further information on how components are analyzed by the React plugin, check out the [repository](https://github.com/zeplin/cli-connect-react-plugin).

☝️ _If you want to see the output locally in Zeplin before you publish it to your team, check out our guide on [testing your changes locally](TEST_LOCALLY.md)._

## 5. Add links _(Optional)_

Connected Components also lets you add links to various sources like your Storybook, repository, wiki and so on. In the screenshot above, notice that we have links to GitHub and Storybook.

To add links to your components, check out these guides:

- [Adding Storybook links](../link/STORYBOOK.md)
- [Adding Styleguidist links](../link/STYLEGUIDIST.md)
- [Adding repository links](../link/REPOSITORY.md), e.g. GitHub, GitLab, Bitbucket
- [Adding custom links](../link/CUSTOM.md), e.g. internal Design System wiki

## 6. Connect more components

Now that we connected our very first component, you can go ahead and connect more! Check out the section [Add component from codebase](#add-component-from-codebase) if you need any help.

Hope this getting started guide was helpful, reach out to us at [support@zeplin.io](mailto:support@zeplin.io) if you have any questions or feedback.

For further details on how to customize the configuration file, check out the [Configuration file documentation](/CONFIGURATION_FILE.md).

# Troubleshooting

If you run into any issues while running the `zeplin connect` command, make sure that you have the React plugin installed by running the following npm command:

```sh
npm list -g --depth 0 @zeplin/cli-connect-react-plugin
```

Since the React plugin uses [react-docgen](https://github.com/reactjs/react-docgen) to analyze React components, if you can't see documentation or code snippets in Zeplin after you successfully run the command, check out react-docgen [guidelines](https://github.com/reactjs/react-docgen#guidelines-for-default-resolvers-and-handlers) for supported formats. You can also debug your components using [react-docgen playground](https://reactcommunity.org/react-docgen/).

# Related resources

- [Configuration file documentation](/CONFIGURATION_FILE.md)
- [Plugins](/README.md#Plugins)
- [Build your own plugin](https://github.com/zeplin/cli/blob/master/PLUGIN.md)
