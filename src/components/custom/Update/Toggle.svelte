<script lang="ts">
 import "./Toggle.styles.css";
 export let checked: boolean;
 export let color: string = "";
 export let classList: string = "";
</script>

<input
 type="checkbox"
 on:change
 bind:checked
 class={`toggle  ${color} ${classList}`}
/>
