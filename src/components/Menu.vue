<template lang="">
    <div class="container">
        <div class="container-teks">
            Welcome To Our Store!
            <div>
                <button @click="" class="">Tombol</button>
            </div>
        </div>
        
        <div class="container-table">
            <table border="1">
                    <tr>
                        <td>No</td>
                        <td>Nama</td>
                        <td>Harga</td>
                        <td>Jumlah</td>
                        <td>Action</td>
                    </tr>
                    <tr>
                        <td>No</td>
                        <td>1</td>
                        <td>2</td>
                        <td>3</td>
                        <td>4</td>
                    </tr>
                    <tr>
                        <td>No</td>
                        <td>1</td>
                        <td>2</td>
                        <td>3</td>
                        <td>4</td>
                    </tr>
            </table>
        </div>
    </div>
</template>




<script>
export default {
    
}
</script>

<style>
    .container
    {
        display: flex;
        flex-direction: column; /* Mengatur tata letak elemen vertikal */
        align-items: center; /* Mengatur konten di tengah horizontal */
        height: 100vh; /* Untuk mengisi tinggi layar secara penuh */
    }
    .container-teks
    {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        width: 20%;
        height: 20%;
        margin-top: 5%;
        box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
        
    }
    .container-table
    {
        display: flex;
        max-width: 80%;
        width: auto;
        height: auto; 
        margin-top: 2%;
        box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
        background-color: white;
    }
    table {
    width: 100%; /* Mengisi lebar tabel ke seluruh lebar kontainer */
    border-collapse: collapse; /* Menggabungkan batas antar sel */
  }

  table, td {
    padding: 10px; /* Mengatur jarak dalam sel */
    text-align: center; /* Mengatur teks menjadi rata tengah */
  }

  tr:first-child {
    border: 2px solid black; /* Menambahkan garis bawah pada baris pertama */
    font-weight: bold; /* Menambahkan tebal pada teks pada baris pertama */
  }

</style>