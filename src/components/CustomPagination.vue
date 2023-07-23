<template>
  <div>
    <vs-table>
      <template #thead>
        <vs-tr>
          <vs-th> Date </vs-th>
          <vs-th> Description </vs-th>
          <vs-th> Type </vs-th>
          <vs-th> Status </vs-th>
        </vs-tr>
      </template>
      <template #tbody>
        <vs-tr :key="i" v-for="(tr, i) in displayedLogs" :data="tr">
          <vs-td>
            {{ tr.dateLog }}
          </vs-td>
          <vs-td>
            {{ tr.descript }}
          </vs-td>
          <vs-td>
            {{ tr.type }}
          </vs-td>
          <vs-td>
            {{ tr.status }}
          </vs-td>
        </vs-tr>
      </template>
    </vs-table>
    <vs-pagination
      v-model="currentPage"
      :length="totalPages"
      @change="onChangePage"
    />
  </div>
</template>

<script>
export default {
  props: {
    logs: {
      type: Array,
      required: true,
    },
    itemsPerPage: {
      type: Number,
      default: 10,
    },
  },
  data() {
    return {
      currentPage: 1,
    };
  },
  computed: {
    totalPages() {
      return Math.ceil(this.logs.length / this.itemsPerPage);
    },
    displayedLogs() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage;
      const endIndex = startIndex + this.itemsPerPage;
      return this.logs.slice(startIndex, endIndex);
    },
  },
  methods: {
    onChangePage(page) {
      this.currentPage = page;
    },
  },
};
</script>
