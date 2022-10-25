<template>
    <div class="bg-light min-vh-100 d-flex flex-row align-items-center">
        <CContainer>
            <CRow class="justify-content-center">
                <CCol :md="9" :lg="7" :xl="6">

                    <body>
                        <div class="alert">
                            <span class="closebtn" onclick="this.parentElement.style.display='none';">&times;</span>
                            <div class="w3-panel w3-green w3-round-large">
                                <h5 class="p"><i>Inscription des recruteurs</i></h5>
                            </div>
                            <br />
                            <form>
                                <div class="form-row">
                                    <form>
                                        <div class="row">
                                            <div class="col">
                                                <label class="l" for="inputEmail4">Nom:</label>
                                                <input type="text" class="form-control" placeholder="First name" v-model="firstName" required/>
                                            </div>
                                            <div class="col">
                                                <label class="l" for="inputEmail4">Prénom:</label>
                                                <input type="text" class="form-control" placeholder="Last name" v-model="lastName" required/>
                                            </div>
                                        </div>
                                    </form>
                                    <form>
                                        <div class="row">
                                            <div class="col">
                                                <label class="l" for="inputEmail4">Email:</label>
                                                <input type="email" class="form-control" id="inputEmail4"
                                                    placeholder="Addo@gmail.com" v-model="email" required/>
                                            </div>
                                            <div class="col">
                                                <label class="l" for="inputEmail4">Mot de passe:</label>
                                                <input type="password" class="form-control" id="inputPassword4"
                                                    placeholder="Password" v-model="password" required/>
                                            </div>
                                        </div>
                                    </form>
                                </div>
                                <div class="form-group">
                                    <label class="l" for="inputAddress">Addresse</label>
                                    <input type="text" class="form-control" id="inputAddress"
                                        placeholder="1234 Main St" v-model="address" required/>
                                </div>
                                <div class="form-group">
                                    <label class="l" for="inputAddress2">Date de naissance:</label>
                                    <input type="date" class="form-control" id="inputdate"
                                        placeholder="Apartment, studio, or floor" v-model="birthDate" required/>
                                </div>
                                <div class="form-group">
                                    <label class="l" for="inputAddress"> Entreprise:</label>
                                    <input type="text" class="form-control" id="inputAddress"
                                        placeholder="1234 Main St" v-model="company" required/>
                                </div>
                                <div class="form-group">
                                    <label for="inputAddress">Ville</label>
                                    <input type="select" class="form-control" id="inputAddress"
                                        placeholder="1234 Main St" v-model="city" required/>
                                </div>

                                <div class="form-row">
                                    <div class="form-group col-md-4">
                                        <label class="l" for="inputState">Sexe</label>
                                        <select id="inputState" class="form-control" v-model="gender" required>
                                            <option class="l" selected>Homme</option>
                                            <option class="l"> Femme</option>
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
                                </div>
                                <div class="center">
                                    <button @click="ajout()" type="button"
                                        class="btn btn-info">S'inscrire</button>
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
import axios from "axios";
export default {
    name: "Register1",
    data(){
        return{
firstName : null,
lastName : null,
password: null,
address: null,
birthDate : null,
company: null,
city : null,
gender : null,
email : null,
role : "recruteur"
        }
    },
    methods: {
        ajout(){
            let recruteur = {firstName:this.firstName,lastName:this.lastName,email:this.email,password:this.password,address:this.address,birthDate:this.birthDate,company:this.company,city:this.city,gender:this.gender,role:this.role}
             localStorage.setItem("recruteur",JSON.stringify(recruteur))
             this.$router.push({path:"modalite"})
        }
   }
}
</script>


<style scoped>
.center {
    text-align: center;
}

.l {
    font-size: 12px;
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
</style>
