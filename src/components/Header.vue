<template>
    <div>
  <b-nav tabs>
    <b-nav-item disabled>Trial app</b-nav-item>
    <b-nav-item disabled>Counter : {{numCorrect}}/{{numTots}}</b-nav-item>
    
  </b-nav>
</div>
</template>

<script>
export default{
  props :[
    'numTots',
    'numCorrect',
  ]
}

</script>