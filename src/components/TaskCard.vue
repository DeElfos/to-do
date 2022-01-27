<template>
  <div
    v-for="(data, index) in returnCardInfo"
    :key="index"
    @click="openData(index)"
  >
    <q-card
      class="my-card q-ma-lg border-radius back-primary"
      v-if="data.section == filter"
    >
      <q-card-section>
        <div class="row">
          <div class="col-12 text-weight-bolder text-h6 text-primary">
            {{ data.taskName }}
          </div>

          <div class="col-12 q-pt-sm ellipsis-2-lines">
            {{ data.description }}
          </div>

          <div class="col-12 q-pt-md text-subtitle1">
            Status:
            <span class="text-primary text-weight-bolder">
              {{ status[data.status] }}
            </span>
          </div>
        </div>
      </q-card-section>
    </q-card>

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
  methods: {
    openData(index) {
      this.tempTitle = this.cardInfo[index].taskName;
      this.tempDescription = this.cardInfo[index].description;
      this.tempStatus = this.cardInfo[index].status;
      this.tempIndex = index;
      this.tempSection = this.groups[this.cardInfo[index].section];

      this.openDialog = true;
    },
    cancelEdit() {
      this.tempTitle = "";
      this.tempDescription = "";
      this.tempStatus = "";
      this.tempSection = "";

      this.openDialog = false;
    },
    saveEdit() {
      let newInfo = {
        taskName: this.tempTitle,
        description: this.tempDescription,
        status: this.tempStatus,
        section: this.tempSection.value,
      };

      this.$emit("changeData", { data: newInfo, index: this.tempIndex });

      this.openDialog = false;
    },
  },

  emits: ["changeData"],
  props: {
    cardInfo: Object,
    filter: Number,
    groups: Object,
  },

  computed: {
    returnCardInfo() {
      return this.cardInfo;
    },
  },
  data() {
    return {
      tempTitle: "",
      tempDescription: "",
      tempStatus: "",
      tempIndex: "",
      tempSection: "",

      openDialog: false,
      status: ["NEXT", "IN PROGRESS", "COMPLETED"],
    };
  },
};
</script>
