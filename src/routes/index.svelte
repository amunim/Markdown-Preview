<script lang="ts">
    import Editor from "../Components/Editor.svelte";
    import Preview from "../Components/Preview.svelte";
    import { Parser, Lexer } from "marked";
    let parser = new Parser();
    let lexer = new Lexer();
    let showFull = 0; //0 - none, 1 - editor, 2 - preview
    let text = `# Welcome to my Svelte Markdown Previewer!

## This is a sub-heading...
### And here's some other cool stuff:

Heres some code, \`<div></div>\`, between 2 backticks.

\`\`\`
// this is multi-line code:

function anotherExample(firstLine, lastLine) {
  if (firstLine == '\`\`\`' && lastLine == '\`\`\`') {
    return multiLineCode;
  }
}
\`\`\`

You can also make text **bold**... whoa!
Or _italic_.
Or... wait for it... **_both!_**
And feel free to go crazy ~~crossing stuff out~~.

There's also [links](https://www.freecodecamp.org), and
> Block Quotes!

And if you want to get really crazy, even tables:

Wild Header | Crazy Header | Another Header?
------------ | ------------- | -------------
Your content can | be here, and it | can be here....
And here. | Okay. | I think we get it.

- And of course there are lists.
  - Some are bulleted.
     - With different indentation levels.
        - That look like this.


1. And there are numbered lists too.
1. Use just 1s if you want!
1. And last but not least, let's not forget embedded images:

![freeCodeCamp Logo](https://cdn.freecodecamp.org/testable-projects-fcc/images/fcc_secondary.svg)
`;
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