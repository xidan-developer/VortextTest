<script>
import Header from "../components/header.svelte";
import Footer from "../components/footer.svelte";
export let params

</script>

<Header />
<div class="container">
    Demonstration page {params}
</div>
<Footer/>
