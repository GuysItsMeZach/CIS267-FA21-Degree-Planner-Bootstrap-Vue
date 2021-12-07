<template>
  <div class="section">
    <div class="accordion-item">
      <h2
        class="accordion-header"
        :id="schedule.id"
        v-b-toggle:[schedule.collapseId]
      >
        <div class="d-flex flex-row justify-content-between px-2">
          <div>
            <h4 class="my-0">{{ schedule.name }}</h4>
          </div>
          
        </div>
      </h2>
      <b-collapse :id="schedule.collapseId">
        <div class="accordion-body">
          <table class="table table-hover">
            <thead>
              <th>Courses</th>
              <td></td>
              <td></td>
              <th>Credits</th>
            </thead>
            <tr
              class="makehover"
              v-for="c in schedule.classes"
              :key="c.id"
              @click="remove(c.id, schedule)"
            >
              <td>{{ c.id }}</td>
              <td>
                <span class="fw-bold">{{ c.name }} </span>
              </td>
              <td>
                <span v-if="c.category == 'LAC'" class="badge bg-primary">
                  {{ c.category }}
                </span>
                <span v-else class="badge bg-secondary">
                  {{ c.category }}
                </span>
              </td>
              <td>{{ c.hours }}</td>
            </tr>
            <tr>
              <td></td>
              <td></td>
              <td></td>
              <td class="fw-bold">{{ schedule.total }}</td>
            </tr>
          </table>
        </div>
      </b-collapse>
    </div>
  </div>
</template>

<script>
export default {
  name: "SemesterSchedule",
  props: { schedule: Object },
  methods: {
    remove(id, schedule) {
        this.$emit("remove-course", id, schedule);
    },
  },
};
</script>

<style>
.section {
  padding-top: 1vh;
}

</style>