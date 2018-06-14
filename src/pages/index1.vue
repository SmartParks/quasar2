<template>
  <q-table
    title="Table Title"
    :data="tableData"
    :columns="columns"
    row-key="name"
  />
</template>

<script>
export default {
  data: () => ({
    columns: [
      {
        name: 'name',
        required: true,
        label: 'Dessert (100g serving)',
        align: 'left',
        field: 'name',
        sortable: true
      },
      {
        name: 'calories',
        required: true,
        label: 'Next',
        align: 'left',
        field: 'name',
        sortable: true
      },
      {
        name: 'fat',
        required: true,
        label: 'Right',
        align: 'right',
        field: 'name',
        sortable: true
      }
    ],
    tableData: [
      {
        name: 'Frozen Yogurt',
        calories: 159,
        fat: 6.0,
        carbs: 24,
        protein: 4.0,
        sodium: 87,
        calcium: '14%',
        iron: '1%'
      },
      {
        name: 'Carrots',
        calories: 159,
        fat: 6.0,
        carbs: 24,
        protein: 4.0,
        sodium: 87,
        calcium: '14%',
        iron: '1%'
      },
      {
        name: 'Bread',
        calories: 159,
        fat: 6.0,
        carbs: 24,
        protein: 4.0,
        sodium: 87,
        calcium: '14%',
        iron: '1%'
      }
    ],
    color: [
    	{
    		color: '#ddd'
    	}
    ]
  })
}
</script>
