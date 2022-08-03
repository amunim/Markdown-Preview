<script lang="ts">
    import Fa from "svelte-fa";
    import { faFreeCodeCamp } from "@fortawesome/free-brands-svg-icons";
    import { faArrowsAlt, faCompress } from "@fortawesome/free-solid-svg-icons";

    export let id: string;
    export let text: string;
    export let compressed = false;
    export let onExpandCollapse: Function;
</script>

<div class="flex flex-col items-center my-4 {(compressed) ? "h-max" : "" }">
    <div class="border-[1.5px] p-0 w-[30rem] shadow-2xl">
        <div class="bg-secondary p-1 m-0">
            <div class="flex flex-row my-0 justify-start border-b-2">
                <Fa class="mt-1" icon={faFreeCodeCamp} />
                <h2 class=" font-bold ml-1">Editor</h2>

                <div
                    class="ml-auto hover:bg-secondary"
                    on:click={() => onExpandCollapse()}
                >
                    <Fa
                        class="mt-1 changeonhover"
                        icon={compressed ? faCompress : faArrowsAlt}
                    />
                </div>
            </div>
        </div>
        <textarea
            {id}
            class="m-0 p-0 bg-highlightbg resize-y min-h-[140px] -mb-1 w-full"
            bind:value={text}
        />
    </div>
</div>
