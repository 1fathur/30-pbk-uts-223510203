<template>
  <div class="up">
    <h1>Daftar Kegiatan</h1>
    <div>
      <button @click="toggleFilter">{{ filterAktif ? 'Hapus Filter' : 'Filter Belum Selesai' }}</button>
    </div>
    <div class="table-container">
      <table class="table">
        <thead>
          <tr>
            <th>Nama Kegiatan</th>
            <th>Status</th>
            <th>Aksi</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(kegiatan, index) in filteredKegiatan" :key="index">
            <td :class="{ 'selesai': kegiatan.selesai }">{{ kegiatan.nama }}</td>
            <td>{{ kegiatan.selesai ? 'Selesai' : 'Belum Selesai' }}</td>
            <td>
              <button v-if="!kegiatan.selesai" @click="tandaiSelesai(index)">Selesai</button>
              <button v-else @click="batalkanSelesai(index)">Batalkan</button>
              <button @click="hapusKegiatan(index)">Hapus</button>
            </td>
          </tr>
        </tbody>
      </table>

      <div>
        <h2>Tambah Kegiatan Baru</h2>
        <input type="text" v-model="namaKegiatan" placeholder="Nama Kegiatan">
        <button @click="tambahKegiatan">Tambah</button>
      </div>
    </div>
    <div class="background">
      <img src="https://wallpaperwaifu.com/wp-content/uploads/2024/01/giant-whale-swimming-in-a-sea-of-stars-thumb.jpg" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      daftarKegiatan: [
        { nama: 'Belajar Vue.js', selesai: false },
        { nama: 'Menulis laporan proyek', selesai: true },
        { nama: 'Bersih-bersih rumah', selesai: false }
      ],
      namaKegiatan: '',
      filterAktif: false
    };
  },
  computed: {
    filteredKegiatan() {
      if (this.filterAktif) {
        return this.daftarKegiatan.filter(kegiatan => !kegiatan.selesai);
      } else {
        return this.daftarKegiatan;
      }
    }
  },
  methods: {
    tambahKegiatan() {
      if (this.namaKegiatan.trim() !== '') {
        this.daftarKegiatan.push({ nama: this.namaKegiatan, selesai: false });
        this.namaKegiatan = '';
      }
    },
    tandaiSelesai(index) {
      this.daftarKegiatan[index].selesai = true;
    },
    batalkanSelesai(index) {
      this.daftarKegiatan[index].selesai = false;
    },
    hapusKegiatan(index) {
      this.daftarKegiatan.splice(index, 1);
    },
    toggleFilter() {
      this.filterAktif = !this.filterAktif;
    }
  }
};
</script>

<style scoped>
.up{
  margin-top: -200px;
  margin-left: -300px;
}
.table-container {
  backdrop-filter: blur(10px);
  left: 30%;
  top:35%;
  width: 50%;
  position: absolute;
  color: white;
  font-weight: bolder;
}

.table {
  width: 100%;
  border-collapse: collapse;
}

.table th,
.table td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

.selesai {
  text-decoration: line-through;
}

button {
  background-color: #007bff;
  border: none;
  color: white;
  padding: 8px 16px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

.background img{
  position: fixed;
  top: 0;
  left: 0;
  min-height: 90%;
  min-width: 1500px;
  width: 100%;
  height: 100%;
  overflow: hidden;
  z-index: -2;
  object-fit: cover;
  -webkit-background-size:cover; -moz-background-size:cover; -o-background-size:cover; background-size: cover;
  filter: brightness(0.8);
}
</style>
