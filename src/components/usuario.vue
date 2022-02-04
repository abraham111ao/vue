
<template>

  <div class="card">

    <img class="avatar" src="https://www.pngmart.com/files/10/User-Account-PNG-Clipart.png">

    <div class="infos">
      <div class="name capitalize">
        {{ user.username }}
      </div>
      <div class="birth">
        <i class="fas fa-fw fa-user"></i>{{ user.name }}
      </div>
      <div class="email">
        <i class="fas fa-fw fa-envelope"></i>{{ user.email }}
      </div>
      <div class="phone">
        <i class="fas fa-fw fa-phone"></i>{{ user.phone }}
      </div>
      <div class="nationality capitalize">
        <i class="fas fa-fw fa-globe-americas"></i>{{ user.address.city }}
      </div>
    </div>

  </div>
</template>

<script>

export default {
    props: ['user']
}

</script>

<style scope>
@import url("https://fonts.googleapis.com/css?family=Nunito");
@import 'https://pro.fontawesome.com/releases/v5.10.0/css/all.css';


body main .card {
  width: 470px;
  min-height: 185px;
  display: flex;
  padding: 10px;
  border-radius: 10px;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
  background: #00ccffcc;
}
body main .card .avatar {
  width: 100px;
  height: 100px;
  margin-right: 10px;
  border-radius: 50%;
}
body main .card .infos {
  flex: 1 1 auto;
  display: flex;
  flex-direction: column;
}
body main .card .infos div:not(:last-child) {
  margin-bottom: 10px;
}
body main .card .infos div.capitalize {
  text-transform: capitalize;
}
body main .card .infos div.name {
  font-size: 150%;
  font-weight: bold;
}
body main .card .infos div i {
  margin-right: 10px;
}

@media only screen and (max-width: 800px) {
  body main {
    flex-direction: column !important;
    font-size: 80%;
  }
  body main .card {
    max-width: 80%;
    width: auto;
    min-height: 150px;
  }
}
</style>