<template>
  <CRow>
    <CCol col="12" xl="12">
      <transition name="slide">
      <CCard>
        <CCardBody>
            <CButton color="primary" @click="createSoftware()">Crear  Software</CButton>
            <CAlert
              :show.sync="dismissCountDown"
              color="primary"
              fade
            >
              ({{dismissCountDown}}) {{ message }}
            </CAlert>
            <CDataTable
              hover
              :items="items"
              :fields="fields"
              :items-per-page="10"
              pagination
            >
              <template #author="{item}">
                <td>
                  <strong>{{item.author}}</strong>
                </td>
              </template>
              <template #title="{item}">
                <td>
                  <strong>{{item.title}}</strong>
                </td>
              </template>
              <template #content="{item}">
                <td>
                  {{item.content}}
                </td>  
              </template>
              <template #applies_to_date="{item}">
                <td>
                  {{item.applies_to_date}}
                </td>
              </template>
              <template #status="{item}">
                <td>
                  <CBadge :color="item.status_class">{{item.status}}</CBadge>
                </td>
              </template>
              <template #note_type="{item}">
                <td>
                  <strong>{{item.note_type}}</strong>
                </td>
              </template>
            
              <template #editar="{item}">
                <td>
                  <CButton color="primary" @click="editSoftware( item.id )">Editar</CButton>
                </td>
              </template>
              <template #borrar="{item}">
                <td>
                  <CButton v-if="you!=item.id" color="danger" @click="deleteSoftware( item.id )">Borrar</CButton>
                </td>
              </template>
            </CDataTable>
        </CCardBody>  
      </CCard>
      </transition>
    </CCol>
  </CRow>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Softwares',
  data: () => {
    return {
      items: [],
     
      fields: ['nombre', 'descripcion',  'editar', 'borrar'],
      currentPage: 1,
      perPage: 5,
      totalRows: 0,
      you: null,
      message: '',
      showMessage: false,
      dismissSecs: 7,
      dismissCountDown: 0,
      showDismissibleAlert: false
    }
  },
  computed: {
  },
  methods: {
    getRowCount (items) {
      return items.length
    },
    noteLink (id) {
      return `software/${id.toString()}`
    },
    editLink (id) {
      return `software/${id.toString()}/edit`
    },
    showNote ( id ) {
      const noteLink = this.noteLink( id );
      this.$router.push({path: noteLink});
    },
    editSoftware ( id ) {
      const editLink = this.editLink( id );
      this.$router.push({path: editLink});
    },
    deleteSoftware ( id ) {
      let self = this;
      let noteId = id;
      axios.post(  '/api/software/' + id + '?token=' + localStorage.getItem("api_token"), {
        _method: 'DELETE'
      })
      .then(function (response) {
          self.message = 'Registro borrado exitosamente.';
          self.showAlert();
          self.getSoftware();
      }).catch(function (error) {
        console.log(error);
        self.$router.push({ path: '/login' });
      });
    },
    createSoftware () {
      this.$router.push({path: 'software/create'});
    },
    countDownChanged (dismissCountDown) {
      this.dismissCountDown = dismissCountDown
    },
    showAlert () {
      this.dismissCountDown = this.dismissSecs
    },
    getSoftware (){
      let self = this;
      axios.get(  '/api/software?token=' + localStorage.getItem("api_token") )
      .then(function (response) {
        self.items = response.data;
      }).catch(function (error) {
        console.log(error);
        self.$router.push({ path: '/login' });
      });
    }
  },
  mounted: function(){
    this.getSoftware();
  }
}
</script>

<style scoped>
.card-body >>> table > tbody > tr > td {
  cursor: pointer;
}
</style>
