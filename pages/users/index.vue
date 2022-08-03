<template>
    <div>
        <b-container>
            <h1>Ini Table Pegawai</h1>

            <NuxtLink to="/users/add"><b-button>Tambah Pegawai</b-button></NuxtLink>

            <b-table striped hover :items="users">
                <!-- Custom kolom actions-->
                <template #cell(actions)="row">
                    <nuxt-link :to="`/users/edit/${row.item.id}`">
                        <b-button>Edit</b-button>
                    </nuxt-link>

                    <b-button variant="danger" @click="deleteUser(row.item.id)">Hapus</b-button>
                </template>
            </b-table>
        </b-container>
    </div>
</template>

<script>
  export default {
    data() {
      return {
        users: []
      }
    },
    mounted() {
        this.getUsers()
    },
    methods: {
        async getUsers() {
            this.users = await this.$axios.$get('http://localhost:8000/api/users')

            // tambah kolom actions ke this.users
            this.users = this.users.map(item => ({
                ...item,
                actions: '',
            }))
        },
        async deleteUser(id) {
            await this.$axios.$delete(`http://localhost:8000/api/users/${id}`)

            // tampilkan pesan sukses
            this.$bvToast.toast('Pegawai berhasil dihapus', {
                title: 'Sukses!',
            })

            // load ulang users
            this.getUsers()
        }
    }
  }
</script>