# Vite React Typescript Eslint Prettier Husky Lint-staged

Create vite react typescript app using below command

```tsx
npm create vite@latest <app-name> --template react-ts
```

Install dependencies using below command

```tsx
npm i  or npm install
```

Install Eslint as dev dependency using below command

```tsx
npm i -D eslint
```

**Setup Eslint**

init eslint using below command

```tsx
npx eslint --init  or npm eslint/config
```

You will be asked to respond to a few questions. Select answers as listed below.

- How would you like to use ESLint? - To check syntax, find problems, and enforce code style
- What type of modules does your project use? - JavaScript modules (import/export)
- Which framework does your project use? - React
- Does your project use TypeScript? - Yes
- Where does your code run? - Browser
- How would you like to define a style for your project? - Use a popular style guide
- Which style guide do you want to follow? - standard
- What format do you want your config file to be in? - javascript
- The config that you've selected requires the following dependencies - Yes

Open .eslintrc.cjs file and below config

```tsx
module.exports = {
  ....other-configs
  overrides: [],
  parserOptions: {
   ....other-configs
    project: './tsconfig.json',
  },
  ....other-configs
  settings: {
    react: {
      version: 'detect',
    },
  },
};
```



**Verify eslint configuration by executing below command.**

```tsx
npx eslint --ext .jsx,.js,.tsx,.ts src/ or npx eslint .
```

> It should show messages similar like "XXXX problems (XXXX errors, XX warnings)"



**Setup Prettier**

Install prettier as dev dependency using below command

```tsx
npm i -D prettier
```

Linters usually contain not only code quality rules, but also stylistic rules. Most stylistic rules are unnecessary when using Prettier, but worse – they might conflict with Prettier. So let's turn off eslint rules that conflicts with Prettier using pre made config called "eslint-config-prettier".

```tsx
npm install --save-dev eslint-config-prettier
```

Then, add "prettier" to the "extends" array in your .eslintrc.json file. Make sure to put it last, so it gets the chance to override other configs.

```tsx
module.exports = {
    ....other-configs
    "extends": [
        ....other-configs
        "prettier"
    ],
    ....other-configs
}
```

Install Prettier plugin in VS code and configure below setting by going in vs code user settings, use `cmd + ,` to open using settings and search format

![](/Users/nimmakayala.reddy/Desktop/Screenshot%202023-02-01%20at%2011.07.00%20AM.png)



#### **Configure pre-commit hook with husky & lint-staged**

Set up a pre-commit hook using husky & lint-staged to make sure that every commit is formatted.

```tsx
npm install --save-dev husky lint-staged
npx husky install
npm set-script prepare "husky install"
npx husky add .husky/pre-commit "npx lint-staged"
```

Add following object inside your package.json file.

```tsx
"lint-staged": {
        "src/**/*.{js,jsx,ts,tsx}": "eslint --cache --fix",
        "src/**/*.{js,jsx,ts,tsx,css,scss,md}": "prettier --write --ignore-unknown"
    }
```

#### Test configuration

Open couple of .ts/.tsx files and add unnecessary indents as well as the "debugger" keyword at multiple places and save your files.

Stage all the modified files and try to commit your changes using following commands.

```
git add .
git commit -m "does it work?"
```

It should trigger pre-commit hook.
