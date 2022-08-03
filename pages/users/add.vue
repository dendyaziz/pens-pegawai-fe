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

            <!-- Ini field input password -->
            <b-form-group label="Password">
                <b-form-input v-model="password" type="password" required></b-form-input>
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
      username: '',
      password: ''
    }
  },
  methods: {
    async onSubmit() {
        await this.$axios.$post('http://localhost:8000/api/users', {
            name: this.name,
            email: this.email,
            username: this.username,
            password: this.password
        })

        // tampilkan pesan sukses
        this.$root.$bvToast.toast('Pegawai berhasil ditambah', {
            title: 'Sukses!',
        })

        // redirect je halaman tabel pegawai
        this.$router.push('/users')
    }
  }
}
</script>
