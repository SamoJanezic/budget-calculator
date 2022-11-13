<template>
    <div class="container cont-input">
        <div class="row justify-content-center">
            <div class="col-md-2">
                <select v-model="typeOf">
                    <option value="income">Income</option>
                    <option value="expense">Expense</option>
                </select>
            </div>
            <div class="col-md-4">
                <input
                id="descriptionField"
                type="text"
                size="30"
                placeholder="Add description"
                v-model="description"
                @keyup.enter="changeFocus('valueField')">
            </div>
            <div class="col-md-2">
                <input
                id="valueField"
                type="number"
                size="4"
                placeholder="Value"
                v-model="value"
                @keyup.enter="createItem()">
            </div>
            <button class="col-md-2" @click="createItem()">Submit</button>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                typeOf: 'income',
                description: '',
                value: '',
            }
        },
        methods: {
            createItem() {
                if (this.description === '' || this.value === ''){
                    return;
                }
                if (this.typeOf === 'income' && this.value > 0) {
                    this.budgetData.allItems.inc.push(new Income(this.getId(this.budgetData.allItems.inc.length), this.description, this.value));
                    this.budgetData.totals.inc.push(parseFloat(this.value))
                } else {
                    this.budgetData.allItems.exp.push(new Expense(this.getId(this.budgetData.allItems.exp.length), this.description, this.value));
                    this.budgetData.totals.exp.push(parseFloat(-Math.abs(this.value)));
                }
                this.resetFields();
                this.changeFocus('descriptionField');
            },
            getId(type) {
                if(type === 0) {
                    return 1;
                } else {
                    return type + 1;
                }
            },
            // sendData() {
            //     this.$emit('wasSend', [this.typeOf, this.description, this.value]);
            //     resetFields();
            // },
            resetFields() {
                this.description = '';
                this.value = '';
            },
            changeFocus(field) {
                document.getElementById(field).focus();
            }
        },
        props: ['budgetData'],
    }

    class Income{
        constructor(id, description, value) {
            this.id = id;
            this.description = description;
            this.value = value;
            this.show = false;
        }
    }

    class Expense{
        constructor(id, description, value) {
            this.id = id;
            this.description = description;
            this.value = -value;
            this.show = false;
        }
    }
</script>

<style scoped>
    .cont-input {
        padding:10px;
        border: 1px solid black;
        background-color:aqua;
    }
    input[type=number]{
        width: 100px;
    }
</style>