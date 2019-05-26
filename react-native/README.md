# React Native
React Native lets you build native mobile apps using JavaScript and React.  
https://facebook.github.io/react-native/

## Getting Started
[expo](https://docs.expo.io/versions/v32.0.0/) makes creating/running/debugging react native projects a lot easier.

```
# install expo
npm install -g expo-cli

# start a new expo project
expo init YourProjectName

# run the expo server
cd YourProjectName
npm install && npm start
```

## Running the app on your phone
1. Install the [Expo app](https://play.google.com/store/apps/details?id=host.exp.exponent&hl=en) on your phone.
2. Using the Expo app on your phone, scan the provided QR code and wait until the app is loaded.

## Running the app on a virtual android device
1. Install [Android Studio](https://developer.android.com/studio) with `sudo snap install android-studio --classic`  
    Note: after installing Android Studio, follow [these instructions](https://developer.android.com/studio/run/emulator-acceleration?utm_source=android-studio#vm-linux) to configure VM acceleration. If you get permission issues for kvm, try following [these instructions](https://stackoverflow.com/questions/37300811/android-studio-dev-kvm-device-permission-denied).
2. Open "AVD Manager" from `Android studio > Configure > AVD Manager`
3. Create and start a new Virtual Device
4. On the terminal tab where you started the expo server, type `a`. The expo server will then install Expo on the virtual device and start your app.

Note: to "shake" your android virtual device, press `Ctrl + m`. You'll see the React Native dev menu pop up.

## Configuring ESLint, Prettier, and Jest
I like using [ESLint](https://eslint.org/) for syntax errors and letting [Prettier](https://prettier.io/) take care of styling. Also, I prefer having Prettier run on `git add` and Jest run before any `git push`.

Installation:
```
npm install --save-dev eslint-config-airbnb eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react prettier eslint-config-
prettier eslint-plugin-prettier eslint-plugin-jest husky lint-staged
```

.eslintrc.json
```
{
  "env": {
    "jest": true
  },
  "extends": [
    "airbnb",
    "prettier",
    "prettier/react"
  ],
  "plugins": ["prettier", "jest"],
  "rules": {
    "react/jsx-filename-extension": [1, { "extensions": [".js", ".jsx"] }],
    "jest/no-disabled-tests": "error",
    "jest/no-focused-tests": "error",
    "jest/no-identical-title": "error",
    "jest/prefer-to-have-length": "warn",
    "jest/valid-expect": "error"
  }
}
```

Add the following to your `package.json`:
```
  "scripts": {
    "lint": "eslint src/**/*.js",
    "test": "jest",
    "test-debug": "node --inspect-brk=0.0.0.0:9229 ./node_modules/.bin/jest"
  },
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged",
      "pre-push": "npm run lint && npm run test"
    }
  },
  "lint-staged": {
    "*.{js,jsx,json,md}": [
      "prettier --write",
      "git add"
    ]
  }
```

## Additional Resources
I found two egghead courses related to react native:
- [Build a React Native Application for iOS and Android from Start to Finish](https://egghead.io/courses/build-a-react-native-application-for-ios-and-android-from-start-to-finish)
- [Build a React Native Todo Application](https://egghead.io/courses/build-a-react-native-todo-application)

I'm going to try them out and see how it goes.
