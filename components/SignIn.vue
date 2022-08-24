<template>
    <div class="row">
        <button class="btn btn-primary mt-2" @click="signIn">Sign In</button>
    </div>
</template>
<script>
import { Sign } from "crypto";
import { getAuth, signInWithEmailAndPassword } from "firebase/auth";
import { SignIn } from "~/build/components";
const auth = getAuth()
export default {
    name: 'SignIn',
    data() {
        return {
            email: "usmankhan7419@gmail.com",
            password: "12345678"
        };
    },
    methods: {
        signIn: async function () {
            signInWithEmailAndPassword(auth, this.email, this.password)
            .then((userCredential) => {
                // Signed in 
                const user = userCredential.user;
                window.location="/"
                // ...
            })
            .catch((error) => {
                const errorCode = error.code;
                const errorMessage = error.message;
            });
                    }
    }
//     beforeMount() {
//         this.signIn()
//     }
}
</script>