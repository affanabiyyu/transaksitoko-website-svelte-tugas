<script>
  import Chart from "chart.js";

  let barChart;
  let pieChart;

  let date = "2020-09-14";

  let arrayOutput = [];
  let objectOutput = {
    id_rokok: "",
    nama_rokok: "",
    jumlah: "",
    harga_rokok: ""
  };

  let test 

  const fetchData = (async () => {
    const response = await fetch(
      "http://localhost/rest-api-rokok/api/penjualanperhari?date=" + date,
      {
        method: "GET"
      }
    );
    let responseJson = await response.json();
    console.log(responseJson);
    for (let i=0; i<responseJson.data.length; i++){
      for (let j=0; i<responseJson.data[i].length; j++){
        let flag = false;
        // Cek di Array Output
        // for (let k=0; k<arrayOutput.length; k++){
        //   if (arrayOutput[k].id_rokok == responseJson.data[i][j].id_rokok){
        //     arrayOutput[k].jumlah += responseJson.data[i][j].jumlah;
        //     flag = true;
        //   }; 
        // };
        console.log(responseJson);
        console.log(responseJson.data);
        console.log(responseJson.data[i]);
        console.log(responseJson.data[i][j]);
        console.log(responseJson.data[i][j].id_rokok);
        // if (flag === false) {
        //   objectOutput.id_rokok = responseJson.data[i][j].id_rokok;
        //   objectOutput.nama_rokok = responseJson.data[i][j].nama_rokok;
        //   objectOutput.jumlah = responseJson.data[i][j].jumlah;
        //   objectOutput.harga_rokok = responseJson.data[i][j].harga_rokok;
        //   arrayOutput.push(objectOutput);
        // };
      };
    };
  })();
</script>

<section class="section list-rokok">
  <div class="container">
    <h1 class="title is-1">Penjualan Per Hari</h1>
    <div class="tile is-ancestor">
      <div class="tile is-vertical">
        <div class="tile is-12">
          <div class="tile is-parent">
            <div class="tile is-child box">
              <p class="title is-5">Pie Chart</p>
              <canvas bind:this={pieChart} />
            </div>
          </div>
          <div class="tile is-6 is-vertical is-parent">
            <div class="tile is-child box">
              <p class="title is-5">Select Date</p>
              <div class="select">
                <select bind:value={date}>
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
            <div class="tile is-child box">
              <p class="title is-5">Tabel Penjualan {date}</p>

            </div>
          </div>
        </div>
        <div class="tile is-12">
          <div class="tile is-parent">
            <div class="tile is-child box">
              <canvas bind:this={barChart} />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
