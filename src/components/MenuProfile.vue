<template>
  <div align="center">
    <q-avatar size="100px" class="q-ma-md q-mt-lg">
      <img src="https://cdn.quasar.dev/img/avatar.png" />
    </q-avatar>

    <div class="text-h5 text-primary text-weight-bold">
      {{ user_name }}
    </div>

    <div class="q-pb-lg">
      {{ user_email }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user_name: "Marcos Filho",
      user_email: "santosefilhomarcos@gmail.com",
    };
  },
};
</script>
