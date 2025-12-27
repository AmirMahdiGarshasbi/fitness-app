<script setup>
    import { workoutProgram } from '@/utils';

    defineProps({
        handleSelectWorkout: Function,
        firstIncompleteIndex: Number,
        handleResetPlan: Function
    })

    const workoutTypes = ['Push', 'Pull', 'Legs']

</script>

<template>
    <section id="grid">
        <button :disabled="workoutIdx > 0 && workoutIdx > firstIncompleteIndex" @click="() => handleSelectWorkout(workoutIdx)" :key="workoutIdx" 
        v-for="(workout, workoutIdx) in Object.keys(workoutProgram)" class="card-button plan-card">
            <p>Day {{  workoutIdx < 9 ? '0' + (workoutIdx + 1) :workoutIdx + 1}}</p>
            <h3>{{ workoutTypes[workoutIdx % 3] }}</h3>
        </button>
        <button :disabled="firstIncompleteIndex != -1" @click="handleResetPlan" class="card-button">Reset</button>
    </section>
</template>

<style scoped>
    #grid {
        display: grid;
        grid-template-columns: repeat(3, minmax(0, 1fr));
        gap: 1rem;
    }

    #grid button {
        width: 100%;
    }

    #grid button:disabled {
        box-shadow: none;
        cursor: not-allowed;
    }

    .plan-card {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    @media (min-width: 640px) {
        #grid {
            grid-template-columns: repeat(4, minmax(0, 1fr));
        }
    }
</style>