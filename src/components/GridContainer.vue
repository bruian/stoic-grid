<template>
  <div>
    <div class="container">
      <div class="column">
        <div class="head decoration-head">Column 1</div>
        <div class="cell decoration-cell">Item 1</div>
        <div class="cell decoration-cell">Item 2</div>
        <div class="cell decoration-cell" style="grid-row-start: 4; grid-row-end: 6;">Item 3</div>
        <div class="cell decoration-cell">Item 4</div>
        <div class="cell decoration-cell">Item 5</div>
        <div class="cell decoration-cell">Item 6</div>
        <div class="cell decoration-cell">Item 7</div>
      </div>

      <div class="column">
        <div class="head decoration-head">Column 2</div>
        <div class="cell decoration-cell">Four</div>
        <div class="cell decoration-cell">Five</div>
      </div>

      <SortableColumn lockAxis="y" v-model="items">
        <div class="head decoration-head">Sortable</div>
        <SortableItem v-for="(item, index) in items" :index="index" :key="index" :item="item"/>
      </SortableColumn>

      <!-- <div class="decoration-cell">d</div> -->
    </div>
    <br>
    {{items}}
    {{items2}}
  </div>
</template>

<script>
import { ContainerMixin, ElementMixin } from "vue-slicksort";

const SortableColumn = {
  mixins: [ContainerMixin],
  template: `
    <div class="column">
      <slot />
    </div>
  `
};

const SortableItem = {
  mixins: [ElementMixin],
  props: ["item"],
  template: `
    <div class="cell decoration-cell">{{item}}</div>
  `
};

export default {
  name: "GridContainer",
  components: {
    SortableItem,
    SortableColumn
  },
  props: {
    msg: String
  },
  data() {
    return {
      items: ["Item 1", "Item 2", "Item 3"],
      items2: ["Item 4", "Item 5", "Item 6"]
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.container {
  display: grid;
  grid-template-columns: repeat(3, minmax(30px, 200px));
  /* grid-auto-rows: 200px; */
}

.column {
  display: grid;
  grid-template-rows: 20px repeat(10, 1fr) auto;
  grid-auto-rows: 30px;
}

.head {
}

.decoration-cell {
  border: 1px dotted gray;
  background-color: antiquewhite;
}

.decoration-head {
  background-color: aqua;
}
</style>
