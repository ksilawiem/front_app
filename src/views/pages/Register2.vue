<template>
  <div class="bg-light min-vh-100 d-flex flex-row align-items-center">
    <CContainer>
      <CRow class="justify-content-center">
        <CCol :md="9" :lg="7" :xl="6">

          <body>
            <div class="alert">
              <span class="closebtn" onclick="this.parentElement.style.display='none';">&times;</span>
              <div class="w3-panel w3-green w3-round-large">
                <h5 class="p"><i>Inscription des condidats</i></h5>
              </div>
              <br />
              <form>
                <div class="form-row">
                  <form>
                    <div class="row">
                      <div class="col">
                        <label class="l" for="inputEmail4">Nom:</label>
                        <input type="text" class="form-control" placeholder="First name" v-model="nom" required/>
                      </div>
                      <div class="col">
                        <label class="l" for="inputEmail4">Prénom:</label>
                        <input type="text" class="form-control" placeholder="Last name" v-model="prenom" required/>
                      </div>
                    </div>
                  </form>
                  <form>
                    <div class="row">
                      <div class="col">
                        <label class="l" for="inputEmail4">Email:</label>
                        <input type="email" class="form-control" id="inputEmail4" placeholder="Addo@gmail.com" v-model="email" required/>
                      </div>
                      <div class="col">
                        <label class="l" for="inputEmail4">Mot de passe:</label>
                        <input type="password" class="form-control" id="inputPassword4" placeholder="Password" v-model="motdepasse" required/>
                      </div>
                    </div>
                  </form>
                </div>
                <div class="form-group">
                  <label for="inputAddress">Addresse</label>
                  <input type="text" class="form-control" id="inputAddress" placeholder="1234 Main St" v-model="adresse" required/>
                </div>
                <div class="form-group">
                  <label for="inputAddress">Ville</label>
                  <input type="select" class="form-control" id="inputAddress" placeholder="1234 Main St" v-model="ville" required/>
                </div>
                <div class="form-group">
                  <label class="l" for="inputAddress2">Date de naissance:</label>
                  <input type="date" class="form-control" id="inputdate" placeholder="Apartment, studio, or floor" v-model="date" required/>
                </div>
                <div class="form-row">
                  <div class="form-group col-md-4">
                     <div class="form-group">
                    <label for="exampleFormControlFile1">Curriculum vitae</label>
                    <input type="file" class="form-control-file" id="exampleFormControlFile1" @change="OnFileSelected" required>
                  </div>
                    <label class="l" for="inputState">Sexe</label>
                    <select id="inputState" class="form-control" v-model="sexe" required>
                      <option class="l" selected>Homme</option>
                      <option class="l">Femme</option>
                    </select>
                  </div>
                </div>
                <div class="form-group">
                                    <div class="form-check">
                                        <input class="form-check-input" type="checkbox" value id="cgu" required />
                                        <label class="form-check-label" for="cgu">J'accepte tout les conditions
                                            générales
                                            d'utilisation</label>
                                        <div class="invalid-feedback">Vous devez accepter les CGU pour continuer</div>
                                    </div>

                 
                  <div class="form-check">

                  </div>
                </div>
                <div class="center">
                  <button @click="onUpload()" type="button" class="btn btn-info">S'inscrire</button>
                </div>
              </form>
            </div>
          </body>
        </CCol>
      </CRow>
    </CContainer>
  </div>
</template>
<script>
import  axios from 'axios';
export default {
  
  data(){
      return{
        file : null,
        selectedFile: null,
        nom : null,
prenom : null,
motdepasse: null,
adresse: null,
date : null,

ville : null,
sexe : null,
anneexp : null,
cv : ""
      }
  },
  methods:{
    OnFileSelected(event){
         this.selectedFile =event.target.files[0]
         console.log(this.selectedFile)
    },
    onUpload () {
          const form = new FormData()
          form.append('file',this.selectedFile);
          form.append("upload_preset" , "YassineBm");
          form.append("resource_type", "auto")
          axios.post('https://api.cloudinary.com/v1_1/dqe0t46k3/upload', form)
          .then((result) => this.cv=result.data.secure_url).then(()=>{
          axios.post("http://localhost:8000/api/users/create",{firstName:this.nom,lastName:this.prenom,email:this.email,password:this.motdepasse,address:this.adresse,birthDate:this.date,company:null,city:this.ville,gender:this.sexe
          ,role:"condidat",cv:this.cv,modePaiment:null,début:null,fin:null})
          })
          .then(()=>{
            this.$router.push({path:"/pages/login"});
          }
          )
          
    }
  }
}
</script>
<style scoped>
.center {
  text-align: center;
}

.svg {
  background-color: white;
  position: absolute;
  top: 0px;
  right: 1px;
  color: white;
  /* padding: 10px 10px; */
  font-size: 16px;
  border: none;
}

.closebtn {
  margin-left: 15px;
  color: white;
  font-weight: bold;
  float: right;
  font-size: 22px;
  line-height: 20px;
  cursor: pointer;
  transition: 0.3s;
}

.p {
  text-align: center;
  color: rgb(236, 228, 228);
}

.alert {
  padding: 20px;
  background-color: #202070;
  color: white;
}

.l {
  font-size: 12px;
}
</style>
