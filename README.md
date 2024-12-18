# Debugging JS in VSCode and Chrome

A debugger has a couple of advantages compared to good old print debugging (`console.log()`). You are able to pause the execution of your code at any point you like and can inspect not only one or two, but all values that are available at this point in the execution.

In JavaScript we need to choose a runtime (browser, node, but, etc) to add the debugger vscode comes with.

## Scenario Vanilla HTML/JS

- run your website (with Live Server, or some Preview extension)
- easiest: press `F1` or `Cmd + Shift + P` to open the Command Pallette

  - search for `Debug: Open Link`
  - enter the url, your live server/preview is running, e.g. `http://localhost:5500`
  - vscode will prompt you to create a lauch.json file for you
  - remember to include the created `.vscode` directory in your `.gitignore` to avoid clutter with your team mates

- basic launch.json:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      // environment
      "type": "chrome",
      // launch (open new browser window) vs attach (add to running process - way more complicated to configure)
      "request": "launch",
      // whatever name you like
      "name": "Launch Chrome against localhost",
      // the url you're running on
      "url": "http://localhost:5500"
    }
  ]
}
```

Now you can add breakpoints by hovering next to your line number. Whenever the execution of your code reaches this breakpoint, it will pause and let you inspect all variables, and step through the execution of your code line by line.

## Scenario Node App (CLI, Express server)

- let vscode create a launch.json for you in the 'run and debug' tab
- when your cli program expects arguments, you can add them in the "args" field
- example with multiple configs for different cli input

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Launch rps - rock",
      "skipFiles": ["<node_internals>/**"],
      "program": "${workspaceFolder}\\rps.js",
      "args": ["rock"]
    },
    {
      "type": "node",
      "request": "launch",
      "name": "Launch rps - spock",
      "skipFiles": ["<node_internals>/**"],
      "program": "${workspaceFolder}\\rps.js",
      "args": ["spock"]
    },
    {
      "type": "node",
      "request": "launch",
      "name": "Launch rps - well",
      "skipFiles": ["<node_internals>/**"],
      "program": "${workspaceFolder}\\rps.js",
      "args": ["well"]
    },
    {
      "type": "node",
      "request": "launch",
      "name": "Launch rps - multiple",
      "skipFiles": ["<node_internals>/**"],
      "program": "${workspaceFolder}\\rps.js",
      "args": ["Fly", "you", "fools!"]
    }
  ]
}
```

## Scenario: Debugging React with Vite

Start your React App as usual (npm run dev).
Then start debugging. The url needs to match the URL in your browsers bar (that is the address of dev server, vite is running)
When it comes to React, have a look at the [React DevTools](https://react.dev/learn/react-developer-tools). You can inspect your components in there and see all states right away. So there is no special need for a debugger often times.

```json
{
  "configurations": [
    {
      "type": "chrome",
      "request": "launch",
      "name": "Launch React Debugging session",
      "url": "http://localhost:5173"
    }
  ]
}
```

## Scenario: Express Web API

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node-terminal",
      "request": "launch",
      "name": "Launch Express Server",
      "command": "npm run dev",
      "skipFiles": ["<node_internals>/**"]
    }
  ]
}
```
