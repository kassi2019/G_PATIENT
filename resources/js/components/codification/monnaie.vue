<template>
  <div>
    <menucodification></menucodification>
    <br />
    <br />
    <br />
    <div class="main-content-container container-fluid px-4"></div>
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
            data-target="#practiseModal"
          >Nouveau</button>
        </div>
      </div>
    </div>
    <!-- Modal Body -->
    <div
      class="modal fade"
      id="practiseModal"
      tabindex="-1"
      role="dialog"
      aria-labelledby="practiseModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-lg modal-side modal-top-right" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="practiseModalLabel">Ajout Monnaie</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">×</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="md-form">
              <label for="form-autocomplete" class="active">Code</label>
              <input type="search" id="form-autocomplete" class="form-control mdb-autocomplete" />
              <label for="form-autocomplete" class="active">Libelle</label>
              <input type="search" id="form-autocomplete" class="form-control mdb-autocomplete" />
            </div>
          </div>

          <div class="modal-footer">
            <button type="button" class="btn btn-success">Enregistrer</button>
            <button type="button" class="btn btn-danger" data-dismiss="modal">Fermer</button>
          </div>
        </div>
      </div>
    </div>
    <table
      id="example"
      class="table table-striped table-bordered nowrap"
      cellspacing="0"
      width="100%"
    >
      <thead>
        <tr>
          <th width="20%">Code</th>
          <th width="20%">Libelle</th>
          <th>Modifier</th>
          <th>Supprimer</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="monnaies in allmonnaies" :key="monnaies.id">
          <td>{{monnaies.code}}</td>
          <td>{{monnaies.libelle}}</td>
          <td></td>
          <td></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
import { mapGetters } from "vuex";
import menucodification from "./menucodification";
export default {
  components: {
    menucodification
  },
  // methods: {
  //   ...mapActions(["ajouter_monnaie"])
  // },
  computed: {
    ...mapGetters(["allmonnaies"])
  }
  // created() {
  //   this.ajouter_monnaie();
  // }
};
</script>
