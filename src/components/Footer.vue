<template>
  <footer class="footer">
    <p>Artu</p>
    <p>Florient</p>
    <p>TPD</p>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
};
</script>

<style scoped>
.footer {
  position: relative;
  z-index: 1;
  bottom: 0;
  width: 100%;
  color: #FFF;
  font-weight: 400;
  text-align: center;
  background: #f0f0f0;
  padding: 15px 0;

}

.footer::before {
  content: '';
  position: absolute;
  background-image: url('..\img\footer.png');
  background-size: cover;
  background-repeat: no-repeat;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: -1;
}
</style>
