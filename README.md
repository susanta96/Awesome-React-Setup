# React Best Setup / Boilerplate

React + pnpm (alternative to npm) + Vite.JS (Rollup) + SWC (Hot Reload) + ESLint + Prettier +

This setup includes lots of best practices and standard throughout the structure. However, All the setup steps will be included here for reference.

> This boilerplate is for people to reduce the time to setup from scratch, just use this as template to create an awesome new tool to setup react project. However, You can remove anything that, you don't require.

As, eslint comes with vite cli, so we need to setup prettier to format code and have a standard setup. Make sure, eslint & prettier config doesn't override each other.

```sh
pnpm add --save-dev --save-exact prettier
pnpm add --save-dev eslint-config-prettier
```

Install the above packages, then create `.prettierrc.json` file in the project root. As of now, for me basic setup inclues this, in the JSON. However, you can change this, as you like. Refer, [Prettier Docs](https://prettier.io/docs/en/).

> Make sure to include, `prettier` to your eslint config, on `extends` section. And it should be the last one on that list.

```json
{
	"singleQuote": true,
	"tabWidth": 2,
	"arrowParens": "avoid",
	"printWidth": 120,
	"trailingComma": "es5",
	"semi": true,
	"useTabs": true
}
```

> Now, you can create `.prettierignore` file in the root, to mention, which folders or files can be ignored during formatting.

## React + TypeScript + Vite -- Official Comes with ViteJS

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type aware lint rules:

- Configure the top-level `parserOptions` property like this:

```js
   parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module',
    project: ['./tsconfig.json', './tsconfig.node.json'],
    tsconfigRootDir: __dirname,
   },
```

- Replace `plugin:@typescript-eslint/recommended` to `plugin:@typescript-eslint/recommended-type-checked` or `plugin:@typescript-eslint/strict-type-checked`
- Optionally add `plugin:@typescript-eslint/stylistic-type-checked`
- Install [eslint-plugin-react](https://github.com/jsx-eslint/eslint-plugin-react) and add `plugin:react/recommended` & `plugin:react/jsx-runtime` to the `extends` list
