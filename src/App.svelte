<script>
 import { Router, Route } from "svelte-routing";
 import SeparateChaining from "./routes/HashTables/SeparateChaining.svelte";
 import Linear from "./routes/HashTables/Linear.svelte";
 import DoubleHashing from "./routes/HashTables/DoubleHashing.svelte";
 import Quadratic from "./routes/HashTables/Quadratic.svelte";
 import BucketSort from "./routes/SortingAlgorithms/BucketSort.svelte";
 import RadixSort from "./routes/SortingAlgorithms/RadixSort.svelte";
 import BubbleSort from "./routes/SortingAlgorithms/Bubble.svelte";
 import InsertionSort from "./routes/SortingAlgorithms/Insertion.svelte";
 import Selection from "./routes/SortingAlgorithms/Selection.svelte";
 import MergeSort from "./routes/SortingAlgorithms/Merge.svelte";
 import Quicksort from "./routes/SortingAlgorithms/Quicksort.svelte";
 import BinaryTree from "./routes/Trees/BinaryTree.svelte";
 import BST from "./routes/Trees/BST.svelte";
 import AVL from "./routes/Trees/AVL.svelte";
 import RBT from "./routes/Trees/RBT.svelte";
 import BTree from "./routes/Trees/BTree.svelte";
 import SinglyLinked from "./routes/LinkList/SinglyLinked.svelte";
 import DoublyLinked from "./routes/LinkList/DoublyLinked.svelte";
 //  import Playground from "./routes/Playground.svelte";
 import Home from "./routes/Home.svelte";

 import Kevin from "./routes/Playgrounds/Kevin.svelte";
 import Katrina from "./routes/Playgrounds/Hurricane.svelte";
 import Ayushmaan from "./routes/Playgrounds/Ayushman.svelte";
 import Pantea from "./routes/Playgrounds/Panera.svelte";
 import Sebas from "./routes/Playgrounds/Seabass.svelte";
 import Alex from "./routes/Playgrounds/Alex.svelte";
 export let url = "";
</script>

<main>
 <Router {url}>
  <div class="">
   <Route path="/" component={Home} />
   <!-- <Route path="/playground" component={Playground} /> -->
   <Route path="/hash_tables/separate_chaining" component={SeparateChaining} />
   <Route path="/hash_tables/linear" component={Linear} />
   <Route path="/hash_tables/quadratic" component={Quadratic} />
   <Route path="/hash_tables/double_hashing" component={DoubleHashing} />
   <Route path="/sorting_algo/bucket_sort" component={BucketSort} />
   <Route path="/sorting_algo/radix_sort" component={RadixSort} />
   <Route path="/sorting_algo/bubble_sort" component={BubbleSort} />
   <Route path="/sorting_algo/insertion_sort" component={InsertionSort} />
   <Route path="/sorting_algo/selection_sort" component={Selection} />
   <Route path="/sorting_algo/merge_sort" component={MergeSort} />
   <Route path="/sorting_algo/quick_sort" component={Quicksort} />
   <Route path="/trees/binary_tree" component={BinaryTree} />
   <Route path="/trees/bst" component={BST} />
   <Route path="/trees/avl" component={AVL} />
   <Route path="/trees/rbt" component={RBT} />
   <Route path="/trees/b_tree" component={BTree} />
   <Route path="/linklist/singly" component={SinglyLinked} />
   <Route path="/linklist/doubly" component={DoublyLinked} />

   <Route path="/kevin" component={Kevin} />
   <Route path="/alex" component={Alex} />
   <Route path="/katrina" component={Katrina} />
   <Route path="/ayushmaan" component={Ayushmaan} />
   <Route path="/pantea" component={Pantea} />
   <Route path="/sebas" component={Sebas} />
  </div>
 </Router>
</main>
