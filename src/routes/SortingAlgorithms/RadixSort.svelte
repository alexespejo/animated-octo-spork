<script>
 import FormControl from "../../components/custom/FormControl.svelte";
 import Controls from "../../components/custom/layout/Controls.svelte";
 import Visualize from "../../components/custom/layout/Visualize.svelte";
 import NumberInput from "../../components/custom/Inputs/NumberInput.svelte";
 import MarkedElements from "../../components/SortingAlgoControls/BucketSortControls/MarkedElements.svelte";
 import {
  generateRandomIntArray,
  generateRandomStringArray,
 } from "../../lib/sortingAlgo";
 import { onMount } from "svelte";
 import LabelInput from "../../components/custom/Inputs/Label.svelte";
 import HiddenLabel from "../../components/custom/Inputs/HiddenLabel.svelte";
 import Layout from "../../layouts/Layout.svelte";
 import Button from "../../components/custom/Button.svelte";
 import TextInput from "../../components/custom/Inputs/TextInput.svelte";

 let listOfBuckets = [];
 let intOrStringArray = false;
 let bucket = [];
 let subBuckets = [];
 let insertValue = "";
 let indexOfPass = 0;
 let characterCount = 1;
 let itemMarked = "";
 let alphabet = "abcdefghijklmnopqrstuvwxyz";

 function createBuckets() {
  indexOfPass = 0;
  bucket = [];
  subBuckets = [];
  if (intOrStringArray) {
   bucket = generateRandomIntArray(characterCount);
  } else {
   bucket = generateRandomStringArray(characterCount);
  }
  subBuckets.push([...bucket]);
  listOfBuckets = subBuckets;
 }

 function updateBuckets() {
  subBuckets = [];
  subBuckets.push([...bucket]);
  if (intOrStringArray) {
   for (let i = 1; i <= indexOfPass; i++) {
    subBuckets.push(
     [...bucket].sort((a, b) => {
      return (
       Math.floor((a % Math.pow(10, i)) / Math.pow(10, i - 1)) -
       Math.floor((b % Math.pow(10, i)) / Math.pow(10, i - 1))
      );
     })
    );
   }
  } else {
   for (let i = 1; i <= indexOfPass; i++) {
    subBuckets.push(
     [...bucket].sort((a, b) => {
      return a.slice(-i).localeCompare(b.slice(-i));
     })
    );
   }
  }
  listOfBuckets = subBuckets;
 }

 function markElement(key) {
  if (itemMarked === key) {
   itemMarked = "";
  } else {
   itemMarked = key;
  }
 }

 onMount(() => {
  createBuckets();
 });
</script>

<Layout dataStructure="SA">
 <Controls title="Radix Sort">
  <FormControl>
   <HiddenLabel />
   <div class="join space-x-0.5">
    <Button
     color="secondary"
     styles="btn join-item btn-outline"
     on:click={() => {
      if (indexOfPass > 0) {
       indexOfPass--;
       updateBuckets();
      }
     }}
    >
     Undo Pass
    </Button>
    <Button
     color="primary"
     styles="btn join-item btn-outline"
     on:click={() => {
      if (indexOfPass < characterCount) {
       indexOfPass++;
       updateBuckets();
      }
     }}
    >
     Next Pass
    </Button>
   </div>
  </FormControl>
  <FormControl>
   <HiddenLabel />
   <div class="join">
    <TextInput
     color="primary"
     styles="font-bold input input-outline w-16 join-item w-max-w-xs input-sm"
     maxLength={characterCount}
     bind:value={insertValue}
    />
    <Button
     color="primary"
     styles="btn btn-primary btn-outline join-item"
     on:click={() => {
      if (intOrStringArray && !isNaN(Number(insertValue))) {
       bucket.push(parseInt(insertValue));
      } else if (!intOrStringArray && !/\d/.test(insertValue)) {
       bucket.push(insertValue.toUpperCase());
      } else {
       bucket.push("-");
      }
      updateBuckets();
     }}
    >
     Insert
    </Button>
   </div>
  </FormControl>
  <FormControl>
   <HiddenLabel />
   <div class="join">
    <NumberInput
     color="success"
     styles="font-bold input input-bordered join-item input-success"
     bind:value={characterCount}
     placeholder="Maximum: 6"
     on:input={() => {
      if (characterCount > 6) {
       characterCount = 6;
      }
     }}
    />
    <Button
     color="success"
     styles="btn btn-outline join-item"
     on:click={() => {
      createBuckets();
     }}
    >
     Update
    </Button>
   </div>
  </FormControl>

  <FormControl>
   <HiddenLabel />
   <div class="join">
    <Button
     color="primary"
     styles={`btn  join-item ${!intOrStringArray ? "btn-outline" : ""}`}
     on:click={() => {
      intOrStringArray = true;
      createBuckets();
     }}>Integer</Button
    >
    <Button
     color="primary"
     styles={`btn  join-item ${intOrStringArray ? "btn-outline" : ""}`}
     on:click={() => {
      intOrStringArray = false;
      createBuckets();
     }}>String</Button
    >
   </div>
  </FormControl>
  <FormControl>
   <HiddenLabel />
   <div class="join">
    <Button
     color="accent"
     styles="btn btn-outline join-item "
     on:click={() => createBuckets()}
     >Randomize <svg
      xmlns="http://www.w3.org/2000/svg"
      width="16"
      height="16"
      fill="currentColor"
      class="bi bi-shuffle"
      viewBox="0 0 16 16"
     >
      <path
       fill-rule="evenodd"
       d="M0 3.5A.5.5 0 0 1 .5 3H1c2.202 0 3.827 1.24 4.874 2.418.49.552.865 1.102 1.126 1.532.26-.43.636-.98 1.126-1.532C9.173 4.24 10.798 3 13 3v1c-1.798 0-3.173 1.01-4.126 2.082A9.6 9.6 0 0 0 7.556 8a9.6 9.6 0 0 0 1.317 1.918C9.828 10.99 11.204 12 13 12v1c-2.202 0-3.827-1.24-4.874-2.418A10.6 10.6 0 0 1 7 9.05c-.26.43-.636.98-1.126 1.532C4.827 11.76 3.202 13 1 13H.5a.5.5 0 0 1 0-1H1c1.798 0 3.173-1.01 4.126-2.082A9.6 9.6 0 0 0 6.444 8a9.6 9.6 0 0 0-1.317-1.918C4.172 5.01 2.796 4 1 4H.5a.5.5 0 0 1-.5-.5"
      />
      <path
       d="M13 5.466V1.534a.25.25 0 0 1 .41-.192l2.36 1.966c.12.1.12.284 0 .384l-2.36 1.966a.25.25 0 0 1-.41-.192m0 9v-3.932a.25.25 0 0 1 .41-.192l2.36 1.966c.12.1.12.284 0 .384l-2.36 1.966a.25.25 0 0 1-.41-.192"
      />
     </svg></Button
    >
    <Button
     color="accent"
     styles="btn btn-outline join-item"
     on:click={() => {
      for (let i = bucket.length - 1; i > 0; i--) {
       const j = Math.floor(Math.random() * (i + 1));
       [bucket[i], bucket[j]] = [bucket[j], bucket[i]];
      }
      updateBuckets();
     }}
    >
     Shuffle
    </Button>
   </div>
  </FormControl>
 </Controls>
 <Visualize>
  <div class=" flex space-x-5 text-base">
   {#each listOfBuckets as subBucket, index}
    <div class="bucket">
     <div class="bucket-block border-base-100">
      {#if index === 0}
       Original
      {:else if index >= 1}
       <span>{alphabet.slice(0, characterCount - index)}</span>
       <span class="text-info"
        >{alphabet.slice(
         characterCount - index,
         characterCount - index + 1
        )}</span
       >
       <span>{alphabet.slice(characterCount - index + 1, characterCount)}</span>
      {/if}
     </div>
     {#each subBucket as item}
      <MarkedElements mark={itemMarked === item} func={() => markElement(item)}>
       {item}
      </MarkedElements>
     {/each}
    </div>
   {/each}
  </div>
 </Visualize>
</Layout>

<style>
 .bucket {
  @apply flex flex-col;
 }
 .bucket-block {
  @apply font-bold p-3 w-10 text-center border-2 border-base-100 flex items-center justify-center;
 }
</style>
