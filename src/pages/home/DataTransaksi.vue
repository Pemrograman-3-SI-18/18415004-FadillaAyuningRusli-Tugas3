<template>
  <div class="q-pa-md">
    <q-table
      title="Treats"
      :data="data"
      :columns="columns"
      row-key="id"
      :filter="filter"
      :loading="loading"
    >

      <template v-slot:top>
        <span class="text-h5 text-weight-light q-pa-md">
        <span class="text-blue-grey-14">Data Transaksi</span>
      </span>
        <q-space/>
        <q-input borderless dense debounce="300" color="primary" v-model="filter">
          <template v-slot:append>
            <q-icon name="search" />
          </template>
        </q-input>
      </template>

    </q-table>
  </div>
</template>

<script>
export default {
  data () {
    return {
      loading: false,
      filter: '',
      rowCount: 10,
      columns: [
        {
          name: 'desc',
          required: true,
          label: 'Kode Transaksi',
          align: 'left',
          field: row => row.kodeTransaksi,
          format: val => `${val}`,
          sortable: true
        },
        { name: 'namaPembeli', align: 'center', label: 'Nama Pembeli', field: 'namaPembeli', sortable: true },
        { name: 'judulBuku', label: 'Judul Buku', align: 'center', field: 'judulBuku' },
        { name: 'hargaBuku', label: 'Harga Buku', align: 'center', field: 'hargaBuku' },
        { name: 'jumlahBeli', label: 'Jumlah Beli', align: 'center', field: 'jumlahBeli' },
        { name: 'total', label: 'Total', align: 'center', field: 'total' }
      ],
      data: [
        {
          kodeTransaksi: 'K001',
          namaPembeli: 'Fadilla AR',
          judulBuku: 'Pemograman 3',
          hargaBuku: '60000',
          jumlahBeli: '5',
          total: '300000'
        },
        {
          kodeTransaksi: 'K002',
          namaPembeli: 'Ferry',
          judulBuku: 'Pemograman 3',
          hargaBuku: '50000',
          jumlahBeli: '5',
          total: '250000'
        },
        {
          kodeTransaksi: 'K003',
          namaPembeli: 'Nyunyun',
          judulBuku: 'Pemograman 3',
          hargaBuku: '50000',
          jumlahBeli: '1',
          total: '50000'
        }
      ]
    }
  },

  methods: {
    // emulate fetching data from server
    addRow () {
      this.loading = true
      setTimeout(() => {
        const
          index = Math.floor(Math.random() * (this.data.length + 1)),
          row = this.original[Math.floor(Math.random() * this.original.length)]
        if (this.data.length === 0) {
          this.rowCount = 0
        }
        row.id = ++this.rowCount
        const addRow = { ...row } // extend({}, row, { name: `${row.name} (${row.__count})` })
        this.data = [...this.data.slice(0, index), addRow, ...this.data.slice(index)]
        this.loading = false
      }, 500)
    },

    removeRow () {
      this.loading = true
      setTimeout(() => {
        const index = Math.floor(Math.random() * this.data.length)
        this.data = [...this.data.slice(0, index), ...this.data.slice(index + 1)]
        this.loading = false
      }, 500)
    }
  }
}
</script>

<style scoped>

</style>
