<template lang="">
    <div class="container">
    <div class="container-teks">
        Welcome To Our Store!
    </div>

     <div class="container-table">
        <table class="table">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">First</th>
      <th scope="col">Last</th>
      <th scope="col">Handle</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">1</th>
      <td>Mark</td>
      <td>Otto</td>
      <td>@mdo</td>
    </tr>
    <tr>
      <th scope="row">2</th>
      <td>Jacob</td>
      <td>Thornton</td>
      <td>@fat</td>
    </tr>
    <tr>
      <th scope="row">3</th>
      <td>Larry</td>
      <td>the Bird</td>
      <td>@twitter</td>
    </tr>
  </tbody>
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
        height: auto; 
        margin-top: 2%;
    }
</style>