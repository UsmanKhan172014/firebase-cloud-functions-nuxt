<template>
    <div class="container text-center">
        <h1>Encryption Decryption Demo</h1>
        <div class="row">
        <div class="col-md-12">
        <!-- <label>Enter Plain Text</label> -->
        <!-- <Textarea class="form-control" :value="data"></Textarea> -->

        <button class="btn btn-primary mt-2" @click="encryptData">Encrypt</button>
        <button class="btn btn-primary mt-2" @click="decryptData">Decrypt</button>
        </div>
        </div>
        <div class="row">
            <div class="col-md-12">
            <!-- <Textarea class="form-control" v-model="dataResponse"></Textarea> -->
            </div>
        
        </div>
    </div>
</template>
<script>

import { initializeApp } from 'firebase/app';
import {initializeAppCheck,ReCaptchaV3Provider} from 'firebase/app-check'
import { getFunctions, httpsCallable } from 'firebase/functions';
import { getAuth } from "firebase/auth";
const app = initializeApp({
        apiKey: "AIzaSyDdgmCHHo-WcgGSbp6n8CUNeXpIp-hMavE",
        authDomain: "cloud-functions-test-02.firebaseapp.com",
        projectId: "cloud-functions-test-02",
        storageBucket: "cloud-functions-test-02.appspot.com",
        messagingSenderId: "1005391137919",
        appId: "1:1005391137919:web:acc1250ed0bec2812f434a"
});
const auth = getAuth(app);
const appCheck = initializeAppCheck(app, {
  provider: new ReCaptchaV3Provider('6LeRN6AhAAAAAFeKEFkoJ-bYCFzGRegJDJabG_cb'),
  isTokenAutoRefreshEnabled: true
});
const functions = getFunctions(app);
const encryptData = httpsCallable(functions, 'encryptData');
const decryptData = httpsCallable(functions, 'decryptData');
export default {
    name: 'GetStatus',
    data() {
        return {
            data:`{
    "name": "M Usman Khan 2",
    "email":"usman.khan@geniteam.pk",
    "phone":"324234234",
    "subject":"Blockchain Demo",
    "message":"testing the second data entr"
}`,
            cypherText:"U2FsdGVkX192/0xmZimuNTUShU79ec4cSpFg29SZBT/ty05RpOenN1EK2VeDxVLs0EVusvUlsItd01mTFTR1tZ/+xj46YLKZrNEAe1DP1cf+x2uPXXOZp8pC3nbxXO7R3qZJwF8VA49DewVS7ALx9XVwxvE/DwztIGm9BrvzgXlUj9cUVOMnXv47TRl/Y9hPovAjNO/dpGWNiFcKOQeBGWYIgkl6ipTfyn/yXFvLwZYMcya85C3l1Q2icFdY4MQKppqpahT/nFy1j2n3pxl3hoKZ+7mlHiGX9+v/pLhD5FU="
        };
    },
    methods: {
        encryptData: async function () {
            console.log(auth);
            console.log(this.data)
            await encryptData({
                plainText: this.data
            }).then(result => {
                console.log(result.data.data);
                // this.dataResponse = result.data.data
                
            }).catch(error => {
                console.log(error);
            });
        },
        decryptData: async function() {
            console.log(this.cypherText)
             await decryptData({
                cypherText: this.cypherText
            }).then(result => {
                console.log(JSON.parse(result.data.data));
                // this.dataResponse = result.data.data
                
            }).catch(error => {
                console.log(error);
            });
        }
    },
    beforeMount() {
        // this.encryptData();
    }
    
}
</script>