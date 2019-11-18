
<template>
  <div>
    <menucodification></menucodification>
    <br />
    <br />
    <br />
    <div class="main-content-container container-fluid px-4">
      <h3 style="text-align:center">Listes du personnels</h3>
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
              <h4 class="modal-title" id="exampleModalLabel">Formulaire d'Inscrisption</h4>
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">×</span>
              </button>
            </div>
            <form @submit.prevent="creepersonnel">
              <div class="modal-body">
                <div class="modal-body" style="padding: 5px;">
                  <div class="row">
                    <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                      <div class="form-group">
                        <label>Nom Personnel</label>
                        <input
                          class="form-control"
                          placeholder="Nom personnel"
                          type="text"
                          v-model="chmpajout.name"
                          required
                          autofocus
                        />
                      </div>
                    </div>
                    <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                      <div class="form-group">
                        <label>Prenoms Personnel</label>
                        <input
                          class="form-control"
                          placeholder="Prenoms personnel"
                          type="text"
                          v-model="chmpajout.prenoms"
                          required
                          autofocus
                        />
                      </div>
                    </div>
                  </div>
                  <div class="row">
                    <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                      <div class="form-group">
                        <label>Date Naissance</label>
                        <input
                          class="form-control"
                          type="date"
                          v-model="chmpajout.datenaissance"
                          required
                          autofocus
                        />
                      </div>
                    </div>

                    <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                      <div class="form-group">
                        <label>Lieu Naissance</label>
                        <input
                          class="form-control"
                          placeholder="Lieu Naissance"
                          type="text"
                          v-model="chmpajout.lieunaissance"
                          required
                          autofocus
                        />
                      </div>
                    </div>
                  </div>

                  <div class="row">
                    <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                      <div class="form-group">
                        <label>Statut Personnel</label>
                        <select
                          id="statut_id"
                          v-model="chmpajout.statut"
                          class="form-control form-control-sm"
                        >
                          <option v-for="statut in stats" :key="statut.id">{{statut}}</option>
                        </select>
                      </div>
                    </div>
                    <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                      <div class="form-group">
                        <label>Email</label>
                        <input
                          class="form-control"
                          placeholder="kassifabrice@gmail.com"
                          type="text"
                          v-model="chmpajout.email"
                          autofocus
                        />
                      </div>
                    </div>
                  </div>

                  <div class="row">
                    <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                      <label>Actif</label>

                      <input type="checkbox" v-model="chmpajout.actif" />
                    </div>
                    <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                      <div class="form-group">
                        <label>Fonction</label>
                        <select
                          id="statut_id"
                          v-model="chmpajout.fonction"
                          class="form-control form-control-sm"
                        >
                          <option v-for="option in fonctions" :key="option.id">{{option.libelle}}</option>
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

      <div class="row">
        <div class="col-lg-3 col-md-3 col-sm-3" style="padding-bottom: 10px;">
          <div class="btn-group btn-group-toggle" data-toggle="buttons">
            <button
              type="submit"
              class="btn btn-info"
              @click.prevent="tri='tous'"
            >Tous({{nombretous}})</button>
            <button
              type="submit"
              class="btn btn-success"
              @click.prevent="tri='actif'"
            >Actif ({{nombreactif}})</button>
            <button
              type="submit"
              class="btn btn-danger"
              @click.prevent="tri='inactif'"
            >Inactif({{nombreinactif}})</button>
          </div>
        </div>
        <div class="col-lg-3 col-md-3 col-sm-3">
          <div>
            <input
              class="form-control"
              placeholder="Chercher par Nom ou Prenoms"
              type="text"
              v-model="search"
              required
              autofocus
            />
          </div>
        </div>
        <div class="col-lg-3 col-md-3 col-sm-3">
          <button
            type="submit"
            class="btn btn-danger"
            v-show="selection.length>0"
            @click="Deletetout"
          >Tout Supprimer</button>
        </div>
        <div class="col-lg-3 col-md-3 col-sm-3">
          <button
            type="submit"
            class="btn btn-info"
            @click="activer"
            v-show="selection.length>0"
          >Actif</button>
        </div>
      </div>
      <div class="table-responsive">
        <br />

        <table class="table table-bordered">
          <thead>
            <tr>
              <th>
                <input type="checkbox" v-model="selectAll" @click="select" />
                <label>Tout Case</label>
              </th>
              <th>index</th>
              <th>Nom</th>
              <th>Prenoms</th>
              <th>Date Naissance</th>
              <th>Lieu Naissance</th>
              <th>Email</th>
              <th>Statut</th>
              <th>Actif</th>
              <th>Case Actif</th>

              <th>Modifier</th>
              <th>Supprimer</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(users,index) in filtre_personnel" :key="users.id">
              <td>
                <label class="form-checkbox">
                  <input type="checkbox" v-model="selection" :value="users.id" />
                  <i class="form-icon"></i>
                </label>
              </td>
              <td>{{index}}</td>
              <td>{{users.name}}</td>
              <td>{{users.prenoms}}</td>
              <td>{{users.datenaissance}}</td>
              <td>{{users.lieunaissance}}</td>
              <td>{{users.email}}</td>
              <td>{{users.statut}}</td>
              <td v-if="users.actif">actif</td>
              <td v-else>inactif</td>
              <td>
                <input type="checkbox" v-model="users.actif" />
              </td>

              <td style="text-align:center">
                <button @click="showedit(index)" class="btn btn-info">Modifier</button>
              </td>
              <td style="text-align:center">
                <button class="btn btn-danger" @click="Deletedata(index, users.id)">Supprimer</button>
              </td>
            </tr>
          </tbody>
        </table>
        <div v-if="filtre_personnel.length"></div>
        <div v-else>
          <p style="text-align:center;font-size:30px;color:red;">Aucun utilisateur trouvé</p>
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
              <form @submit.prevent="modifierperso">
                <div class="modal-body">
                  <div class="modal-body" style="padding: 5px;">
                    <div class="row">
                      <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                        <div class="form-group">
                          <label>Nom Personnel</label>
                          <input
                            class="form-control"
                            placeholder="Nom personnel"
                            type="text"
                            v-model="chmpmof.name"
                            required
                            autofocus
                          />
                        </div>
                      </div>
                      <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                        <div class="form-group">
                          <label>Prenoms Personnel</label>
                          <input
                            class="form-control"
                            placeholder="Prenoms personnel"
                            type="text"
                            v-model="chmpmof.prenoms"
                            required
                            autofocus
                          />
                        </div>
                      </div>
                    </div>
                    <div class="row">
                      <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                        <div class="form-group">
                          <label>Date Naissance</label>
                          <input
                            class="form-control"
                            type="date"
                            v-model="chmpmof.datenaissance"
                            required
                            autofocus
                          />
                        </div>
                      </div>

                      <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                        <div class="form-group">
                          <label>Lieu Naissance</label>
                          <input
                            class="form-control"
                            placeholder="Lieu Naissance"
                            type="text"
                            v-model="chmpmof.lieunaissance"
                            required
                            autofocus
                          />
                        </div>
                      </div>
                    </div>

                    <div class="row">
                      <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                        <div class="form-group">
                          <label>Statut Personnel</label>
                          <select
                            id="statut_id"
                            v-model="chmpmof.statut"
                            class="form-control form-control-sm"
                          >
                            <option v-for="statut in stats" :key="statut.id">{{statut}}</option>
                          </select>
                        </div>
                      </div>
                      <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                        <div class="form-group">
                          <label>Email</label>
                          <input
                            class="form-control"
                            placeholder="kassifabrice@gmail.com"
                            type="text"
                            v-model="chmpmof.email"
                            autofocus
                          />
                        </div>
                      </div>
                    </div>

                    <div class="row">
                      <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                        <label>Actif</label>

                        <input type="checkbox" v-model="chmpmof.actif" />
                      </div>
                      <div class="col-lg-6 col-md-6 col-sm-6" style="padding-bottom: 10px;">
                        <div class="form-group">
                          <label>Mot de Passe</label>
                          <input
                            class="form-control"
                            placeholder="********"
                            type="password"
                            v-model="chmpmof.password"
                            autofocus
                          />
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
  </div>
</template>
  
<script>
import menucodification from "../components/codification/menucodification";
export default {
  components: {
    menucodification
  },
  data() {
    return {
      tblepersonnel: [],
      selection: [],
      fonction: [],

      tri: "tous",
      //id: "",
      chmpajout: {
        name: "",
        prenoms: "",
        statut: "",
        lieunaissance: "",
        datenaissance: "",
        email: "",
        actif: false,
        fonction: ""
      },
      chmpmof: {
        name: "",
        prenoms: "",
        statut: "",
        lieunaissance: "",
        datenaissance: "",
        email: "",
        actif: ""
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
  computed: {
    filtre_personnel() {
      if (this.tri == "actif") {
        return this.tblepersonnel.filter(users => users.actif);
      } else if (this.tri == "inactif") {
        return this.tblepersonnel.filter(users => !users.actif);
      } else {
        const st = this.search.toLowerCase();
        return this.tblepersonnel.filter(users => {
          return (
            users.name.toLowerCase().includes(st) ||
            users.prenoms.toLowerCase().includes(st)
          );
        });
      }
    },
    nombreactif() {
      return this.tblepersonnel.filter(users => users.actif).length;
    },

    nombreinactif() {
      return this.tblepersonnel.filter(users => !users.actif).length;
    },
    nombretous() {
      return this.tblepersonnel.length;
    }
  },
  methods: {
    reset() {
      this.chmpajout.name = "";
      this.chmpajout.prenoms = "";
      this.chmpajout.statut = "";
      this.chmpajout.actif = "";
      this.chmpajout.datenaissance = "";
      this.chmpajout.lieunaissance = "";
      this.chmpajout.email = "";
      this.chmpajout.fonction = "";
    },
    reset1() {
      this.chmpmof.name = "";
      this.chmpmof.prenoms = "";
      this.chmpmof.statut = "";
      this.chmpmof.actif = "";
      this.chmpmof.datenaissance = "";
      this.chmpmof.lieunaissance = "";
      this.chmpmof.email = "";
      this.chmpmof.password = "";
    },
    select() {
      this.selection = [];

      if ((this.selectAll = !this.selectAll)) {
        for (let index in this.filtre_personnel) {
          this.selection.push(this.filtre_personnel[index].id);
        }
      }
    },

    //method d'insertion des données
    creepersonnel() {
      // console.log("salut toi");
      axios
        .post("api/ajouterpersonnel", {
          name: this.chmpajout.name,
          prenoms: this.chmpajout.prenoms,
          datenaissance: this.chmpajout.datenaissance,
          lieunaissance: this.chmpajout.lieunaissance,
          statut: this.chmpajout.statut,
          actif: this.chmpajout.actif,
          email: this.chmpajout.email,
          password: this.chmpajout.password
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
        this.tblepersonnel = response.data.personnels;
      });length
    },*/
    showedit(index) {
      // console.log("rrrrrrr");
      $("#modifierModal").modal();
      this.chmpmof = this.filtre_personnel[index];
      console.log(this.chmpmof);
    },
    modifierperso(index) {
      //console.log(this.id);
      axios
        .put("api/modifierutilisateur/" + this.chmpmof.id, {
          name: this.chmpmof.name,
          prenoms: this.chmpmof.prenoms,
          datenaissance: this.chmpmof.datenaissance,
          lieunaissance: this.chmpmof.lieunaissance,
          statut: this.chmpmof.statut,
          actif: this.chmpmof.actif,
          email: this.chmpmof.email,
          password: this.chmpmof.password
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
        this.tblepersonnel.splice(index, 1);
        axios
          .delete("api/suputilisateur/" + id)

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
    Deletetout() {
      let conf = confirm("Etes vous sûre de  supprimer ");
      if (conf === true) {
        //this.tblepersonnel.splice(index,n);
        axios
          .post("/api/Fabrice/Parametre/toutsuppersonnel", {
            id: this.selection
          })

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
    activer() {
      //this.tblepersonnel.splice(index,n);
      axios.post("/api/Fabrice/Parametre/actifinactif", { id: this.selection });
      this.afficher();

      this.selection = [];
      this.selectAll = false;
      // .then(response => {
      //   /* .then(data => {*/
      //   console.log();
      //   Swal.fire({
      //     position: "top-end",
      //     type: "success",
      //     title: "Suppression Reussi",
      //     showConfirmButton: false,
      //     timer: 3000
      //   });
      //   this.afficher();
      // })
      // .catch(err => console.log(err));
    },
    //changerstatut() {},
    afficher() {
      axios.get("api/listeutilisateur").then(response => {
        this.tblepersonnel = response.data.Utilisateurs;
      });
    }
  },
  Deletedata(index, id) {
    let conf = confirm("Etes vous sûre de supprimer ");
    if (conf === true) {
      this.tblepersonnel.splice(index, 1);
      axios
        .delete("api/suputilisateur/" + id)

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

