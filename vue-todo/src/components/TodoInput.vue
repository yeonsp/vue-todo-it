<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer cursor" v-on:click="addTodo">
        <font-awesome-icon :icon="['fas', 'plus']" class="addBtn" />
    </span>

    <TodoModal v-if="showModal" @close="showModal = false">
        <h3 slot:header class="closeModalBtn">
            경고
            <font-awesome-icon :icon="['fas', 'times']" @click="showModal=false" class="cursor" />
        </h3>
        <div slot:body>아무것도 입력하지 않으셨습니다.</div>
    </TodoModal>
  </div>
</template>

<script>
import { TodoModal } from "./common/TodoModal.vue";
export default {
    data() {
        return {
            newTodoItem: "",
            showModal: false,
        }
    },
    methods: {
        addTodo() {
            if (this.newTodoItem !== '') {
                this.$emit('addTodoItem', this.newTodoItem);
                this.clearInput();
            } else {
                this.showModal = true;
            }
        },
        clearInput() {
            this.newTodoItem = '';
        }
    },
    components: {
        TodoModal
    }
}
</script>

<style scoped>
input:focus {
    outline: none;
}
.inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input {
    border-style: none;
    font-size: 0.9rem;
}
.addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.addBtn {
    color: white;
    vertical-align: middle;
}
.closeModalBtn {
    color: #42b983;
}
</style>