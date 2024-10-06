# Project Setup Guide

Follow the steps below to set up your project and configure TypeScript, ESLint, and Prettier.

## To Show Structure
```
tree -I "node_modules|dist|.git"
```

## Structure
```
.
├── LICENSE
├── README.md
├── eslint.config.mjs
├── package-lock.json
├── package.json
├── src
│   ├── constants
│   │   └── enum.ts
│   ├── controllers
│   │   └── user.controller.ts
│   ├── index.ts
│   ├── middlewares
│   │   └── error.middleware.ts
│   ├── models
│   │   └── User.ts
│   ├── routes
│   │   └── api.route.ts
│   ├── services
│   │   └── user.service.ts
│   ├── type.d.ts
│   └── utils
│       └── jwt.ts
└── tsconfig.json
```


## 1. Initialize the Project

```bash
npm init -y
```

## 2. Install TypeScript and Node Types

```bash
npm install typescript --save-dev
npm install @types/node --save-dev
```

## 3. Configure ESLint

Initialize ESLint configuration:

```bash
npm init @eslint/config@latest
```

### During Setup, Answer the Following Questions:

```text
How would you like to use ESLint?       problems
What type of modules does your project use?     JS
Which framework does your project use?     none
Does your project use TypeScript?     Yes
Where does your code run?     Node
Would you like to install them now?     Yes
Which package manager do you want to use?     npm
```

## 4. Install Additional Dependencies

```bash
npm install prettier eslint-config-prettier eslint-plugin-prettier tsx tsc-alias tsconfig-paths rimraf nodemon --save-dev
```

## 5. Configure `tsconfig.json`

Create a `tsconfig.json` file and paste the following content:

```json
{
  "compilerOptions": {
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "target": "ES2023",
    "outDir": "dist",
    "esModuleInterop": true,
    "strict": true,
    "skipLibCheck": true,
    "baseUrl": ".",
    "paths": {
      "~/*": ["src/*"]
    }
  },
  "files": ["src/type.d.ts"],
  "include": ["src/**/*"]
}
```

## 6. Configure ESLint

Create an `eslint.config.mjs` file and paste the following configuration:

```javascript
import globals from 'globals'
import pluginJs from '@eslint/js'
import tseslint from 'typescript-eslint'
import eslintPluginPrettier from 'eslint-plugin-prettier'

export default [
  { files: ['**/*.{js,mjs,cjs,ts}'] },
  { languageOptions: { globals: globals.node } },
  pluginJs.configs.recommended,
  ...tseslint.configs.recommended,
  {
    plugins: {
      prettier: eslintPluginPrettier
    },
    rules: {
      '@typescript-eslint/no-explicit-any': 'warn',
      '@typescript-eslint/no-unused-vars': 'warn',
      'prettier/prettier': [
        'warn',
        {
          arrowParens: 'always',
          semi: false,
          trailingComma: 'none',
          tabWidth: 2,
          endOfLine: 'auto',
          useTabs: false,
          singleQuote: true,
          printWidth: 120,
          jsxSingleQuote: true
        }
      ]
    },
    ignores: ['**/node_modules/', '**/dist/']
  }
]
```

## 7. Configure Prettier

Create a `.prettierrc` file and paste the following content:

```json
{
  "arrowParens": "always",
  "semi": false,
  "trailingComma": "none",
  "tabWidth": 2,
  "endOfLine": "auto",
  "useTabs": false,
  "singleQuote": true,
  "printWidth": 120,
  "jsxSingleQuote": true
}
```

## 8. Configure Prettier Ignore

Create a `.prettierignore` file and paste the following content:

```
node_modules/
dist/
```

## 9. Configure Editor Settings

Create a `.editorconfig` file and paste the following content:

```
[*]
indent_size = 2
indent_style = space
```

## 10. Configure Nodemon

Create a `nodemon.json` file and paste the following content:

```json
{
  "watch": ["src", ".env"],
  "ext": ".ts,.js",
  "ignore": [],
  "exec": "tsx ./src/index.ts"
}
```

## 11. Update `package.json` Scripts

Edit the `scripts` section of your `package.json` file:

```
"scripts": {
  "dev": "npx nodemon",
  "build": "rimraf ./dist && tsc && tsc-alias",
  "start": "node dist/index.js",
  "lint": "eslint .",
  "lint:fix": "eslint . --fix",
  "prettier": "prettier --check .",
  "prettier:fix": "prettier --write ."
}
```

## 12. Define Global Types

Create a `./src/type.d.ts` file:

```ts
// Define your global types here
```

## 13. Run Development, Build, and Start Commands

Use the following commands to run your project:

```bash
npm run dev       # Start the development server
npm run build     # Build the project
npm run start     # Start the project
```

## 14. Fix Lint and Format Issues

Use the following commands to fix linting and formatting issues:

```bash
npm run lint          # Run ESLint
npm run lint:fix      # Automatically fix linting issues
npm run prettier      # Check for formatting issues
npm run prettier:fix  # Automatically fix formatting issues
```

## 15. Install new package
```bash
npm i express
npm i @types/express --save-dev
```
---