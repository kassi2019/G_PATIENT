
<template>
  <div class="main-content-container container-fluid px-4">
    <h3 style="text-align:center">Listes des Articles</h3>
    <div class="container center">
      <br />
      <div class="row">
        <div class="col-lg-5 col-md-5 col-sm-5" style="padding-bottom: 10px;"></div>
        <div class="col-lg-5 col-md-5 col-sm-5" style="padding-bottom: 10px;"></div>
        <div class="col-lg-2 col-md-2 col-sm-42" style="padding-bottom: 10px;">
          <div class="div-action pull pull-right" style="padding-bottom:5px;">
            <br />
            <button
              type="button"
              class="btn btn-primary btn"
              data-toggle="modal"
              data-target="#exampleModal"
            >Nouveau</button>
          </div>
        </div>
      </div>
    </div>
    <div
      class="modal fade"
      id="exampleModal"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-lg" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h4 class="modal-title" id="exampleModalLabel">Formulaire Articles</h4>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">×</span>
            </button>
          </div>
          <form @submit.prevent="creearticle">
            <div class="modal-body">
              <div class="modal-body" style="padding: 5px;">
                <div class="row">
                  <div class="col-lg-12 col-md-12 col-sm-12" style="padding-bottom: 10px;">
                    <div class="form-group">
                      <label>Titre Article</label>
                      <input
                        class="form-control"
                        placeholder="Titre Article"
                        type="text"
                        v-model="chmpajout.titre"
                        required
                        autofocus
                      />
                    </div>
                  </div>
                </div>
                <div class="row">
                  <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                    <div class="form-group">
                      <label>Contenu Article</label>
                      <input
                        class="form-control"
                        placeholder="Contenu Article"
                        type="text"
                        v-model="chmpajout.contenu"
                        required
                        autofocus
                      />
                    </div>
                  </div>
                  <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                    <div class="form-group">
                      <label>Fournisseur</label>
                      <select
                        id="statut_id"
                        v-model="chmpajout.user"
                        class="form-control form-control-sm"
                      >
                        <option v-for="option in users" :key="option.id"></option>
                      </select>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="modal-footer">
              <button type="submit" class="btn btn-success">Enregistrer</button>
              <button type="button" class="btn btn-danger" data-dismiss="modal">Fermer</button>
            </div>
          </form>
        </div>
      </div>
    </div>

    <div class="table-responsive">
      <br />

      <table class="table table-bordered">
        <thead>
          <tr>
            <th>index</th>
            <th>Titre</th>
            <th>Contenu</th>
            <th>Fournisseur</th>
            <th>Modifier</th>
            <th>Supprimer</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(article,index) in tblearticle" :key="article.id">
            <td>{{index}}</td>
            <td>{{article.titre}}</td>
            <td>{{article.contenu}}</td>
            <td>{{article.user}}</td>
            <td style="text-align:center">
              <button @click="showedit(index)" class="btn btn-info">Modifier</button>
            </td>
            <td style="text-align:center">
              <button class="btn btn-danger" @click="Deletedata(index, article.id)">Supprimer</button>
            </td>
          </tr>
        </tbody>
      </table>
      <div v-if="tblearticle.length"></div>
      <div v-else>
        <p style="text-align:center;font-size:30px;color:red;">Aucun Article Enregistrer</p>
      </div>
      <!--debut modal modifier-->
      <div
        class="modal fade"
        id="modifierModal"
        tabindex="-1"
        role="dialog"
        aria-labelledby="exampleModalLabel"
        aria-hidden="true"
      >
        <div class="modal-dialog modal-lg" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h4 class="modal-title" id="exampleModalLabel">Formulaire de Modification</h4>
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">×</span>
              </button>
            </div>
            <form @submit.prevent="modifierarticle">
              <div class="modal-body">
                <div class="modal-body" style="padding: 5px;">
                  <div class="row">
                    <div class="col-lg-12 col-md-12 col-sm-12" style="padding-bottom: 10px;">
                      <div class="form-group">
                        <label>Titre Article</label>
                        <input
                          class="form-control"
                          placeholder="Nom personnel"
                          type="text"
                          v-model="chmpajout.titre"
                          required
                          autofocus
                        />
                      </div>
                    </div>
                  </div>
                  <div class="row">
                    <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                      <div class="form-group">
                        <label>Contenu Article</label>
                        <input
                          class="form-control"
                          placeholder="Prenoms personnel"
                          type="text"
                          v-model="chmpajout.contenu"
                          required
                          autofocus
                        />
                      </div>
                    </div>
                    <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                      <div class="form-group">
                        <label>Fournisseur</label>
                        <select
                          id="statut_id"
                          v-model="chmpajout.user"
                          class="form-control form-control-sm"
                        >
                          <!-- <option v-for:"option in users" :key="option.id">
                                {{option.libelle}}
                          </option>-->
                        </select>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="modal-footer">
                <button type="submit" class="btn btn-success">Enregistrer</button>
                <button type="button" class="btn btn-danger" data-dismiss="modal">Fermer</button>
              </div>
            </form>
          </div>
        </div>
      </div>
      <!--fin modal modifier-->
    </div>
  </div>
</template>
  
<script>
export default {
  data() {
    return {
      tblearticle: [],
      selection: [],
      users: [],

      //id: "",
      chmpajout: {
        titre: "",
        contenu: "",
        user: ""
      },
      chmpmof: {
        titre: "",
        contenu: "",
        user: ""
      },
      selectAll: false,
      search: "",
      statut: "",
      stats: ["Marie", "Celibataire", "Divorcé"]
    };
  },
  created() {
    this.afficher();
    //this.creerfonction();
    //this.reset();
  },
  computed: {},
  mounted() {
    this.comboxuser();
  },
  methods: {
    reset() {
      this.chmpajout.titre = "";
      this.chmpajout.contenu = "";
      this.chmpajout.user = "";
    },
    reset1() {
      this.chmpajout.titre = "";
      this.chmpajout.contenu = "";
      this.chmpajout.user = "";
    },
    comboxuser() {
      axios.get("api/kassi/parametre/listearticle").then(
        response =>
          (users = _map(response.data.users, function(data) {
            return_.pick(data, "libelle", "id");
          }))
      );
    },
    //method d'insertion des données
    creearticle() {
      // console.log("salut toi");
      axios
        .post("api/ajouterarticle", {
          titre: this.chmpajout.titre,
          contenu: this.chmpajout.contenu,
          user: this.chmpajout.user
        })
        .then(response => {
          Swal.fire({
            position: "top-end",
            type: "success",
            title: "Enregistrement Reussi",
            showConfirmButton: false,
            timer: 3000
          });
          this.reset();
          this.afficher();
        });
      // console.log(this.code, this.libelle);
    },
    /*modedit(id) {
      axios.get("api/affiche_edit/" + id + "/edit").then(response => {
        this.tblearticle = response.data.personnels;
      });length
    },*/
    showedit(index) {
      // console.log("rrrrrrr");
      $("#modifierModal").modal();
      this.chmpmof = this.tblearticle[index];
      console.log(this.chmpmof);
    },
    modifierarticle(index) {
      //console.log(this.id);
      axios
        .put("api/modifierarticle/" + this.chmpmof.id, {
          titre: this.chmpmof.titre,
          contenu: this.chmpmof.contenu,
          user: this.chmpmof.user
        })
        .then(response => {
          console.log();

          Swal.fire({
            position: "top-end",
            type: "success",
            title: "Modification Reussi",
            showConfirmButton: false,
            timer: 3000
          });

          this.reset1();
          this.afficher();
          //this.modoEditar = false;
        });
    },
    Deletedata(index, id) {
      let conf = confirm("Etes vous sûre de supprimer ");
      if (conf === true) {
        this.tblearticle.splice(index, 1);
        axios
          .delete("api/suparticle/" + id)

          .then(response => {
            /* .then(data => {*/
            console.log();
            Swal.fire({
              position: "top-end",
              type: "success",
              title: "Suppression Reussi",
              showConfirmButton: false,
              timer: 3000
            });
            this.afficher();
          })
          .catch(err => console.log(err));
      }
    },

    //changerstatut() {},
    afficher() {
      axios.get("api/kassi/parametre/listearticle").then(response => {
        this.tblearticle = response.data.Articles;
      });
    }
  },
  Deletedata(index, id) {
    let conf = confirm("Etes vous sûre de supprimer ");
    if (conf === true) {
      this.tblearticle.splice(index, 1);
      axios
        .delete("api/suparticle/" + id)

        .then(response => {
          /* .then(data => {*/
          console.log();
          Swal.fire({
            position: "top-end",
            type: "success",
            title: "Suppression Reussi",
            showConfirmButton: false,
            timer: 3000
          });
          this.afficher();
        })
        .catch(err => console.log(err));
    }
  }
};
</script>

