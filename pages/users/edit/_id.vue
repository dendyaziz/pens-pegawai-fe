<template>
    <b-container>
        <h1 class="mt-5">Tambah Pegawai</h1>

        <b-form @submit.prevent="onSubmit">
            <!-- Ini field input nama -->
            <b-form-group label="Nama">
                <b-form-input v-model="name" required></b-form-input>
            </b-form-group>

            <!-- Ini field input email -->
            <b-form-group label="Email">
                <b-form-input v-model="email" type="email" required></b-form-input>
            </b-form-group>

            <!-- Ini field input username -->
            <b-form-group label="Username">
                <b-form-input v-model="username" required></b-form-input>
            </b-form-group>

            <b-button variant="primary" type="submit">Simpan</b-button>
        </b-form>
    </b-container>
</template>

<script>
export default {
  data () {
    return {
      name: '',
      email: '',
      username: ''
    }
  },
  mounted() {
    this.getUser()
  },
  methods: {
    async onSubmit() {
        const id = this.$route.params.id
        await this.$axios.$put(`http://localhost:8000/api/users/${id}`, {
            name: this.name,
            email: this.email,
            username: this.username
        })

        // tampilkan pesan sukses
        this.$root.$bvToast.toast('Pegawai berhasil diubah', {
            title: 'Sukses!',
        })

        // redirect je halaman tabel pegawai
        this.$router.push('/users')
    },
    async getUser() {
        const id = this.$route.params.id
        const user = await this.$axios.$get(`http://localhost:8000/api/users/${id}`)
    
        this.name = user.name
        this.email = user.email
        this.username = user.username
    }
  }
}
</script>
