<script>
import { RouterLink, RouterView } from 'vue-router'
export default {
    
}
</script>

<template >
    <div class="d-flex flex-column flex-shrink-0 p-3 text-bg-dark menu" style="width: 280px;heigth:100vh;" >
        <a href="/" class="d-flex align-items-center mb-3 mb-md-0 me-md-auto text-white text-decoration-none">
          <svg class="bi pe-none me-2" width="40" height="32"><use xlink:href="#bootstrap"></use></svg>
          <span class="fs-4">Painel</span>
        </a>
        <hr>
        <ul class="nav nav-pills flex-column mb-auto">
          <li class="nav-item">
            <RouterLink to="/" class="nav-link " aria-current="page" active-class="active">
              <svg class="bi pe-none me-2" width="16" height="16"><use xlink:href="#home"></use></svg>
              Home
            </RouterLink>
          </li>
          <li class="nav-item">
            <RouterLink to="/about" class="nav-link " aria-current="page" active-class="active">
              <svg class="bi pe-none me-2" width="16" height="16"><use xlink:href="#home"></use></svg>
              Dashboard
            </RouterLink>
          </li>
          <li class="nav-item">
            <RouterLink to="/cadastro" class="nav-link " aria-current="page" active-class="active">
              <svg class="bi pe-none me-2" width="16" height="16"><use xlink:href="#home"></use></svg>
              Cadastro
            </RouterLink>
          </li>
          <li class="nav-item">
            <RouterLink to="/" class="nav-link " aria-current="page" active-class="active">
              <svg class="bi pe-none me-2" width="16" height="16"><use xlink:href="#home"></use></svg>
              Produtos
            </RouterLink>
          </li>
          <li class="nav-item">
            <RouterLink to="/" class="nav-link " aria-current="page" active-class="active">
              <svg class="bi pe-none me-2" width="16" height="16"><use xlink:href="#home"></use></svg>
              Categorias
            </RouterLink>
          </li>
        </ul>
        <hr>
       </div>
</template>

<style lang="">
   
</style>