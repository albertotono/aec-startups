<template>
  <div class="card">
    <div class="card-img-top" alt="Logo" />
    <div class="card-body">
      <p class="card-text">
        <a href="https://airtable.com/shrLpxcEdauXQcecZ" target="blank">
          <img src="@/assets/imgs/plus.png" alt="plus-sign" />
        </a>
      </p>
      <p>
        <a href="https://airtable.com/shrLpxcEdauXQcecZ" target="blank"
          >Submit Entry</a
        >
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Card',
  mounted() {}
}
</script>

<style lang="scss">
.card-img-top {
  background: linear-gradient(15deg, #745fb5, #9a6dbb);
}
.card-body {
  img {
    width: 60px;
    cursor: pointer;
    transition: all 0.1s ease-in;
    margin-top: -64px;
    &:hover {
      transform: scale(1.025, 1.025);
      margin-top: -70px;
    }
  }
}
</style>
