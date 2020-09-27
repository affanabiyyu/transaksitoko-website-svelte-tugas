<script>
  import Chart from "chart.js";
  import html2pdf from "html2pdf.js";
  import { onMount } from "svelte";

  let grafik;
  let myChart;

  let date = "2020-09-14";
  let dateOutput = "2020-09-14";

  let listPenjualan = [];
  let totalPenjualan = 0;
  let arrayLabels = [];
  let arrayData = [];

  onMount(() => {
    myChart = new Chart(grafik,{});
    updateData();
  });

  function updateData() {
    myChart.destroy();
    let fetchData = (async () => {
      let response = await fetch(
        "http://localhost/rest-api-rokok/api/penjualanperhari?date=" + date,
        {
          method: "GET"
        }
        );
      let responseJson = await response.json();
      let array1 = await responseJson.data;
      let counter = 0;
      totalPenjualan = 0;

      for (let i=0; i<array1.length; i++) {
        for (let j=0; j<array1[i].length; j++) {
          listPenjualan[counter] = array1[i][j];
          totalPenjualan = totalPenjualan + parseInt(listPenjualan[counter].harga_rokok * listPenjualan[counter].jumlah);
          arrayData[counter] = listPenjualan[counter].jumlah;
          arrayLabels[counter] = listPenjualan[counter].nama_rokok;
          counter = counter + 1;
        };
      };

      myChart = new Chart(grafik, {
        type: "bar",
        data: {
          labels: arrayLabels,
          datasets: [
          {
            label: "Jumlah Rokok Terjual",
            data: arrayData,
            borderWidth: 1
          }
          ]
        },
        options: {
          maintainAspectRatio: true,
          scales: {
            yAxes: [
            {
              ticks: {
                beginAtZero: true,
                stepSize: 5
              }
            }
            ]
          }
        }
      });
    })();
  };
  
  function printHandler() {
    myChart.resize();
    myChart.update();
    let opt = {
      margin : 0.15,
      filename: 'Laporan Penjualan.pdf',
      image : {
        type: 'jpeg',
        quality: 0.8
      },
      html2canvas: { scale: 1.5 },
      jsPDF: { unit: 'in', format: 'letter', orientation: 'landscape' }
    };

    html2pdf().set(opt).from(document.body).save();
  }

</script>

<section class="section list-rokok">
  <div class="container">

    <div class="columns">
      <div class="column is-10">
        <p class="title is-5">Select Date</p>
        <div class="select">
          <select bind:value={date} on:change={updateData}>
            <option>2020-09-14</option>
            <option>2020-09-15</option>
            <option>2020-09-16</option>
            <option>2020-09-17</option>
            <option>2020-09-18</option>
            <option>2020-09-19</option>
            <option>2020-09-20</option>
            <option>2020-09-21</option>
          </select>
        </div>
      </div>
      <div class="column">
        <button class="button is-link is-fullwidth is-outlined" on:click={printHandler}>Get PDF</button>
      </div>
    </div>

    <div class="columns">
      <div class="column">
        <h1 class="title is-3">Penjualan Tanggal {date}</h1>
      </div>
    </div>

    <div class="tile is-ancestor">
      <div class="tile is-parent">
        <div class="tile is-child box" style="position: relative;">
          <canvas bind:this={grafik} />
        </div>
      </div>
      <div class="tile is-parent">
        <div class="tile is-child box">

          <table class="table is-fullwidth is-striped is-hoverable is-mobile">
            <thead>
              <tr>
                <th>Deskripsi</th>
                <th>Qty</th>
                <th>Harga</th>
                <th>Total</th>
              </tr>
            </thead>
            <tbody>
              {#each listPenjualan as penjualan}
              <tr>
                <td>{penjualan.nama_rokok}</td>
                <td>{penjualan.jumlah}</td>
                <td>Rp. {penjualan.harga_rokok},-</td>
                <td>Rp. {penjualan.harga_rokok * penjualan.jumlah},-</td>
              </tr>
              {/each}
            </tbody>
            <tfoot>
              <tr>
                <th></th>
                <th></th>
                <th>Total</th>
                <th>Rp. {totalPenjualan},-</th>
              </tr>
            </tfoot>
          </table>

        </div>
      </div>
    </div>

   </div>
</section>
