# Quick Start Guide for React.js Apps

<!-- ## Description -->

Creating a new React App is one of the hardest steps in making a React app, for the sole reason of, you rarely do it.
You can have multiple, React apps, but for each of those apps, you only start it **ONCE**. The steps for starting them are simple, but it's not something that's easily committed to memory (Unless you make **A LOT** of apps).

- What's the syntax structure for the command to create it?
- Did I install all the packages I need? Am I missing something?
- How do I start testing on other devices?

These are some of the questions I have when I start a new React app. And while the answers are not particularly hard or hard to find, it still requires some Google-fu to get.

I created this README to help me quickly start new React apps. By putting my notes all in one place and online, I'm hoping it will help me, and possibly others, quickly set up a new React app.

## Getting Started

- This guide assumes you understand how React applications work, and you just need help with the initial set up.
- The following instructions are assuming you are using the Linux OS. I use Ubuntu.
- Make sure to have the LTS (Long Term Support) of Node to avoid errors.

## Table of Contents

1. [Starting the App](#1-starting-the-app)
2. [Installing TypeScript Separately](#2-installing-typescript-separately)
3. [Packages](#3-packages)

   3.1 [Tailwind](#31-tailwind)

4. [Testing on Other Devices](#4-testing-on-other-devices)
5. [Testing App through VirtualBox](#5-testing-app-through-virtualbox)

## [1] Starting the App

- Start a terminal instance in the directory you want place your project folder and run the following command to create a React app with Vite.

```
npm create vite@latest my-first-react-app -- --template
```

You will then be given the option to pick a Framework and a Variant.

- Framework: React
- Variant: JavaScript

You can also pick TypeScript as your Variant. [I will also have instructions later for how to add TypeScript to an existing React project.](#2-installing-typescript)

- NOTE: If I wanted to create an app with the folder name _super-cool-app_, I would run...

```
npm create vite@latest super-cool-app -- --template react
```

- **NOTE**: _For the following steps, I will assume the app's name is *super-cool-app*._
- Enter whatever you need to in the terminal to continue.
- Next, go to the directory of the newly made app, install it's packages, and open the app by going to localhost:5173 in your web browser.

```
cd super-cool-app
npm install
npm run dev
```

**Congratulation**! You have created a React App. All done. Finished.

But not really.

There's still a couple more things to do before you're done, excluding actually making your own app.

## [2] Installing TypeScript Separately

If you already created a React project and want to switch from JavaScript to TypeScript, follow these steps.

- Install these packages.

```
npm install --save typescript @types/node @types/react @types/react-dom @types/jest
```

- Create a ts.config file in root directory of your project (Next to your package.json file). There are TWO ways to do this.

#### 1 - Create the default ts.config file.

```
tsc --init
```

#### 2 - Manually create the ts.config file yourself (Advanced).

Do this if you are already familiar with how you want to configure TypeScript.

## [3] Packages

Here are some helpful packages you can use for your React projects.

### [ESLint](eslint.org)

- A linter for JavaScript.
- Should already be installed if you used Vite.
- Recommended to save as a dev dependency.

```
npm install --save-dev eslint
```

---

### [Prettier](https://prettier.io/)

- Automatically formats code for a variety of languages for improved readability.
- Also available as a VS Code extension.
- Recommended to save as a dev dependency.

```
npm install --save-dev prettier
```

---

### [SASS](https://sass-lang.com) (Or any other CSS preprocessor you prefer)

- CSS preprocessors allow you to easily write complex CSS.
- There are many processors other than SASS, such as LESS, and Stylus.

```
npm install --save-dev sass
```

---

### [React Router](https://reactrouter.com/en/main)

- When your app requires routing to multiple pages.

```
npm install react-router-dom
```

## [3.1] Tailwind

Tailwind is a CSS framework where you can use predefined class names to style your components. Since Tailwind can usually be used in combination with other packages, I'll be giving Tailwind its own section.

### [Tailwind](https://tailwindcss.com/)

Use Tailwind's installation guide according to the framework you're using.
[https://tailwindcss.com/docs/installation/framework-guides](https://tailwindcss.com/docs/installation/framework-guides)

- For Vite

  - Install tailwind, postcss, and autoprefixer.

  ```
  npm install -D tailwindcss postcss autoprefixer
  ```

  - Make sure your tailwind.config.js file has the following

  ```
  /** @type {import('tailwindcss').Config} */
  export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
  }
  ```

  - In your root directory, have a css file and add the Tailwind directives. Make sure to import the index.css file into your main.js file. (Or .jsx/.ts/.tsx)

  ```
  /* index.css */
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
  ```

  - You can now use Tailwind's classes in your project.

### [clsx](npmjs.com/package/clsx)

- A helpful utility function that constructs className strings conditionally.

```
// Implementation
// Strings (variadic)
clsx('foo', true && 'bar', 'baz');
//=> 'foo bar baz'

// Objects
clsx({ foo:true, bar:false, baz:isTrue() });
//=> 'foo baz'
```

### [tailwind-merge](https://www.npmjs.com/package/tailwind-merge)

- Utility function to merge Tailwind classes without conflicts.

```
twMerge('px-2 py-1 bg-red hover:bg-dark-red', 'p-3 bg-[#B91C1C]')
// → 'hover:bg-dark-red p-3 bg-[#B91C1C]'
```

### [class-variance-authority](npmjs.com/package/class-variance-authority)

- Allows you to create and organize variants of your components.
  [Look at the cva documentation for examples.](https://cva.style/docs/getting-started/variants)

## [4] Testing on Other Devices

Do you use multiple computers while working and want to view your app and your code at the same time?

Do you want to test your app on your actual mobile device instead of using a browser's dev tools?

Then this will be **extremely** helpful.

- In a Code editor, open your project, and open the package.json file.
- This file stores information on how your application is configured.
  - You can see your installed packages here.
- You will see an object named "scripts" that looks as such.

```
"scripts": {
    "dev": "vite",
    "build": "vite build",
    "lint": "eslint . --ext js,jsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview"
  },
```

- These are commands you can run from a terminal.
- When you first started the app and ran "npm run dev", it was actually a shortcut that ran "npm run vite".
  - You only replaced 1 word so it wasn't much of a shortcut, but you can make some really complex shortcuts.
- Add this to the scripts.

```
"host": "vite --host"
```

- And you're all done!
- All you need to do now is run your app with...

```
npm run host
```

- Your app is now running on your local network.
- Find your IP address and paste it in your browser's address bar along with the default port number, 5173, that Vite uses..
- The terminal where you ran "npm run host" should display the address you should use.
  ```
  IP_ADDRESS:5173
  ```
- You can now access your app on any devices connected to the same network, even mobile devices.

- You can add --host to the preview script to test the production version of your app on other devices.

## [5] Testing App through VirtualBox

**This step is optional and for those only in my unique situation.**

I have a Windows machine. However, I use Oracle's VirtualBox to use an Ubuntu virtual machine. Because of this, I can see my projects running on the local Ubuntu machine, but if I try to view it on another computer or a mobile device, it will not connect. Even if it's on the same network.

The solution is port forwarding.
For this, you need to know 3 things.

- Your virtual machine's IP address.
- Your host machine's IP address.
- Port numbers for each the technologies you use.

In VirtualBox on your host machine, go to Settings > Network, and you will see your network adapters.

- My current setup has 3 adapters.
  - NAT
  - Host-only Adapter
  - NAT Network
- They each have the Cable Connected enabled under Advanced.

- In the NAT adapter, click Port Forwarding.
- This is where you add your port forwarding rules for Vite. If you use other programs/frameworks, you'll need to add a rule for each of them if you plan to test on your local network.

You'll need to add your rules like so.
The name can be anything as long as you remember what it's for.

| Name         | Protocol | Host IP           | Host Port | Guest IP           | Guest Port |
| ------------ | -------- | ----------------- | --------- | ------------------ | ---------- |
| Vite         | TCP      | Host Machine's IP | 5173      | Guest Machine's IP | 5173       |
| Vite Preview | TCP      | Host Machine's IP | 4173      | Guest Machine's IP | 4173       |

Running your React app using npm run preview runs the production build which actually uses port 4173. So adding that will allow that to use the local network.

- Other default port numbers I use that can be helpful...
  - Flask: 5000
  - Visual Studio Code's Live Server Extension: 5500
  - Express: 3000

So if your sites stop loading, check for these things.

- IP addresses of your virtual machine or host might have changed.
- You're using a new technology which runs on a port that you have not added a rule for.
