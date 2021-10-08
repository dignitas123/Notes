## Install dependencies
`npm install vite @vitejs/plugin-vue --save-dev`

## add "dev": "vite" to scripts in package.json

## optionally add
`"build": "vue-tsc --noEmit && vite build", // build for production`\
`"serve": "vite preview" // locally preview production build`

## create `vite.config.ts` in root folder of project
```
// vite.config.ts
import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";
import path from "path";

export default defineConfig({
    plugins: [vue()],
    resolve: {
        alias: {
            "@": path.resolve(__dirname, "/src"),
        },
    },
    define: {
        "process.env": {},
    },
});

```

## remove index.html from public folder and create index.html in root folder of project
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <link rel="icon" href="/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
</head>

<body>
    <div id="app"></div>
    <script type="module" src="/src/main.ts"></script>
</body>

</html>
```
