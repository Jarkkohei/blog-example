# Blog-example

Blog example project with Svelte and svelte-router 

(from Youtube channel - Classsed - Svelte Tutorial (Better than React?) )

## Install

Clone project and install dependencies.
```bash
git clone https://github.com/Jarkkohei/blog-example.git
cd blog-example
npm install
```

Add `env.js` -file into the root folder of your project and add following code into it, replacing the `<YOUR_API_BASE_URL_HERE>` with your API base url ( without the trailing `/` )

This file can be used to also store other constants, although be aware that they will be visible in the bundle.js -file as a plain text.

```javascript
const env = {
    API_BASE_URL: '<YOUR_API_BASE_URL_HERE>'
};

export default env;
```

Run the developement server.
```bash
npm run dev
```



*Note that you will need to have [Node.js](https://nodejs.org) installed.*


Navigate to [localhost:5000](http://localhost:5000). You should see your app running. 

---
## Deploying to the web

### With [now](https://zeit.co/now)

Install `now` if you haven't already:

```bash
npm install -g now
```

Then, from within your project folder:

```bash
now
```

As an alternative, use the [Now desktop client](https://zeit.co/download) and simply drag the unzipped project folder to the taskbar icon.

### With [surge](https://surge.sh/)

Install `surge` if you haven't already:

```bash
npm install -g surge
```

Then, from within your project folder:

```bash
npm run build
surge public
```
