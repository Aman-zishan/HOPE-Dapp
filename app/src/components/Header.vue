<template>
  <header class="header">
    <b-navbar class="container is-max-desktop">
      <template v-slot:brand>
        <b-navbar-item tag="router-link" :to="{ path: '/' }">
          <logo />
        </b-navbar-item>
      </template>
      <template v-slot:start>
        <b-navbar-item tag="router-link" to="/" class="has-text-primary">Home</b-navbar-item>
      </template>
      <template v-slot:end>
        <template v-if="connected">
          <b-navbar-item tag="div">
            <b-button
              inverted
              size="is-small is-primary"
              icon-left="plus"
              @click="$router.push('/campaign/new')"
            >
              New Campaign
            </b-button>
          </b-navbar-item>
          <b-navbar-item tag="div">
            <user-address
              v-if="connected"
              :address="address"
              class="has-background-primary-light mt-1"
              truncate
            />
          </b-navbar-item>
        </template>
        <b-navbar-item tag="div" v-else>
          <b-button size="is-primary is-small" @click="connect">Connect Wallet</b-button>
        </b-navbar-item>
      </template>
    </b-navbar>
  </header>
</template>

<script>
import { mapState } from 'vuex';
import Logo from '@/components/LogoMain.vue';
import UserAddress from '@/components/UserAddress.vue';
import { connect } from '../store/modules/ethers/ethersConnect';

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Header',
  components: { Logo, UserAddress },
  computed: mapState('ethers', ['connected', 'address']),
  methods: { connect },
};
</script>
