---
sidebarDepth: 3
---

# vuepress-plugin-serve <GitHubLink repo="vuepress/vuepress-plugin-serve"/>

`vuepress-plugin-serve` is a VuePress plugin which serves generated files.

## Usage

### Global Installation

```bash
npm install -g vuepress-plugin-serve
# OR
yarn global add vuepress-plugin-serve
```

### Local Installation

```bash
npm install vuepress-plugin-serve
# OR
yarn add vuepress-plugin-serve
```

### Add to `config.js`

```js
module.exports = {
  plugins: [
    ['serve', {
      post: 1234,
      staticOptions: {
        dotfiles: 'allow',
      },
    }],
  ]
}
```
or
```js
module.exports = {
  plugins: {
    serve: {
      beforeServer(app, server) {
        app.get('/path/to/my/custom', function(req, res) {
          res.json({ custom: 'response' })
        })
      },
    },
  }
}
```

## CLI

After using this plugin, VuePress will add a `serve` command. This command will created a server based on the generated files. It has the following options:

### --build

Execute `vuepress build` before creating the server.

### --open

Open the browser when the server is ready.

### --host `<host>`

See [host](#host).

### --port `<port>`

See [port](#port).

## Configuration

### commandName

- **type:** `string`
- **default:** `'serve'`

Vuepress-plugin-serve will add a vuepress command. This option can be used to specify the command name.

### host

- **type:** `string`
- **default:** `'localhost'`

Specify the host to use for the server.

### port

- **type:** `number`
- **default:** `8080`

Specify the port to use for the server.

### notFoundPath

- **type:** `string`
- **default:** `'404.html'`

Path for "404 not found" page.

### staticOptions

- **type:** `object`
- **default:** `{}`

Options for [serve-static](https://github.com/expressjs/serve-static#servestaticroot-options).

### beforeServer

- **type:** `(app, server) => void`
- **default:** `undefined`

Executed before the server accepts client information. Similar to VuePress's [beforeDevServer](https://v1.vuepress.vuejs.org/en/plugin/option-api.html#beforedevserver) option.

### afterServer

- **type:** `async (app, server) => void`
- **default:** `undefined`

Executed after the server accepts client information. Similar to VuePress's [afterDevServer](https://v1.vuepress.vuejs.org/en/plugin/option-api.html#afterdevserver) option.
