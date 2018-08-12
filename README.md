# crab

## Overview

The `crab` command line utility is intended as a CLI for React. It is drawn from extensive experience with the value of the comprehensive Ember CLI tool, but also inspired in part by VueCLI and create-react-app.

Crab differs from that latter in three core ways. 

1.  it creates a more comprehensive example scaffold. In particular this includes fully implemented Sass support, and a working browser. It is bizarre that this is not included in create-react-app, as it is one of the most challenging and poorly documented areas of the React ecosystem.
2. It includes code generators, which facilitate the creation of elements of UI, while easing the developer experience - something that Ember gets very right, and React (IMO) is abysmal at.
3. Where Create React App is setup and built with Webpack, crab uses [ParcelJS](https://parceljs.org/). Parcel is much more user-friendly and provides support for a huge amount of the modern web world with zero config.


## Installation and basic usage
```
npm install -g crab
crab create octopus-garden
cd octopus-garden
parcel index.html
```


## Usage


### create

Despite being the core functionality this is **not** yet ready for prime time. At present it will only show debug output. It should be operational within 48 hours.

### generate

Create a file - currently limited to component - for React, using current best-practise. 

Simple example

```
crab generate component components/Menu
```

As the `generate` command is aliased to `g`, and the file type is optional and defaults to component, the following is identical.

```
crab g components/Menu
```

A `.js` is appended to the filename automatically and is not required, but is harmless and will not duplicate if accidentally added.

You can create a component in any directory structure as long as the structure itself already exists.

```
crab g components/ui/nav/NavBar
```

Options are:

| Option           | Description | 
| ---------------- |-------------| 
| `-f, --functional` | Creates a functional rather than class based component |
| `--content <string>` | Content to put into the render block. Line breaks will be respected and can just be entered like so: `</h2>\n<p>`|
| `--imports <string>` | Pre-written import statements to include in the head. Again, line breaks are respected. |

Note that the last two options are intended to facilitate scripted generation of components, and do not particularly help daily workflows.

Full example:

```
crab g components/AboutUs -f --imports "import { Link } from 'react-router-dom';" --content "<h2>About Us</h2>\n\n<p>Some text about the company<Link to="/history">View our history</Link></p>"
```

Note that you can put anything in this import/content. Crab does not verify or validate it.

Note also that you don't need to use crab in any specific directory. In fact, typically you will want to run it in your `app/components` directory.

### destroy

The opposite of `generate`, using the destroy command **will remove code**.

This is a destructive command and full responsibility should be taken when using it. It is nevertheless a useful command when quickly making structures:

```
crab g AboutUs //whoops, not right
crab destroy AboutUs
crab g components/AboutUs -f
```

Be very warned, though. Crab **will** delete any file it's told to delete

```
crab destroy App.js
crab destroy index
```

The only chance to save your app is a single confirmation.

For tab-completion purposes, `crab destroy` supports the `.js` file extension, but it is not required.

#### crab

The core purpose of the `crab` CLI package is to allow you to execute `crab crab`. This will output a 🦀.


| Option           | Description | 
| ---------------- |-------------| 
| `-a, --ascii` | outputs an orange (\\/)!_!(\\/) instead |

Note that future versions may allow variadic use of the `crab` keyword, potentially allowing the output of many more crabs. This is considered an advanced feature.

### serve

Crab does **not** include tools to serve your page, instead it sets up a working Parcel application. To serve your new React application, just navigate to the directory, and run `parcel index.html`.

