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
        ],
        ExerciseLists: []
    }),
    methods: {
        Create() {
            setTimeout(() =>
        { this.showNotification = false; }, this.timeout
    );

            if (this.msg.length) {
                let id = Math.floor(Math.random()*100);
                const next = { id, name: this.msg };
                this.ExerciseLists.push(next);
            }
            else {
                this.showNotification = true;
            }
        },
        //TODO Define Delete method 6:12
        Delete(idx) {
            this.ExerciseLists = this.ExerciseLists.filter(
                (r) => r.id !== idx
            )
        }
    }
}
</script>

<style scoped>
  .f-enter-from,
  .f-leave-to {
    opacity: 0;
    transform: translateX(-40px);
  }
  .f-enter-to,
  .f-leave-from {
    opacity: 1;
    transform: translateX(0px);
  }
  .f-enter-active,
  .f-leave-active {
    transition: all 0.5s ease;
  }
  .m-enter-active {
    animation: shake 0.5s ease-in;
  }
  @keyframes shake {
    0% { transform: translateX(-40px); opacity: 0; }
    25% { transform: translateX(-10px); opacity: 1; }
    50% { transform: translateY(-40px); }
    75% { transform: translateY(0px);}
    100% { transform: translateX(0px); }
  }
</style>