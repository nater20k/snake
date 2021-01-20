<script>
  const blocks = document.querySelectorAll('#block');
  for (let index = 0; index < blocks.length; index++) {
    const element = array[index];
  }
</script>

<main>
  <div id="table">
    <div class="block" />
  </div>
</main>

<style>
  #table {
    width: 800px;
    height: 800px;
    background-color: gray;
    display: grid;
    grid-template-columns: repeat(20, 40px);
    grid-template-rows: repeat(20, 40px);
    margin: auto;
  }

  .block {
    width: 40px;
    height: 40px;
    background-color: black;
  }
</style>
