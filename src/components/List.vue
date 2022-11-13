<template>
  <div class="container">
    <div class="row justify-content-between">
      <div class="col-6">
        <div>
          <li
            v-for="(el, idx) in budgetData.allItems.inc"
            :key="idx"
            style="list-style: none"
          >
            <div
              class="row pos"
              @mouseover="el.show = true"
              @mouseleave="el.show = false"
            >
              <div class="col-2 cBorder">{{ el.id }}</div>
              <div class="col-6 cBorder">{{ el.description }}</div>
              <div class="col-4 cBorder">
                {{ Math.abs(el.value).toFixed(2) }} €
                <div
                  v-if="el.show"
                  class="btn"
                  @click="deleteItem(el.value, idx)"
                >
                  <i class="fa fa-close"></i>
                </div>
              </div>
            </div>
          </li>
        </div>
      </div>
      <div class="col-6">
        <div>
          <li
            v-for="(el, idx) in budgetData.allItems.exp"
            :key="idx"
            style="list-style:none"
          >
            <div
              class="row neg"
              @mouseover="el.show = true"
              @mouseleave="el.show = false"
            >
              <div class="col-2 cBorder">{{ el.id }}</div>
              <div class="col-6 cBorder">{{ el.description }}</div>
              <div class="col-4 cBorder">
                {{ -Math.abs(el.value).toFixed(2) }} €
                <div
                  v-if="el.show"
                  class="btn"
                  @click="deleteItem(-el.value, idx)"
                >
                  <i class="fa fa-close"></i>
                </div>
              </div>
            </div>
          </li>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {
    deleteItem(value, id) {
      this.$emit("itemDeleted", value, id);
    }
  },
  props: ["budgetData"]
};
</script>

<style>
.cBorder {
  border: 1px solid black;
  width: 100;
}
.pos {
  background-color: lightgreen;
}
.neg {
  background-color: rgb(255, 67, 67);
}
.btn {
  float: right;
  text-align: right;
  padding: 0px 2px 0px 2px;
  display: inline-block;
  height: 20px;
  cursor: pointer;
  line-height: 1;
}
</style>
