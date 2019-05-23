# TypeScript

## Getting Started
1. Install typescript
    ```
    npm install --save-dev typescript
    ```
2. Add a "tsc" script to your package.json:
    ```
    //package.json
    ...
    "scripts": {
      "tsc": "tsc",
      ...
    },
    ```
3. Create a tsconfig.json file with tsc init:
    ```
    npm run tsc -- --init
    ```
    Note: Modify the tsconfig.json values to match your project structure.

4. Compile typescript
    ```
    npm run tsc
    ```

## Useful links
- [Use Prettier with TSLint and be happy](https://alexjover.com/blog/use-prettier-with-tslint-and-be-happy/)
- [Using Jest with TypeScript](https://basarat.gitbooks.io/typescript/docs/testing/jest.html)
- [Rusty Composition in TypeScript](https://hashnode.com/post/rusty-composition-in-typescript-cjo8g6y6b004hlxs1sabgzuzd)
- [Setting up a monorepo with Lerna for a TypeScript project](https://blog.logrocket.com/setting-up-a-monorepo-with-lerna-for-a-typescript-project-b6a81fe8e4f8)
