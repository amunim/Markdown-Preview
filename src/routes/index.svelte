<script lang="ts">
    import Editor from "../Components/Editor.svelte";
    import Preview from "../Components/Preview.svelte";
    import { Parser, Lexer } from "marked";
    let parser = new Parser();
    let lexer = new Lexer();
    let showFull = 0; //0 - none, 1 - editor, 2 - preview
    let text = "";
    let markup = "";
    $: {
        lexer = new Lexer();
        markup = parser.parse(lexer.lex(text));
    }

    function handleClick(showFullIndex: number): void
    {
        if (showFull === showFullIndex)
            showFull = 0;
        else
            showFull = showFullIndex;
    }
</script>

<svelte:head>
    <title>Simple Markdown Previewer</title>
    <html lang="en" />
</svelte:head>

{#if showFull == 0}
<Editor id="editor" bind:text onExpandCollapse={() => handleClick(1)}/>
    <Preview id="preview" {markup} onExpandCollapse={() => handleClick(2)}/>
{:else if showFull == 1}
<Editor id="editor" bind:text compressed onExpandCollapse={() => handleClick(1)}/>
{:else if showFull == 2}
<Preview id="preview" {markup} compressed onExpandCollapse={() => handleClick(2)}/>
{:else}
An error occured!
{/if}
