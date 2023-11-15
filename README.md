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

### Eslint Rules

this is an optional setting which I prefer. You can remove this, if you don't like to get errors when using `console.log` statements. But this actually help before commiting the code, sometimes developers do forget to remove `console.log` which leads to heavier bundle size.

```cjs
{
	rules: {
		'no-console': ['error', { allow: ['warn', 'error'] }],
	},
}
```

### Setup Conventional Commits with husky

This will require, if you're in a team environment, which is will force developer to write conventional commits.

> You can remove husky, conventional commits, commitizen, if you're setting up only for personl projects.

```sh
pnpm dlx husky-init && pnpm install
```

It will:

1. Add `prepare` script to package.json
2. Create a sample pre-commit hook that you can edit (by default, npm test will run when you commit)
3. You can change, from default to set you linting rules and lint fix commands. (we're making it, <b>npx lint-staged</b>, instead of pnpm test).

```sh
pnpm add --save-dev lint-staged
```

lint staged will help you to run eslint or any formatting only on staged files, not full repo.
this is actually a very good, pre-commit hooks to be run.

Also add this to package.json:

```json
{
	"lint-staged": {
		"*.(js|ts|tsx|jsx)": "prettier --write --ignore-unknown"
	}
}
```

To add another hook use husky add. For example:

```sh
pnpm husky add .husky/commit-msg 'echo "something"'
```

After running this, it will create an file / hooks in `.husky` folder. There, we'll add conventional commits bash script.

```bash
#!/usr/bin/env sh
if ! head -1 "$1" | grep -qE "^(feat|fix|chore|docs|test|style|refactor|perf|build|ci|revert)(\(.+?\))?: .{1,}$"; then
    echo "Aborting commit. Your commit message is invalid." >&2
    exit 1
fi
if ! head -1 "$1" | grep -qE "^.{1,88}$"; then
    echo "Aborting commit. Your commit message is too long." >&2
    exit 1
fi
```

this will make sure you're following the conventional pattern. Now, we just need to setup another thing, called `commitizen`, for helping developers to write conventional commits using CLI.

```sh
pnpm add -g commitizen
```

```sh
commitizen init cz-conventional-changelog --pnpm --save-dev --save-exact
```

After this almost you're ready to have proper commit setup. just add new script to package.json:

```json
{
	"scripts": {
		"cz": "git cz",
		"acp": "git add . && git cz && git push" //optional
	}
}
```

Thats it. Done ✅ .

#### FYI -- Uninstall

If you really want to Uninstall husky and other hooks

```sh
pnpm remove husky && git config --unset core.hooksPath
```

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
