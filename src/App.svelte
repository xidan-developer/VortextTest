<script>

import { Router, Route, Link } from "svelte-routing";
import Home from "./routes/Home.svelte";
import Partners from "./routes/Partners.svelte";


</script>

<Router>
  <div>
    <Route path="/*">
        <Home />
    </Route>

    <Route path="/partners" component={Partners} params="{'Partners'}"  />

  </div>
</Router>
<style lang="sass">

</style>