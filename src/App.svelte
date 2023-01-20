<script lang="ts">
      import CodeMirror from "svelte-codemirror-editor";
    import { json } from "@codemirror/lang-json";
    import { oneDark } from "@codemirror/theme-one-dark";
    
    let value = "";

    const handleChanges = () => {
      console.log(JSON.parse(value))
    }
    
</script>

<main>
  <CodeMirror
    bind:value
    basic={true}
    useTab={true}
    tabSize={2}
    lineWrapping={false}
    lang={json()}
    theme={oneDark}
    styles={{
        "&": {
            width: "90vw",
            maxWidth: "90vw",
            height: "80vh",
            textAlign: "left",
        },
    }}
    on:change={handleChanges}
/>
</main>

<style>

</style>