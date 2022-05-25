<template>
  <v-app-bar
    id="app-bar"
    absolute
    app
    color="transparent"
    flat
    height="75"
  >
    <v-btn
      class="mr-3"
      elevation="1"
      fab
      small
      @click="setDrawer(!drawer)"
    >
      <v-icon v-if="value">
        mdi-view-quilt
      </v-icon>

      <v-icon v-else>
        mdi-dots-vertical
      </v-icon>
    </v-btn>

    <v-toolbar-title
      class="hidden-sm-and-down font-weight-light"
      v-text="$route.name"
    />

    <v-spacer/>
    <v-tooltip bottom>
      <template v-slot:activator="{ on, attrs }">
      <v-btn        
        class="ml-2 ma-2"
        min-width="0"
        v-bind="attrs"
        v-on="on"
        color="indigo"
        outlined
        @click="connectUser"
      >
        Connect
        <v-icon medium right>mdi-credit-card-scan-outline</v-icon>
      </v-btn>
      </template>
    <span>Read User Data</span>
  </v-tooltip>
  </v-app-bar>
</template>

<script>
  // Components
  import { VHover, VListItem } from 'vuetify/lib'

  // Utilities
  import { mapState, mapMutations } from 'vuex'

  export default {
    name: 'DashboardCoreAppBar',

    components: {
      AppBarItem: {
        render (h) {
          return h(VHover, {
            scopedSlots: {
              default: ({ hover }) => {
                return h(VListItem, {
                  attrs: this.$attrs,
                  class: {
                    'black--text': !hover,
                    'white--text secondary elevation-12': hover,
                  },
                  props: {
                    activeClass: '',
                    dark: hover,
                    link: true,
                    ...this.$attrs,
                  },
                }, this.$slots.default)
              },
            },
          })
        },
      },
    },

    props: {
      value: {
        type: Boolean,
        default: false,
      },
    },

    data: () => ({
      
    }),

    computed: {
      ...mapState(['drawer', 'token']),
    },

    methods: {
      ...mapMutations({
        setDrawer: 'SET_DRAWER',
        setToken: 'SET_TOKEN'
      }),
      connectUser() {
        this.setToken('eyJraWQiOiJCZlo0LXB3eS1YcE5oN0E2S1p3cFJHRlRkM25MdXlUY1p6c1hxcHdaUkQ4IiwiYWxnIjoiUlMyNTYifQ.eyJ2ZXIiOjEsImp0aSI6IkFULmxuRWNhNThHUzBnekZyOHZPRm02ZklOSi1pb0U0UXNHd002WWNuZm4xQzAiLCJpc3MiOiJodHRwczovL2Rldi0wMTkzNjg2MS5va3RhLmNvbS9vYXV0aDIvZGVmYXVsdCIsImF1ZCI6ImFwaTovL2RlZmF1bHQiLCJpYXQiOjE2NTM0NTgxOTksImV4cCI6MTY1MzQ2MTc5OSwiY2lkIjoiMG9hNDRkOHBsaEJZN3ZPYzg1ZDciLCJ1aWQiOiIwMHU1MHJ2eXdkOG1HdUp3NzVkNyIsInNjcCI6WyJlbWFpbCIsInByb2ZpbGUiLCJvcGVuaWQiXSwiYXV0aF90aW1lIjoxNjUzNDUyMDUzLCJzdWIiOiJwZXJzb25pY2xlLmRlbW8uYWNjdEBnbWFpbC5jb20ifQ.hOsGVIDUw0ouaKVG_gTZ7ISafgj_zNq_VsC4cO0JS6oHa05hYNECU0hVuQFeTLzQWAljH6iNLRCs15WAXrcG2eDkn5IZW4OZxDf3UBwGtWjbjJgRsqUO2cX7jp_9Ez2AXFAt60OLLu99muICOg43OKglsI6Q36oPSqi7IgkOKNzaY3C2uFnG2OZcblIhYW3uL4ohNAM3-lOMhAEIyGF24FJK7BZ7Ci0PFTaV0e3sPd8NDolbecxM9HQXntQyfjM3r2q155isTltcZ8aEyjDjLkgtJDJBOMSFc9Qq9RWxZUhi4IzPrUwvmiXDXsWq4xXWtQ75rg4XlmuG-EhDUlmfTA')
        //  window.location.replace("https://dev-01936861.okta.com/oauth2/default/v1/authorize?client_id=0oa44d8plhBY7vOc85d7&redirect_uri=http://localhost:3000/users/auth/oktaoauth/callback&response_type=token&scope=openid+profile+email&state=anyRandomString&nonce=anyRandomString&idp=0oa3v658b8VCLoy3L5d7")
      }
    },
  }
</script>
