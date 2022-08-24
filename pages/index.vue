<template>
<div class="container">
  <GetStatus />
  <SignIn/>
</div>
</template>

<script>
import GetStatus from '~/components/GetStatus.vue';
import SignIn from '~/components/SignIn.vue';

export default {
    name: "IndexPage",
    components: { GetStatus, SignIn }
}
</script>
