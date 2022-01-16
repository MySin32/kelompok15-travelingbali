<template>
  <div class="container" style="margin-top: 130px;">
    <router-link to="/editdetailkategori" class="btn btn-warning"><span class="fa fa-arrow-left"></span></router-link>
    <div class="card">
      <div class="card-header">
        <h1>Tambah Detail Kategori</h1>
      </div>
      <div class="card-body">
        <form>
          <div class="form-group">
            <label for="exampleFormControlInput1">Kategori</label>
            <select class="form-select" aria-label="Default select example" name="id_kategori" v-model="form.id_kategori">
              <option v-for="(kategori, index) in kategoris"
                :key="index"
                >{{ kategori.id }}</option>
            </select>
          </div>
          <div class="form-group">
            <label for="exampleFormControlInput1">Nama</label>
            <input type="text" class="form-control" name="nama" v-model="form.nama"/>
          </div>
          <div class="form-group">
            <label for="exampleFormControlInput1">Alamat</label>
            <input type="text" class="form-control" name="alamat" v-model="form.alamat"/>
          </div>
          <div class="form-group">
            <label for="exampleFormControlFile1">Image</label>
            <input
              type="file"
              class="form-control-file"
              id="exampleFormControlFile1"
              v-on:change="upload"
            />
          </div>
          <div class="form-floating">
            <textarea
              class="form-control"
              placeholder="Leave a comment here"
              id="floatingTextarea2"
              style="height: 100px"
              name="deskripsi"
              v-model="form.deskripsi"
            ></textarea>
            <label for="floatingTextarea2">Deskripsi</label>
          </div>
          <button class="btn btn-success" type="submit" @click="savekategoridetail">Tambah</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import Kategoridetail from "../../services/kategoridetail.service";
import Kategori from "../../services/kategori.service";
export default {
  name: "Editkategori",
  data() {
    return {
      kategoris:[],
          form:{
              id_kategori:"",
              nama:"",
              alamat:"",
              image:"",
              Deskripsi:"",
          }
    };
  },
  mounted() {
    this.retrievekategoris();
  },
  methods: {
    upload: function(event){
      const namagambar = event.target.files[0].name
      this.form.image=namagambar
    },
    // save comments
    savekategoridetail() {
      var data = {
        id_kategori: this.form.id_kategori,
        nama: this.form.nama,
        alamat: this.form.alamat,
        image: this.form.image,
        deskripsi: this.form.deskripsi,
      };

      Kategoridetail.create(data)
        .then((response) => {
          console.log(response.data);
        })
        .catch((e) => {
          console.log(e);
        });
    },
      retrievekategoris() {
          Kategori.getAll()
              .then(response => {
              this.kategoris = response.data;
              console.log(response.data);
              })
              .catch(e => {
              console.log(e);
              });
          },
  },
};
</script>
