# Install dependencies
`npm install vite @vitejs/plugin-vue --save-dev`

# add "dev": "vite" to scripts in package.json

# optionally add
# "build": "vue-tsc --noEmit && vite build", // build for production
# "serve": "vite preview" // locally preview production build

# create vite.config.ts in root
```
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
