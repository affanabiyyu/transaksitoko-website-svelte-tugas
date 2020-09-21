<script>
  import "./index.scss";
  import { onMount } from "svelte";
  import { linkHome, linkListRokok, linkPenjualanKeseluruhan, linkPenjualanPerRokok, linkPenjualanPerHari, linkLogin } from "../link.js";

  onMount(async () => {
    // START JS NAVBAR HAMBURGER
    // Get all "navbar-burger" elements
    let _navbarBurgers = Array.prototype.slice.call(
      document.querySelectorAll(".navbar-burger"),
      0
    );
    // Check if there are any navbar burgers
    if (_navbarBurgers.length > 0) {
      // Add a click event on each of them
      _navbarBurgers.forEach(function(_el) {
        _el.addEventListener("click", function() {
          // Get the target from the "data-target" attribute
          let target = _el.dataset.target;
          let _target = document.getElementById(target);

          // Toggle the class on both the "navbar-burger" and the "navbar-menu"
          _el.classList.toggle("is-active");
          _target.classList.toggle("is-active");
        });
      });
    }
    document.querySelectorAll(".navbar-link").forEach(function(navbarLink) {
      navbarLink.addEventListener("click", function() {
        navbarLink.nextElementSibling.classList.toggle("is-hidden-mobile");
      });
    });
    // END JS NAVBAR HAMBURGER
  });
</script>

<nav class="navbar is-black" role="navigation" aria-label="main navigation">
  <div class="navbar-brand">
    <a class="navbar-item" href={linkHome}>
      <span class="icon is-medium">
        <i class="fas fa-smoking" />
      </span>
      <span class="has-text-weight-bold">Kelontong Koh Apan</span>
    </a>

    <a
      role="button"
      class="navbar-burger burger"
      aria-label="menu"
      aria-expanded="false"
      data-target="navbarBasicExample">
      <span aria-hidden="true" />
      <span aria-hidden="true" />
      <span aria-hidden="true" />
    </a>
  </div>

  <div id="navbarBasicExample" class="navbar-menu">
    <div class="navbar-start">
      <a class="navbar-item" href={linkListRokok}>List Rokok</a>

      <div class="navbar-item has-dropdown is-hoverable">
        <a class="navbar-link">Laporan</a>

        <div class="navbar-dropdown">
          <a class="navbar-item" href={linkPenjualanKeseluruhan}>
            Penjualan Keseluruhan
          </a>
          <a class="navbar-item" href={linkPenjualanPerRokok}>
            Penjualan Per Rokok
          </a>
          <a class="navbar-item" href={linkPenjualanPerHari}>
            Penjualan Per Hari
          </a>
        </div>
      </div>
    </div>

    <div class="navbar-end">
      <div class="navbar-item">
        <div class="buttons">
          <a class="button is-warning" href={linkLogin}>Log in Database</a>
        </div>
      </div>
    </div>
  </div>
</nav>
