<script lang="ts">
    import "../app.css";
    import "svelte";
</script>
<head>
    <script src="https://cdn.freecodecamp.org/testable-projects-fcc/v1/bundle.js"></script>
</head>

<div class="h-full w-full fixed top-0 left-0 p-0 m-0 z-0 bg-primary">
</div>
<div class="h-full w-full absolute top-0 left-0 p-0 m-0 z-10">
    <slot />
</div>
