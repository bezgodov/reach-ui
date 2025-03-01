# Welcome to Reach UI Development ♿️

Thanks for getting involved with Reach UI development!\
Support React@18 (except ListBox component)

## Looking for the documentation?

https://reach.tech/

## Getting Started

Reach UI is built and tested with [Yarn](https://yarnpkg.com). Please follow their [install instructions](https://yarnpkg.com/getting-started/install) to get Yarn installed on your system.

Then, run these commands:

```
git clone git@github.com:reach/reach-ui.git
cd reach-ui
pnpm install
pnpm build
```

## Root Repo Scripts:

```sh
pnpm build        # builds all packages
pnpm dev        # starts storybook server
pnpm test         # runs tests in all packages
```

## Running / Writing Examples

First do the steps in "Getting started", then start the Storybook server:

```
pnpm dev
```

Next, put a file in `packages/<component-dir>/examples/<name>.example.js` and make it look like this:

```jsx
import * as React from "react";

// The name of the example (always name the variable `name`)
let name = "Basic";

// The example to render (always name the function `Example`)
function Example() {
	return <div>Cool cool cool</div>;
}

// Assign the name to the example and then export it as a named constant
Example.storyName = name;
export const Basic = Example;

// Default export an object with the title matching the name of the Reach package
export default { title: "Dialog" };
```

Now you can edit the files in `packages/*` and storybook will automatically reload your changes.

**Note**: If you change an internal dependency you will need to run `yarn build` again. For example, if working on `MenuButton` requires a change to `Rect` (an internal dependency of `MenuButton`), you will need to run `yarn build` for the changes to `Rect` to show up in your `MenuButton` example.

## Running / Writing Tests

First do the steps in "Getting Started", then:

```
pnpm test
```

Or if you want to run the tests as you edit files:

```
pnpm test --watch
```

Often you'll want to just test the component you're working on:

```
cd packages/<component-path>
pnpm test --watch
```

## Development Plans

The components to be built come from the the [Aria Practices Design Patterns and Widgets](https://www.w3.org/TR/wai-aria-practices-1.2), with a few exceptions. Here is a table of the components and their status.

✅ - Released<br/>
🛠 - Building<br/>

| Status | Name           |
| ------ | -------------- |
| ✅     | Accordion      |
| ✅     | Alert          |
| ✅     | Alert Dialog   |
| ✅     | Checkbox       |
| ✅     | Combo Box      |
| ✅     | Dialog (Modal) |
| ✅     | Disclosure     |
| 🛠      | Hover Card     |
| ✅     | Listbox        |
| ✅     | Menu Button    |
| 🛠      | Radio Group    |
| ✅     | Slider         |
| ✅     | Tabs           |
| 🛠      | Toggletip      |
| ✅     | Tooltip        |

## Releases [DEPRECATED]

This is (was?) our current release process. It's not perfect, but it has almost the right balance of manual + automation for me. We might be able to put some of this in a script...

```sh
$ git checkout main
$ git pull origin main
$ git checkout dev
$ git pull origin dev
$ git checkout -b release-<version>
$ git merge main

# Resolve any merge conflicts and commit if necessary

# Run the build locally and make sure there are no problems
$ pnpm build
$ pnpm test

# Check out the `main` branch and merge release changes from `dev`
$ git checkout main
$ git pull origin main
$ git merge dev

# Write the changelog based on commits. We'll automate this part
# eventually, but for now this is manual.

# Then create a new version and git tag locally. Don't push yet!
$ pnpm ver [version]

# Take a look around and make sure everything is as you'd expect.
# You can inspect everything from the commit that lerna made with:
$ git log -p

# If something needs to be changed, you can undo the commit and
# delete the tag that lerna created and try again.

# If everything looks good, push to GitHub along with the new tag:
$ git push origin main --follow-tags

# Open up https://github.com/reach/reach-ui/actions and watch the build. There will
# be 2 builds, one for the push to the main branch and one for the
# new tag. The tag build will run the build and all the tests and then
# automatically publish to npm if everything passes. If there's a
# problem, we have to figure out how to fix manually.

# Paste the changelog into the release on GitHub. The release is
# complete … huzzah!
```

You need to be careful when publishing a new package because the `lerna publish` on CI will fail for new packages. To get around this, you should publish a `0.0.0` version of the package manually ahead of time. Then the release from CI will be ok. This is really janky but AFAICT the only workaround.

Stuff I'd like to improve:

- Automate changelog generation and GitHub release from CI
- Document how we're using GitHub PRs to generate the changelog somewhere

## Website

The website is a Gatsby app in the `website` directory. It automatically deploys to https://reach.tech/ when the `website` branch is updated.
