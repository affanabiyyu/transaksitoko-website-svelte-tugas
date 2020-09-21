<script>
  import Chart from "chart.js";

  let listRokok = [];
  let grafikRokok;
  let arrayLabels = [];
  let arrayData = [];

  const fetchData = (async () => {
    const response = await fetch("http://localhost/rest-api-rokok/api/rokok", {
      method: "GET"
    });
    let responseJson = await response.json();
    listRokok = await responseJson.data;
    for (let i = 0; i < listRokok.length; i++) {
      arrayLabels[i] = listRokok[i].nama_rokok;
      arrayData[i] = listRokok[i].harga_rokok;
    }
    let myBarChart = new Chart(grafikRokok, {
      type: "horizontalBar",
      data: {
        labels: arrayLabels,
        datasets: [
          {
            label: "Harga Rokok",
            data: arrayData,
            backgroundColor: [
              "rgba(255, 99, 132, 0.2)",
              "rgba(54, 162, 235, 0.2)",
              "rgba(255, 206, 86, 0.2)",
              "rgba(75, 192, 192, 0.2)",
              "rgba(153, 102, 255, 0.2)",
              "rgba(255, 159, 64, 0.2)",
              "rgba(255, 99, 132, 0.2)",
              "rgba(54, 162, 235, 0.2)",
              "rgba(255, 206, 86, 0.2)",
              "rgba(75, 192, 192, 0.2)",
              "rgba(153, 102, 255, 0.2)",
              "rgba(255, 159, 64, 0.2)",
              "rgba(255, 99, 132, 0.2)",
              "rgba(54, 162, 235, 0.2)"
            ],
            borderColor: [
              "rgba(255, 99, 132, 1)",
              "rgba(54, 162, 235, 1)",
              "rgba(255, 206, 86, 1)",
              "rgba(75, 192, 192, 1)",
              "rgba(153, 102, 255, 1)",
              "rgba(255, 159, 64, 1)",
              "rgba(255, 99, 132, 1)",
              "rgba(54, 162, 235, 1)",
              "rgba(255, 206, 86, 1)",
              "rgba(75, 192, 192, 1)",
              "rgba(153, 102, 255, 1)",
              "rgba(255, 159, 64, 1)",
              "rgba(255, 99, 132, 1)",
              "rgba(54, 162, 235, 1)"
            ],
            borderWidth: 1
          }
        ]
      },
      options: {
        maintainAspectRatio: false,
        scales: {
          xAxes: [
            {
              ticks: {
                beginAtZero: true
              }
            }
          ]
        }
      }
    });
    myBarChart.canvas.parentNode.style.height = '40rem';
  })();
</script>

<section class="section list-rokok">
  <div class="container">
    <h1 class="title is-1">List Rokok</h1>
    <div class="columns">
      <div class="column">
        <canvas bind:this={grafikRokok} />
      </div>
      <div class="column">
        <table class="table is-fullwidth is-striped is-hoverable is-mobile">
          <thead>
            <tr>
              <th>
                <abbr title="number">ID</abbr>
              </th>
              <th>
                <abbr title="name">Nama Rokok</abbr>
              </th>
              <th>
                <abbr title="price">Harga</abbr>
              </th>
            </tr>
          </thead>

          <tbody>
            {#each listRokok as rokok}
              <tr>
                <td>{rokok.id_rokok}</td>
                <td>{rokok.nama_rokok}</td>
                <td>Rp. {rokok.harga_rokok},-</td>
              </tr>
            {/each}
          </tbody>

        </table>
      </div>
    </div>
  </div>
</section>
