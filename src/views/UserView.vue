<template>
  <div>
    <section class="session"
             style="background-image: url(./static/icons-background.svg)">
      <div class="hero-body">
        <div class="column is-8 is-offset-2">
          <div class="box ">
            <div class="columns">
              <div class="column ">
                <div class="column is-half">
                  <p class="image is-128x128">
                    <img src="https://bulma.io/images/placeholders/128x128.png">
                  </p>
                </div>
                <div class="column is-half">
                  <h1 class="">
                    {{$t('Nickname')}}: {{nickame}}
                  </h1>
                  <h2 class="">
                    {{$t('Address')}}: {{address}}
                  </h2>
                  <h1 class="">
                    {{$t('Benefit')}}: {{benefit}}
                  </h1>
                </div>
              </div>

            </div>

            <div class="navbar-tabs">
              <a class="navbar-item is-tab">
                <a v-if="me && me.address.toUpperCase() === address">{{$t('Cards I Bought')}}</a>
                <a v-else>{{$t('Cards He Bought')}}</a>
              </a>
              <a class="navbar-item is-tab">
                <a v-if="me && me.address.toUpperCase() === address">{{$t('Cards I Created')}}</a>
                <a v-else>{{$t('Cards He Created')}}</a>
              </a>
            </div>
          </div>
        </div>

      </div>

    </section>

    <ItemList :itemIds='itemIds' />
  </div>
</template>

<script>
import ItemList from '@/components/ItemList';
import { getItemsOf } from '@/api';

export default {
  name: 'UserView',
  components: {
    ItemList,
  },
  data: () => ({
    itemIds: [],
  }),

  computed: {
    address() {
      return this.$route.params.address.toUpperCase();
    },
    me() {
      return this.$store.state.me;
    },
  },
  async created() {
    this.itemIds = await getItemsOf(this.$route.params.address);
  },

  watch: {},

  methods: {},
};
</script>
<style scoped>
.user-info-wrapper {
  border-radius: 5px;
}
</style>

