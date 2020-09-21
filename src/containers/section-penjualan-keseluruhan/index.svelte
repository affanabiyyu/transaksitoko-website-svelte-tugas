<script>
  import "./index.scss";
  import Chart from "chart.js";

  let listPemasukan = [];
  let grafik;
  let arrayDate = [];
  let arrayIncome = [];

  const fetchData = (async () => {
    const response = await fetch(
      "http://localhost/rest-api-rokok/api/totaltransaksi",
      {
        method: "GET"
      }
    );
    let responseJson = await response.json();
    listPemasukan = await responseJson.data;

    for (let i = 0; i < listPemasukan.length; i++) {
      arrayDate[i] = listPemasukan[i].tanggal;
      arrayIncome[i] = listPemasukan[i].transaksi;
    }

    let chart = new Chart(grafik, {
      type: "line",
      data: {
        labels: arrayDate,
        datasets: [
          {
            label: "Total Pemasukan",
            data: arrayIncome,
            showline: true,
            fill: false,
            backgroundColor: "rgba(255, 206, 86, 1)",
            borderColor: "rgba(255, 206, 86, 1)",
            borderWidth: 3
          }
        ]
      },
      options: {
        maintainAspectRatio: false,
        scales: {
          yAxes: [
            {
              ticks: {
                beginAtZero: true
              }
            }
          ]
        }
      }
    });
    chart.canvas.parentNode.style.height = "20rem";
  })();
</script>

<section class="section list-rokok">
  <div class="container">
    <h1 class="title is-1">Penjualan Keseluruhan</h1>
    <div class="columns">
      <div class="column">
        <canvas bind:this={grafik} />
      </div>
    </div>
    <div class="columns">
      <div class="column">
        <table class="table is-fullwidth is-striped is-hoverable is-mobile">
          <thead>
            <tr>
              <th>
                <abbr title="number">ID</abbr>
              </th>
              <th>
                <abbr title="date">Tanggal</abbr>
              </th>
              <th>
                <abbr title="income">Pemasukan</abbr>
              </th>
            </tr>
          </thead>
          <tbody>
            {#each listPemasukan as pemasukan}
              <tr>
                <td>{pemasukan.id}</td>
                <td>{pemasukan.tanggal}</td>
                <td>Rp. {pemasukan.transaksi},-</td>
              </tr>
            {/each}
          </tbody>
        </table>
      </div>
    </div>
  </div>
</section>
