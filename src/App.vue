<template>
    <div>
        <div class="main">
            <app-display
                :totalsArr="budgetData.totals"
            ></app-display>
            <app-input
                :budgetData="budgetData"
            ></app-input>
            <app-list
                :budgetData="budgetData"
                @itemDeleted="deleteFromBudget"
            ></app-list>
        </div>
    </div>
</template>


<script>

    import Input from './components/Input.vue'
    import List from './components/List.vue'
    import Display from './components/Display.vue'


    export default {
        data() {
            return {
                budgetData: {
                    allItems: {
                        exp: [],
                        inc: [],
                    },
                    totals: {
                        exp: [],
                        inc: [],
                    }
                }
            }
        },
        components: {
            appDisplay: Display,
            appInput: Input,
            appList: List,
        },
        methods: {
            deleteFromBudget(value, id) {
                if (value > 0){
                    this.budgetData.allItems.inc.splice(id, 1);
                    this.budgetData.totals.inc.splice(id, 1);
                } else {
                    this.budgetData.allItems.exp.splice(id, 1);
                    this.budgetData.totals.exp.splice(id, 1);
                }
            }
        }
    }
</script>

<style>
    .main {
        background-color: lightblue;
        border: 1px black;
        padding: 30px;
        height: 100vh;
    }
</style>
