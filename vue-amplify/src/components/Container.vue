<template>
    <div class="container">
        <transition name="f" appear>
            <form @submit.prevent="Create()">
                <label>New Workout</label>
                <input 
                type="text"
                v-model="msg"
                autocomplete="off"
                >
                <button>Add workout</button>
            </form>
            </transition>
            <ExerciseList
            :ExerciseLists="ExerciseLists"
            :Delete="Delete" />
            <transition name="m" appear>
                <w-notification
                v-show="showNotification"
                warning
                bottom="true"
                round
                shadow
                transition="bounce"
                >
                Please enter a value.
            </w-notification>
            </transition>
    </div>
</template>

<script>
import ExerciseList from './ExerciseList.vue';

export default {
    components: {
        ExerciseList,
    },
    data: () => ({
        msg: "",
        showNotification: false,
        timeout: 2000,
        exampleData: [
            { id: 1, name: 'Item 1' },
            { id: 2, name: 'Item 2' },
            { id: 3, name: 'Item 3' },
        ]
    }),
    methods: {
        Create() {
            setTimeout(() =>
        { this.showNotification = false; }, this.timeout
    );
            if (this.msg.length) {
                let id = Math.floor(Math.random()*100);
                const next = { id, name: this.msg };
                this.ExerciseList.push(next);
            }
        },
        //TODO Define Delete method 6:12
    }
}
</script>

<style>

</style>