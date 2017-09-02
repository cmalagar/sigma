<template>
  <div>
    <div>
      {{ id }}
    </div>
    <div>
      {{ title }}
    </div>
  </div>
</template>

<script type="text/javascript">
  export default {
    props: [ 'id', 'title' ]
  }
</script>
