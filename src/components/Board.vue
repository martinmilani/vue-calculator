<template>
  <div class="grid  grid-cols-4 grid-rows-5">
    <button class="btn-ac" value="ac">
      AC
    </button>

    <button class="btn-text" value="del">
      DEL
    </button>

    <button class="btn-grey-2xl" value="/">
      /
    </button>

    <button class="btn-grey-2xl" value="*">
      *
    </button>

    <button class="btn-white" value="7" @click="handleNumbers">7</button>

    <button class="btn-white" value="8" @click="handleNumbers">8</button>

    <button class="btn-white" value="9" @click="handleNumbers">9</button>

    <button class="btn-plus" value="+">
      +
    </button>

    <button class="btn-white" value="4" @click="handleNumbers">4</button>

    <button class="btn-white" value="5" @click="handleNumbers">5</button>

    <button class="btn-white" value="6" @click="handleNumbers">6</button>

    <button class="btn-white" value="1" @click="handleNumbers">1</button>

    <button class="btn-white" value="2" @click="handleNumbers">2</button>

    <button class="btn-white" value="3" @click="handleNumbers">3</button>

    <button class="btn-grey-2xl" value="-">
      -
    </button>

    <button class="btn-zero" value="0" @click="handleNumbers">0</button>

    <button class="btn-grey-2xl" value=".">
      .
    </button>

    <button class="btn-equal" value="0">
      =
    </button>
  </div>
</template>

<script>
export default {
  props: ["handleNumbers"],
};
</script>

<style>
.btn-equal {
  @apply h-20 bg-gray-100 font-normal text-3xl text-red-500 active:bg-gray-200 font-bold focus:outline-none;
}

.btn-ac {
  @apply h-20 bg-gray-100 font-normal text-xl text-red-500 active:bg-gray-200 font-bold focus:outline-none;
}

.btn-white {
  @apply font-normal text-xl active:bg-gray-50 focus:outline-none;
}
.btn-zero {
  @apply col-span-2 font-normal text-xl active:bg-gray-50 focus:outline-none;
}
.btn-grey-2xl {
  @apply h-20 bg-gray-100 font-normal text-2xl active:bg-gray-200 focus:outline-none;
}
.btn-text {
  @apply h-20 bg-gray-100 font-normal text-xl active:bg-gray-200 focus:outline-none;
}
.btn-plus {
  @apply col-start-4 col-end-4 row-start-2 row-end-4 bg-gray-100 font-normal text-xl active:bg-gray-200 focus:outline-none;
}
</style>
