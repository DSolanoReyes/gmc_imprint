## Project setup

```
# yarn
yarn

# npm
npm install

# pnpm
pnpm install

# pnpm
bun install
```

### Compiles and hot-reloads for development

```
# yarn
yarn dev

# npm
npm run dev

# pnpm
pnpm dev

# bun
bun run dev
```

### Compiles and minifies for production

```
# yarn
yarn build

# npm
npm run build

# pnpm
pnpm build

# bun
bun run build
```

### Lints and fixes files

```
# yarn
yarn lint

# npm
npm run lint

# pnpm
pnpm lint

# bun
bun run lint
```

## Usage and Examples
Below we have an example of what the main components of the website look like. First you see that the 
image has been imported and given a name and is referenced in "objectThing" as a src, and again in 
the variable "selectedImage". This is then mounted, so it appears as the default image when the website
first loads. It has the whole object just as an insurance that the default image is the one mentioned.

```vue
<script>
  import menuimage from '/src/assets/chosenimage'
</script>
```

```javascript
<script>
export default {
    mounted() {
        this.selectedImage = {ID: "0", name: "your name", colour: "#000000", src: menuImage}
        this.objectThing[1].src = menuimage
    }
}
</script>
```


```javascript
<script>
export default {
    data () {
        objectThing: [{ ID: "1", name: "item name", colour: "#000000", src: chosenimage}]
        
        selectedImage: {src: menuimage}
    }
}
</script>
```

```javascript
<script>
export default {
    data () {
        methods: {
            changeObject () {
                if (image.ID === 1){
                    this.selectedimage = menuimage
                }
            }
        }
    }
}
</script>
```

The method gets triggered by a @click option on the <v-select></v-select> in the template section.
It's using v-models and props to call in what it sees. There is also several v-binding properties that
are being used to make things reactive. The only complicated one is the one above. Realistically
if you look at the names of what's being called you can trace down where everything is being called.

```vue
<template>
    <v-select return-object
    label="Select Menu Color"
    placeholder="Select..."
    variant="outlined"
    :items="fontColors"
    :item-props="itemProps"
    v-model="selectedImage"
    @click="changeImage"
    ></v-select>
</template>
```

## Documentation

For more information follow these other links: 
- [v-models](https://vuejs.org/guide/components/v-model.html)
- [props](https://vuejs.org/guide/components/props.html#prop-passing-details)
- [v-bind](https://vuejs.org/guide/essentials/class-and-style)

For examples on how Vuetify works with the field inputs work follow these
- [Select Component](https://vuetifyjs.com/en/components/selects/)
- [Text Field](https://vuetifyjs.com/en/components/text-fields/#usage)

For configuring Vite 
- [Configuration Reference](https://vitejs.dev/config/).

