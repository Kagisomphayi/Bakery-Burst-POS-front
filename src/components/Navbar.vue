<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container-fluid">
      <a class="navbar-brand" href="#"></a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ms-md-auto gap-2">
          <li class="nav-item rounded">
            <a class="nav-link" aria-current="page" href="#"
              ><router-link to="/">Home</router-link></a
            >
          </li>
          <li class="nav-item rounded">
            <a class="nav-link" href="#"
              ><router-link to="/about">About</router-link></a
            >
          </li>
          <li class="nav-item rounded">
            <a class="nav-link" href="#"
              ><router-link to="/products">Products</router-link></a
            >
          </li>
          <li class="nav-item rounded">
            <a class="nav-link" href="#"
              ><router-link to="/login">Login</router-link></a
            >
          </li>
          <li class="nav-item rounded">
            <a class="nav-link" href="#"
              ><router-link to="/register">Register</router-link></a
            >
          </li>
          <li class="nav-item rounded">
            <a class="nav-link" href="#"
              ><router-link to="/register">Contact us</router-link></a
            >
          </li>
          <li class="nav-item dropdown rounded">
            <a
              class="nav-link dropdown-toggle"
              href="#"
              id="navbarDropdown"
              role="button"
              data-bs-toggle="dropdown"
              aria-expanded="false"
              ><i class="bi bi-person-fill me-2"></i>Profile</a
            >
            <ul
              class="dropdown-menu dropdown-menu-end"
              aria-labelledby="navbarDropdown"
            >
              <li><a class="dropdown-item" href="#">Account</a></li>
              <li>
                <hr class="dropdown-divider" />
              </li>
              <li><a class="dropdown-item" href="#">Delete Accout</a></li>
            </ul>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {

    
};
</script>

<style></style>
