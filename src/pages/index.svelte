<script lang="ts">
</script>

<div class="container">
  <div class="intro">
    <h1 class="greeting">Hi <span>👋</span></h1>
    <p>I'm Matt, a web developer from Phoenix, Az.</p>
    <p>I am passionate about my Faith, Family, green grass, web development, mechanical keyboards, and VS Code.</p>
  </div>
</div>

<style>
  p {
    line-height: 150%;
    font-size: 1.25em;
  }
  .intro {
    padding: 2em 1em;
  }
  .greeting {
    font-family: 'Victor Mono', monospace;
  }

  span:hover {
    animation-name: howdy;
    animation-duration: 1s;
    animation-iteration-count: infinite;
    transform-origin: 60% 60%;
    display: inline-block;
  }

  @keyframes howdy {
    0% {
      transform: rotate(0deg);
    }
    10% {
      transform: rotate(14deg);
    }
    20% {
      transform: rotate(-8deg);
    }
    30% {
      transform: rotate(14deg);
    }
    40% {
      transform: rotate(-4deg);
    }
    50% {
      transform: rotate(10deg);
    }
    60% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(0deg);
    }
  }
</style>
