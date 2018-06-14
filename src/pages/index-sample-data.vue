<template>
  <q-table
    title="Table Title"
    :data="tableData"
    :columns="columns"
    row-key="name"
  />
</template>

<script>
import axios from 'axios'
import tableData from 'assets/table-data'
export default {
  data () {
    return {
      bikeData: null, 
      tableData,
      columns: [
        {
          name: 'desc',
          required: true,
          label: 'Dessert (100g serving)',
          align: 'left',
          field: 'name',
          sortable: true
        },
        { name: 'calories', label: 'Calories', field: 'calories', sortable: true },
        { name: 'fat', label: 'Fat (g)', field: 'fat', sortable: true },
        { name: 'carbs', label: 'Carbs (g)', field: 'carbs', sortable: true },
        { name: 'protein', label: 'Protein (g)', field: 'protein', sortable: true },
        { name: 'sodium', label: 'Sodium (mg)', field: 'sodium', sortable: true },
        { name: 'calcium', label: 'Calcium (%)', field: 'calcium', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10) },
        { name: 'iron', label: 'Iron (%)', field: 'iron', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10) }
      ],
      filter: '',
      visibleColumns: ['desc', 'fat', 'carbs', 'protein', 'sodium', 'calcium', 'iron'],
      separator: 'horizontal',
      selection: 'multiple',
      selected: [
        // initial selection
        { name: 'Ice cream sandwich' }
      ],
      pagination: {
        page: 2
      },
      paginationControl: { rowsPerPage: 3, page: 1 },
      loading: false,
      dark: true,
      selectedSecond: [
        { name: 'Eclair' }
      ]
    }
  },
  watch: {
    'paginationControl.page' (page) {
      this.$q.notify({
        color: 'secondary',
        message: `Navigated to page ${page}`,
        actions: page < 4
          ? [{
            label: 'Go to last page',
            handler: () => {
              this.paginationControl.page = 4
            }
          }]
          : null
      })
    }
  },
  computed: {
    tableClass () {
      if (this.dark) {
        return 'bg-black'
      }
    }
  },
  mounted () {
    this.getData();
  },
  methods: {
    getData () {
      let _this = this;
      axios.get('https://api.coord.co/v1/bike/location?access_key=p9H_wRiQaoEoIKQBaJnA1oR77yCBY-6Z-AEku8bgJNk&latitude=33.7490&longitude=-84.3880&radius_km=10')
      .then(function (response) {
        console.log(response);
        _this.bikeData = response.data.features;
      })
    },
    deleteRow () {
      this.$q.notify({
        color: 'secondary',
        icon: 'delete',
        message: `Will delete the selected row${this.selectedSecond.length > 1 ? 's' : ''} later, ok?`
      })
    }
  }
}
</script>
