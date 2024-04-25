<script lang="ts" setup>
const username = ref()
const password = ref()

const router = useRouter()
function submit() {
  const solution = [3, 6, 4, 3, 6, 4, 8, 8]
  console.log('attempt login:', JSON.parse(JSON.stringify(inputCode.value)), JSON.parse(JSON.stringify(solution)))

  for(let i in inputCode.value) {
    if(inputCode.value[i] !== solution[i]) {
      console.log('failed to login, mismatch at position', i)
      return router.push('/failure')
    }
  }
  
  router.push('/success')
}

const inputCode = ref([0,0,0,0,0,0,0,0])
</script>

<template>
  <div class="max-w-xl mx-auto my-20 bg-[#5BF4C7] p-4 rounded shadow">
    <h1 class="text-2xl font-bold text-center">
      Please authenticate by performing your personal dance:
    </h1>

    

    <div v-for="row in 8" class="flex">
      <template v-for="col in 8">
        <img
          :src="`img${col}.png`"
          v-if="inputCode[row-1] === col"
          class="w-12 h-12 border-2 border-blue-500 rounded-md m-2"
          @click="inputCode[row-1] = col "
        >
        <img
          :src="`img${col}.png`"
          v-else
          class="w-12 h-12 border-2 border-gray-500 rounded-md m-2 cursor-pointer"
          @click="inputCode[row-1] = col "
        />
      </template>
    </div>

    <div class="flex flex-col gap-3 mt-5">
      <!-- <label>
        <p class="text-sm mb-1 font-semibold">Username</p>
        <n-input v-model:value="username" />
      </label>

      <label>
        <p class="text-sm mb-1 font-semibold">Super dupering boring password</p>
        <n-input v-model:value="password" type="password" />
      </label> -->

      <n-button type="primary" @click="submit">
        Let's go! 💃🏻
      </n-button>
    </div>
  </div>
</template>
