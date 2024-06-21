<script setup>
    import {ref} from 'vue'

    // JSON 
    const questions = ref([
        {
            question : "Cuanto es 1+1",
            answers: [
                {answer: 2, correct: true},
                {answer: 3, correct: false},
                {answer: 4, correct: false},
                {answer: 1, correct: false},
            ]
        },
        {
            question : "Cuanto es 1+1",
            answers: [
                {answer: 2, correct: true},
                {answer: 3, correct: false},
                {answer: 4, correct: false},
                {answer: 1, correct: false},
            ]
        },
        {
            question : "Cuanto es 1+1",
            answers: [
                {answer: 2, correct: true},
                {answer: 3, correct: false},
                {answer: 4, correct: false},
                {answer: 1, correct: false},
            ]
        }
    ])

    const questionIndex = ref(0)
    const correctAnswer = ref(0)
    const wrongAnswer = ref(0)
    const isAnswered = ref(false)
    const isCorrect = ref(false)

    function selectedAnswer(answer){
        if(!isAnswered.value){
            isAnswered.value = true
            isCorrect.value = answer.correct
            if(answer.correct){
                correctAnswer.value++
            }else{
                wrongAnswer.value++
            }
        }
    }

    function next(){
        isAnswered.value = false
        isCorrect.value = false
        questionIndex.value++
    }

</script>

<template>
    <div class="flex justify-center content-center mt-8">
        <div class="space-y6 bg-gray-100 rounded-lg p-8">
            <p class="flex items-center justify-center">{{ questions[questionIndex].question }}</p>
            <div
                :class="{
                    'bg-blue-300': !isAnswered,
                    'bg-green-300': isAnswered && isCorrect,
                    'bg-red-300': isAnswered && !isCorrect
                }"
                class="w-[300px] h-[200px] flex justify-center items-center ml-[20%] select-none"
            >
                UFPSO
            </div>
            <div class="grid grid-cols-2 space-y-1">
                <div v-for="(answer,index) in questions[questionIndex].answers" :key="index">
                    <span @click="selectedAnswer(answer) " class="bg-purple-200 w-[200px] hover:bg-red-300 h-[50px] justify-center items-center flex select-none">
                        {{ answer.answer }}
                    </span>
                </div>
            </div>
            <button @click="next" class="bg-purple-300 rounded-lgp-1 ml-[350px]">Siguiente</button>
            <p>Respuestas correctas: {{ correctAnswer }}</p>
            <p>Respuestas incorrectas: {{ wrongAnswer }}</p>
        </div>
    </div>

</template>