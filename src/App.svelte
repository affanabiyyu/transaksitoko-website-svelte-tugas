<script>
  import { Router, Route } from "svelte-routing";

  import { Home } from "./pages";
  import { ListRokok } from "./pages";
  import { PenjualanPerHari } from "./pages";
  import { PenjualanKeseluruhan } from "./pages";
  import { PenjualanPerRokok } from "./pages";

  import { Navbar } from "./containers";
  import { Footer } from "./containers";

  export let url = "";
</script>

<Navbar />

<Router {url}>
  <Route path="/" component={Home} />
  <Route path="/list-rokok" component={ListRokok} />
  <Route path="/penjualan-keseluruhan" component={PenjualanKeseluruhan} />
  <Route path="/penjualan-per-hari" component={PenjualanPerHari} />
  <Route path="/penjualan-per-rokok" component={PenjualanPerRokok} />
</Router>

<Footer />