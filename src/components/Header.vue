<template>
  <div>
      <nav class="nav-tabs nav-justified">
          <a class="nav-item active mr-5"><b>Quiz app</b></a>
          <a class="nav-item">Counter: {{ this.numCorrect }}/{{ this.numTotal }}</a>
      </nav>
  </div>
</template>

<script>
export default {
    props:[
        'numTotal',
        'numCorrect'
    ]
}
</script>

<style>

</style>