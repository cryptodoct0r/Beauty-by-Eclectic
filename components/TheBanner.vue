<template>
  <div class="banners">
    <div class="banner container">
      <p class="my-auto d-none d-md-flex">
        <strong class="my-auto">FREE SHIPPING FOR ORDERS OVER $300</strong>
      </p>

      <div class="my-auto linksList">
        <div
          v-click-outside="closeSearch"
          v-handle-scroll="closeSearch"
          class="my-auto links"
        >
          <span
            class="search"
            to="#"
          >
            <label for="search" />
            <input
              id="search"
              :class="{ open: isActive }"
              type="text"
              placeholder="Search"
              class="searchTerm"
            >
            <button
              v-if="!isActive"
              class="searchButton"
              @click="opened"
            >
              <i class="fas fa-search" />
            </button>
            <button
              v-if="isActive"
              type="submit"
              class="searchButton"
            >
              <i class="fas fa-search" />
            </button>
          </span>
        </div>
        <div class="my-auto links">
          <b-dropdown
            size="md"
            variant="link"
            toggle-class="text-decoration-none"
            no-caret
          >
            <template v-slot:button-content>
              <i class="fas fa-globe" /><span class="sr-only">Globe</span>
            </template>
            <b-dropdown-item href="#">
              language
            </b-dropdown-item>
            <b-dropdown-item href="#">
              Currency
            </b-dropdown-item>
            <b-dropdown-item href="#">
              Country
            </b-dropdown-item>
          </b-dropdown>
        </div>
        <div class="my-auto links">
          <b-dropdown
            id="dropdown-form"
            ref="dropdown"
            variant="link"
            toggle-class="text-decoration-none"
            no-caret
          >
            <template v-slot:button-content>
              <i class="fas fa-user" /><span class="sr-only">User</span>
            </template>
            <b-dropdown-form>
              <b-form-group
                label="Email"
                label-for="dropdown-form-email"
                @submit.stop.prevent
              >
                <b-form-input
                  id="dropdown-form-email"
                  size="sm"
                  placeholder="email@example.com"
                />
              </b-form-group>

              <b-form-group
                label="Password"
                label-for="dropdown-form-password"
              >
                <b-form-input
                  id="dropdown-form-password"
                  type="password"
                  size="sm"
                  placeholder="Password"
                />
              </b-form-group>

              <b-form-checkbox class="mb-3">
                Remember me
              </b-form-checkbox>
              <b-button
                variant="primary"
                size="sm"
                @click="onClick"
              >
                Sign In
              </b-button>
            </b-dropdown-form>
            <b-dropdown-divider />
            <b-dropdown-item-button>New around here? Sign up</b-dropdown-item-button>
            <b-dropdown-item-button>Forgot Password?</b-dropdown-item-button>
          </b-dropdown>
        </div>
        <div class="my-auto links">
          <div
            v-if="cartCount > 0"
            class="carttotal"
          >
            {{ cartCount }}
          </div>
          <nuxt-link to="/cart">
            <i class="fas fa-shopping-cart shopingCartIcon" />
          </nuxt-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import clickOutside from '@/directives/click-outside'
import handleScroll from '@/directives/handle-scroll'
export default {
  directives: {
    clickOutside,
    handleScroll
  },
  data () {
    return {

      isActive: false
    }
  },
  computed: {
    ...mapGetters(['cartCount'])
  },
  methods: {
    opened () {
      this.isActive = !this.isActive
    },
    onClick () {
      this.isActive = false
    },
    closeSearch () {
      this.isActive = false
    }
  }
}
</script>

<style lang="scss" scoped>
.banners {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: $darkColor;
  color: $lightColor;
  height: 50px;
  width: 100vw;
  text-align: center;
}
.banner {
  display: flex;
  justify-content: center;
  align-items: center;
}

div.linksList {
  padding-left: 0;
  margin-left: auto;
  list-style: none;

  div.links {
    display: inline;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    font-size: 13px;
    padding: 0 20px;
    border-right: 1px solid #ddd;
    position: relative;
    list-style: none;
    text-decoration: none;
    a,
    span {
      color: $blackColor;
      text-decoration: none;
      &:hover {
        color: $primaryColor;
      }
    }
    i {
      color: $lightColor;
      &:hover {
        color: $primaryColor;
      }
    }
  }
}

.carttotal {
  position: absolute;
  border-radius: 0px;
  background: $primaryColor;
  color: white;
  top: -10px;
  right: 18.5px;
  width: 15px;
  text-align: center;
  height: 15px;
  transform: rotate(-50deg);
  font-size: 10px;
  font-weight: bold;
  padding: 0px 3px;
  font-weight: bold;
  z-index: 0;
}

i.shopingCartIcon {
  position: relative;
  z-index: 2;
  opacity: 1;
}

.searchButton {
  background: transparent;
  border: none;
}

input.searchTerm {
  border: none;
  padding: 0 5px;

  background: transparent;
  width: 0px;
  transition: 250ms all ease-in-out;
  outline: none;

  &:focus {
    background-color: $whiteColor;
  }

  &.open {
    border-left: 1px solid #ddd;
    width: 100px;
  }
}

@media screen and (max-width: 375px) {
  div.linksList {
    padding-left: 0;
    margin-left: auto;
    list-style: none;

    div.links {
      display: inline;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      font-size: 13px;
      padding: 0 5px;
      border-right: none;
      position: relative;
      list-style: none;
      text-decoration: none;
      a,
      span {
        color: $blackColor;
        text-decoration: none;
        &:hover {
          color: $primaryColor;
        }
      }
      i {
        color: $lightColor;
        &:hover {
          color: $primaryColor;
        }
      }
    }
  }
}
</style>
