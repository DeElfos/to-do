<template>
  <q-list>
    <div
      v-for="(data, index) in essentialLinks"
      :key="data.title"
      v-bind="index"
    >
      <q-item clickable tag="a" target="_blank" :href="data.link">
        <q-item-section v-if="data.icon" avatar>
          <q-icon :name="data.icon" />
        </q-item-section>

        <q-item-section>
          <q-item-label>{{ data.title }}</q-item-label>
          <q-item-label caption>
            {{ data.caption }}
          </q-item-label>
        </q-item-section>
      </q-item>
    </div>
  </q-list>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "EssentialLink",
  data() {
    return {
      essentialLinks: [
        {
          title: "Docs",
          caption: "quasar.dev",
          icon: "school",
          link: "https://quasar.dev",
        }
      ],
    };
  },
});
</script>
