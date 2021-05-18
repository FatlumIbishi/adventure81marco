<template>
  <div
    uk-sticky="animation: uk-animation-slide-top; sel-target: .uk-navbar-container; cls-active: uk-navbar-sticky; cls-inactive: uk-navbar-transparent uk-light adventureMenu; top: 50vh"
  >
    <nav class="uk-navbar-container">
      <div class="uk-container uk-container-large">
        <div uk-navbar>
          <div class="uk-navbar-left">
            <ul v-if="desktop" class="uk-navbar-nav">
              <li><a uk-scroll href="#">Home</a></li>
              <li>
                <a uk-scroll href="#adventures">Adventures</a>
                <div class="uk-navbar-dropdown">
                  <ul class="uk-nav uk-navbar-dropdown-nav">
                    <li><a uk-scroll href="#adventures">3 HR Charter</a></li>
                    <li><a uk-scroll href="#custom">Custom Tour</a></li>
                    <li><a uk-scroll href="#weddings">Weddings</a></li>
                    <li><a uk-scroll href="#private">Private Dinner</a></li>
                  </ul>
                </div>
              </li>
              <li><a uk-scroll href="#about">About</a></li>
              <li><a uk-scroll href="#contact">Contact us</a></li>
            </ul>
            <div
              v-if="mobile"
              class="uk-navbar-toggle"
              uk-toggle="target: #offcanvas-overlay"
            >
              <div
                uk-navbar-toggle-icon
                class="uk-icon uk-navbar-toggle-icon"
              />
            </div>
          </div>
          <div class="uk-navbar-right">
            <ul class="uk-navbar-nav">
              <li>
                <a
                  :class="{ menuPhone: mobile, menuBtn: desktop }"
                  href="tel:+19207073585"
                >
                  <span class="uk-visible@m">Text us: +1 920-707-3585</span>
                  <i class="fas fa-phone uk-hidden@m"></i>
                </a>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </nav>
    <div id="offcanvas-overlay" ref="offCanvas" uk-offcanvas="overlay: true">
      <div class="uk-offcanvas-bar uk-flex uk-flex-column">
        <button class="uk-offcanvas-close" type="button" uk-close></button>

        <ul class="uk-nav uk-nav-primary uk-nav-center uk-margin-auto-vertical">
          <li><a uk-scroll @click="hideMenu" href="#">Home</a></li>
          <li class="uk-parent">
            <a uk-scroll @click="hideMenu" href="#adventures">Adventures</a>
            <ul class="uk-nav-sub">
              <li>
                <a uk-scroll @click="hideMenu" href="#adventures">
                  3 HR Charter
                </a>
              </li>
              <li>
                <a uk-scroll @click="hideMenu" href="#custom">Custom Tour</a>
              </li>
              <li>
                <a uk-scroll @click="hideMenu" href="#weddings">Weddings</a>
              </li>
              <li>
                <a uk-scroll @click="hideMenu" href="#private"
                  >Private Dinner</a
                >
              </li>
            </ul>
          </li>
          <li><a uk-scroll @click="hideMenu" href="#about">About</a></li>
          <li>
            <a uk-scroll @click="hideMenu" href="#contact">Contact us</a>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import UIkit from "uikit";

export default {
  name: "Menu",
  data: () => ({
    mobile: false,
    desktop: true,
  }),
  computed: {},
  components: {},
  mounted() {
    this.onResize();

    this.$nextTick(() => {
      window.addEventListener("resize", this.onResize);
    });
  },

  beforeDestroy() {
    window.removeEventListener("resize", this.onResize);
  },
  methods: {
    onResize() {
      if (window.innerWidth > 960) {
        this.desktop = true;
        this.mobile = false;
      } else {
        this.desktop = false;
        this.mobile = true;
      }
    },
    hideMenu() {
      const element = this.$refs.offCanvas;
      // eslint-disable-next-line no-undef
      UIkit.offcanvas(element).hide();
    },
  },
};
</script>
