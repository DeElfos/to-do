<template>
  <q-page>
    <div align="center" class="text-h4 q-mt-lg text-weight-bolder">
      Today's To Do List
    </div>

    <NewTask :groups="lists" @newData="newData" />
    <div v-for="(data, index) in mapData" :key="index">
      <CardTitle :title="data.label" />
      <CardTask
        :filter="index"
        :cardInfo="returnDataInfo"
        :groups="lists"
        @changeData="changeData"
      />
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

import CardTitle from "components/TaskTitle.vue";
import CardTask from "components/TaskCard.vue";
import NewTask from "components/newTask.vue";

export default defineComponent({
  name: "PageIndex",
  computed: {
    returnDataInfo() {
      console.log("entrou");
      return this.cardInfo;
    },
    mapData() {
      this.cardInfo;
      return this.lists;
    },
  },
  methods: {
    changeData(dataChanged) {
      this.cardInfo[dataChanged.index] = dataChanged.data;
    },
    newData(dataChanged) {
      this.cardInfo.push(dataChanged.data);
    },
  },
  data() {
    return {
      lists: [
        {
          label: "Main priority",
          value: 0,
        },
        {
          label: "Other tasks",
          value: 1,
        },
      ],
      cardInfo: [
        {
          taskName: "Escrever um post para o blog",
          description: "Criar um estudo de caso para mostrar no blog",
          status: 0,
          section: 0,
        },
        {
          taskName: "Editar vídeo",
          description:
            "Fazer um vídeo de apresentação para este aplicativo e editar",
          status: 0,
          section: 0,
        },
        {
          taskName: "Mostrar texto grande",
          description:
            "Sed id est a eros pretium condimentum eu ac elit. Etiam sollicitudin lobortis lacus non aliquet. Nam condimentum malesuada urna eget imperdiet. Sed nisi orci, congue vitae turpis ut, pretium commodo ex. Maecenas nec velit ultrices, hendrerit metus bibendum, tincidunt urna. Mauris vestibulum facilisis urna, sed pulvinar ante consectetur a. Nunc in pellentesque tortor. Fusce fringilla metus a vehicula ultricies. Morbi dignissim eleifend hendrerit. Aliquam egestas orci sapien, sed maximus metus elementum ac. Vivamus ultricies semper malesuada. Nam gravida nisi ipsum. Pellentesque urna tortor, sodales et risus sit amet, pulvinar euismod elit. Maecenas pretium, ligula ut feugiat malesuada, felis nibh tempus diam, ut dapibus metus justo quis mi. Donec rhoncus velit non ante ullamcorper efficitur. Sed ut ex in mi tempus luctus quis nec ipsum.",
          status: 0,
          section: 1,
        },
      ],
    };
  },
  components: {
    CardTitle,
    NewTask,
    CardTask,
  },
});
</script>
