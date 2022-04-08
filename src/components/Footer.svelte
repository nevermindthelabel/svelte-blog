<script>
  const date = new Date().getFullYear();
</script>

<div class="footer">
  <div class="image">
    <picture>
      <source media="(max-width: 350px)" type="image/avif" srcset="./src/assets/downtown_330.avif" />
      <source media="(max-width: 350px)" type="image/webp" srcset="./src/assets/downtown_330.webp" />
      <source media="(max-width: 500px)" type="image/avif" srcset="./src/assets/downtown_480.avif" />
      <source media="(max-width: 500px)" type="image/webp" srcset="./src/assets/downtown_480.webp" />
      <source media="(max-width: 1000px)" type="image/avif" srcset="./src/assets/downtown_1368.avif" />
      <source media="(max-width: 1000px)" type="image/webp" srcset="./src/assets/downtown_1368.webp" />
      <source type="image/avif" srcset="./src/assets/downtown_3024trim.avif" />
      <source type="image/webp" srcset="./src/assets/downtown_3024trim.webp" />
      <img src="./src/assets/downtown_3024.jpg" alt="thing" />
    </picture>
  </div>

  &copy; Matt Kilcup {date}
</div>

<style>
  img {
    max-inline-size: 100%;
    block-size: auto;
    filter: grayscale(0.2);
  }
</style>
