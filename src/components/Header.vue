<template>
<div>
  <b-nav>
    <b-nav-item disabled><b>Vue-Quiz</b></b-nav-item>
    <b-nav-item disabled>Counter: {{numCorrect}}/{{total}}</b-nav-item>
    
  </b-nav>
</div>
</template>
<script>
export default {
  props:[
    'numCorrect',
    'total'
  ]
}
</script>
