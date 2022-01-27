<template>
  <div class="q-ma-lg">
    <div v-for="(data, index) in ButtonList" :key="index">
      <q-separator
        v-if="data.annotation && data.annotation == 'divisor'"
        color="white"
        class="q-my-md"
      />
      <q-btn
        v-else
        color="transparent"
        class="full-width"
        align="left"
        unelevated
        :label="data.title"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      ButtonList: [
        {
          title: "Privacy Policy",
        },
        {
          title: "Terms of Services",
        },
        {
          annotation: "divisor",
        },
        {
          title: "About Mark It",
        },
        {
          title: "Help",
        },
      ],
    };
  },
};
</script>
