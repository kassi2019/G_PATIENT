<template>
  <div>
    <menucodification></menucodification>
     <br />
    <div class="main-content-container container-fluid px-4"></div>
    <div class="row">
      <div class="col-lg-5 col-md-5 col-sm-5" style="padding-bottom: 10px;"></div>
      <div class="col-lg-4 col-md-4 col-sm-4" style="padding-bottom: 10px;"></div>
      <div class="col-lg-2 col-md-2 col-sm-2" style="padding-bottom: 10px;">
        <div class="div-action pull pull-right" style="padding-bottom:5px;">
          <br />
          <button
            type="button"
            class="btn btn-primary btn"
            data-toggle="modal"
            data-target="#practiseModal"
          >
                <span>
                  <i class="fa fa-plus"></i>
                </span>
            </button>
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
            <h5 class="modal-title" id="practiseModalLabel">Ajout Fonction</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">×</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="md-form">
            
              <label for="form-autocomplete" class="active">Libelle</label>
              <input type="search" id="form-autocomplete" class="form-control mdb-autocomplete" />
            </div>
          </div>

          <div class="modal-footer">
            <button type="button" class="btn btn-success">Valider</button>
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
         
          <th width="70%">Libelle</th>
          <th>Action</th>
         
        </tr>
      </thead>
      <tbody>
        <tr v-for="monnaies in allmonnaies" :key="monnaies.id">
          
          <td>{{monnaies.libelle}}</td>
          <td></td>
          <td></td>
        </tr>
      </tbody>
    </table>
    
     <!-- <fab :actions="fabActions" @cache="afficherModalAjouterFonction"  bg-color="green"></fab> -->
  </div>
</template>
<script>
import { mapGetters } from "vuex";
import menucodification from "./menucodification";
export default {
  components: {
    menucodification
  },
  // data() {
  //   return {
  //     // fabActions: [
  //     //   {
  //     //     name: "cache",
  //     //     icon: "add"
  //     //   }
  //       // {
  //       //   name: "alertMe",
  //       //   icon: "add_alert",
  //       //   class: ""
  //       // }
  //     // ],
     
  //   };
  // },
  // methods: {
  //    //afiicher modal ajouter
  //   afficherModalAjouterFonction() {
  //     this.$("#exampleModal").modal({
  //       backdrop: "static",
  //       keyboard: false
  //     });
  //   },
    // alert() {
    //   console.log("ok");
    // },
  
  computed: {
    ...mapGetters(["allmonnaies"])
  }
  // created() {
  //   this.ajouter_monnaie();
  // }
};
</script>
