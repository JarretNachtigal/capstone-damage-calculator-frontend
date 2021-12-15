<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/">Make Calculation</router-link>
      |
      <router-link to="/history">History</router-link>
      |
      <router-link to="/about">About</router-link> -->
    <header id="header" class="fixed-top">
      <!-- <div class="container d-flex align-items-center justify-content-between"> -->
      <!-- <h1 class="logo"><a href="index.html">eNno</a></h1> -->
      <nav id="navbar" class="navbar">
        <ul>
          <li><a class="nav-link to" href="/">Home</a></li>
          <li><a class="nav-link to" href="/history">History</a></li>
          <li><a class="nav-link to" href="/about">About</a></li>
        </ul>
        <i class="bi bi-list mobile-nav-toggle"></i>
      </nav>
      <!-- .navbar -->
      <!-- </div> -->
    </header>
    <!-- End Header -->

    <!-- .navbar -->
    <!-- </div> -->
    <router-view />
    <!-- ======= Footer ======= -->
    <footer id="footer">
      <!-- <div class="navbar fixed-bottom"> -->
      <div class="container footer-bottom clearfix">
        <div class="copyright">
          &copy; Copyright
          <strong><span>eNno</span></strong>
          . All Rights Reserved
        </div>
        <div class="credits">
          <!-- All the links in the footer should remain intact. -->
          <!-- You can delete the links only if you purchased the pro version. -->
          <!-- Licensing information: https://bootstrapmade.com/license/ -->
          <!-- Purchase the pro version with working PHP/AJAX contact form: https://bootstrapmade.com/enno-free-simple-bootstrap-template/ -->
          Designed by
          <a href="https://bootstrapmade.com/">BootstrapMade</a>
        </div>
      </div>
      <!-- </div> -->
    </footer>
    <!-- End Footer -->
  </div>
</template>

<style></style>
