<script>
  import "./index.scss";
  import {
    linkListRokok,
    linkPenjualanKeseluruhan,
    linkPenjualanPerRokok,
    linkPenjualanPerHari
  } from "../link.js";
</script>

<section class="section menu">
  <div class="container">
    <div class="tile is-ancestor">
      <div class="tile is-parent">
        <a class="tile is-child box" href={linkListRokok}>
          <i class="fas fa-smoking" />
          <br />
          <h2 class="title is-4 has-text-centered has-text-weight-medium">
            List Rokok
          </h2>
        </a>
      </div>
      <div class="tile is-parent">
        <a class="tile is-child box" href={linkPenjualanKeseluruhan}>
          <i class="fas fa-chart-pie" />
          <br />
          <h2 class="title is-4 has-text-centered has-text-weight-medium">
            Penjualan Keseluruhan
          </h2>
        </a>
      </div>
      <div class="tile is-parent">
        <a class="tile is-child box" href={linkPenjualanPerRokok}>
          <i class="fas fa-chart-line" />
          <br />
          <h2 class="title is-4 has-text-centered has-text-weight-medium">
            Penjualan Per Rokok
          </h2>
        </a>
      </div>
      <div class="tile is-parent">
        <a class="tile is-child box" href={linkPenjualanPerHari}>
          <i class="fas fa-chart-bar" />
          <br />
          <h2 class="title is-4 has-text-centered has-text-weight-medium">
            Penjualan Per Hari
          </h2>
        </a>
      </div>
    </div>
  </div>
</section>
