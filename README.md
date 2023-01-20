# JSON Rich Format Text Area

## Svelte integration

[svelte-codemirror-editor](https://github.com/touchifyapp/svelte-codemirror-editor) is a Svelte component that allows you to easily integrate the CodeMirror v6+ editor with Svelte.

### Features

- Seamless integration with Svelte
- Only include languages you need
- Customize your theme
- Add custom extensions
- Readonly mode
- Compatible with SvelteKit

### Installation

To install the `svelte-codemirror-editor` package, run the following command:

```bash
npm install svelte-codemirror-editor
```

You will also need to install the language package you want to use, for example:

```bash
npm i @codemirror/lang-json
```

If you want to use the One Dark theme, you will need to install it as well:

```bash
npm i @codemirror/theme-one-dark
```

### Usage

To use the svelte-codemirror-editor component in your Svelte project, you can import it and use it in your component like this:

```typescript
<script lang="ts">
  import CodeMirror from "svelte-codemirror-editor";
  import { json } from "@codemirror/lang-json";
  import { oneDark } from "@codemirror/theme-one-dark";

  let value = "";
</script>

<CodeMirror bind:value
    lang={json()}
    theme={oneDark}
    styles={{
        "&": {
            width: "500px",
            maxWidth: "100%",
            height: "50rem",
        },
}}
/>

<style></style>
```

#### Props and Events

The CodeMirror component accepts the following props:

- `class `: string
- `value` : string
- `basic` : boolean
- `lang` : LanguageSupport
- `theme` : Extension
- `extensions` : Extension[]
- `useTab` : boolean
- `tabSize` : number
- `styles` : ThemeSpec
- `lineWrapping` : boolean
- `editable` : boolean
- `readonly` : boolean
- `placeholder` : string | HTMLElement

- `on:change={handleChanges}` : This is an event listener that binds the change event to the `handleChanges` callback function. When the user changes the content of the editor, the `handleChanges` function is called.

**Note:**

You can access the content of the `CodeMirror` component using `obj.detail` in this `handleChanges` function

```typescript
const handleChanges = (obj: CustomEvent) => {
  console.log(JSON.parse(obj.detail));
};
```

But you can also bind the value of the editor to a variable in your component by using the `bind:value` attribute, and listen to the change event to handle changes to the editor's content.

```typescript
let value = "";

const handleChanges = () => {
  console.log(JSON.parse(value));
};
```

This is an example of how to use the component in a Svelte app:

```typescript
<script lang="ts">
    import CodeMirror from "svelte-codemirror-editor";
    import { json } from "@codemirror/lang-json";
    import { oneDark } from "@codemirror/theme-one-dark";

    let value = "";

     // Handle changes callback function
    const handleChanges = () => {
      console.log(JSON.parse(value))
    }

</script>

<main>
  <CodeMirror
    bind:value
    basic={true} <!-- Basic configuration. Show the line number. Toggle line numbers -->
    useTab={true} <!-- Allows the use of tabulator -->
    tabSize={2} <!-- Defines the number of spaces the tabulator has -->
    lineWrapping={false} <!-- Choose whether or not to break lines -->
    lang={json()}
    theme={oneDark}
    styles={{
        "&": {
            width: "90vw",
            maxWidth: "90vw",
            height: "80vh",
            textAlign: "left", // by default it starts in the center
        },
    }}
    on:change={handleChanges}
/>
</main>

<style></style>
```

In this way, when the user changes the content of the editor, the handleChanges function is called, and it can do something with the content of the editor (in this case it parse the json and log it).
