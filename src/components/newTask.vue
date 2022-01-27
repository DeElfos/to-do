<template>
  <div>
    <q-page-sticky
      position="bottom-right"
      :offset="[18, 18]"
      style="z-index: 2"
      @click="openDialog = !openDialog"
    >
      <q-btn fab icon="add" color="accent" />
    </q-page-sticky>

    <q-dialog v-model="openDialog" full-width>
      <q-card class="border-radius">
        <q-card-section>
          <div class="text-h6" align="center">Edit Task</div>
        </q-card-section>

        <q-card-section class="q-pt-none q-mt-md">
          <div class="text-subtitle">Title</div>
          <q-input filled v-model="tempTitle" />
        </q-card-section>

        <q-card-section class="q-pt-none q-mt-md">
          <div class="text-subtitle">Description</div>
          <q-input filled v-model="tempDescription" />
        </q-card-section>

        <q-card-section class="q-pt-none q-mt-md row">
          <div
            class="col-12 q-ma-sm"
            v-for="(data, index) in status"
            :key="index"
          >
            <q-btn
              :label="data"
              class="full-width"
              @click="tempStatus = parseInt(index)"
              :disable="parseInt(index) == this.tempStatus"
              :color="parseInt(index) == this.tempStatus ? 'accent' : 'primary'"
            />
          </div>
        </q-card-section>

        <q-card-section>
          <q-select
            outlined
            v-model="tempSection"
            :options="groups"
            label="Group"
          />
        </q-card-section>

        <q-card-actions class="row justify-between q-mx-md q-mb-xs">
          <q-btn outline color="negative" label="Cancel" @click="cancelEdit" />
          <q-btn outline color="positive" label="OK" @click="saveEdit" />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </div>
</template>

<script>
export default {
  props: {
    groups: Object,
  },
  emits: ["newData"],
  data() {
    return {
      tempTitle: "",
      tempDescription: "",
      tempStatus: 0,
      tempIndex: "",
      tempSection: this.groups[0],

      openDialog: false,
      status: ["NEXT", "IN PROGRESS", "COMPLETED"],
    };
  },
  methods: {
      openData() {
      this.openDialog = true;
    },
    cancelEdit() {
    //   this.tempTitle = "";
    //   this.tempDescription = "";
    //   this.tempStatus = "";
    //   this.tempSection = "";

      this.openDialog = false;
    },
    saveEdit() {
      let newInfo = {
        taskName: this.tempTitle,
        description: this.tempDescription,
        status: this.tempStatus,
        section: this.tempSection.value,
      };

      this.$emit("newData", { data: newInfo, index: this.tempIndex });

      this.openDialog = false;
    },
  },

};
</script>
