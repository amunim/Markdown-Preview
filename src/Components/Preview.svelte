<!-- <script lang="ts" context="module">
    export enum Width {
        lg = "lg",
        xl = "xl",
        twoxl = "2xl",
    }
</script> -->
<script lang="ts">
    import Fa from "svelte-fa";
    import { faFreeCodeCamp } from "@fortawesome/free-brands-svg-icons";
    import { faArrowsAlt, faCompress } from "@fortawesome/free-solid-svg-icons";

    export let id: string;
    export let markup: string;
    export let compressed = false;
    export let onExpandCollapse: Function;
</script>

<div class="flex flex-col items-center my-4 p-10">
    <div class="border-[1.5px] p-0 w-[49rem] shadow-2xl">
        <div class="bg-secondary p-1 m-0">
            <div class="flex flex-row my-0 justify-start border-b-2">
                <Fa class="mt-1" icon={faFreeCodeCamp} />
                <h2 class=" font-bold ml-1">Previewer</h2>

                <div class="ml-auto" on:click={() => onExpandCollapse()}>
                    <Fa class="mt-1 hover:fill-orange-500 changeonhover" icon={(compressed ? faCompress: faArrowsAlt)} />
                </div>
            </div>
        </div>
        <div
            {id}
            class="m-0 py-0 px-4 bg-highlightbg -mb-1 w-full border-b-2"
        >
            {@html markup}
        </div>
    </div>
</div>
