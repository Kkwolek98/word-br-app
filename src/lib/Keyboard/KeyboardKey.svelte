<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import type { LetterState } from "../types/letterState";

  export let key: string;
  export let keyState: LetterState;

  const dispatch = createEventDispatcher();

  function getKeyColor(): string {
    switch (keyState) {
      case "default":
        return "bg-gray-500";
      case "correctPlacement":
        return "bg-green-500";
      case "wrongPlacement":
        return "bg-yellow-500";
      case "doesntOccur":
        return "bg-gray-900";
    }
  }

  function getTextDisabledStyles(): string {
    if (keyState === "doesntOccur") {
      return "text-gray-200 font-normal shadow-none";
    } else {
      return "";
    }
  }

  function handleClick() {
    dispatch("keyClick", key);
  }
</script>

<button
  on:click={handleClick}
  class={`${getKeyColor()} w-9 h-12 text-white font-bold rounded-lg shadow-md ${getTextDisabledStyles()}`}
  disabled={keyState === "doesntOccur"}>
  {key}
</button>
