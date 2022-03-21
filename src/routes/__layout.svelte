<script context="module">
  export async function load({ url }) {
    const path = url.pathname;
    return {
      props: { path },
    };
  }
</script>

<script>
  import "../app.css";

  import Header from "$lib/components/Header.svelte";
  import Footer from "$lib/components/Footer.svelte";

  export let path;

  const brand = {
    title: "Green Fort Farms",
    image: "/images/logo.jpg",
    url: "/",
  };
  const items = [
    { title: "The farm", url: "/farm" },
    { title: "Dirty hands", url: "/about" },
    { title: "What's available", url: "/available" },
    { title: "Reach out!", url: "/contact" },
    { title: "Why GFF", url: "/why" },
  ];
</script>

<Header {brand} {items} {path} />

<main>
  <div class="prose">
    <slot />
  </div>
</main>

<Footer
  instagram="https://www.instagram.com/greenfortfarms"
  youtube="https://www.youtube.com/user/greenfortfarms"
  facebook="https://www.facebook.com/groups/greenfortfarms"
/>