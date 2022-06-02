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
        this.setToken('eyJraWQiOiJCZlo0LXB3eS1YcE5oN0E2S1p3cFJHRlRkM25MdXlUY1p6c1hxcHdaUkQ4IiwiYWxnIjoiUlMyNTYifQ.eyJ2ZXIiOjEsImp0aSI6IkFULmsxY3drTHdFc1hfNTZnMDRTeTFZUkhDWTJnWlN0U25Sc3U4RTF0YjNqVlkiLCJpc3MiOiJodHRwczovL2Rldi0wMTkzNjg2MS5va3RhLmNvbS9vYXV0aDIvZGVmYXVsdCIsImF1ZCI6ImFwaTovL2RlZmF1bHQiLCJpYXQiOjE2NTM1MDg5ODEsImV4cCI6MTY1MzUxMjU4MSwiY2lkIjoiMG9hNDRkOHBsaEJZN3ZPYzg1ZDciLCJ1aWQiOiIwMHU1MHJ2eXdkOG1HdUp3NzVkNyIsInNjcCI6WyJlbWFpbCIsIm9wZW5pZCIsInByb2ZpbGUiXSwiYXV0aF90aW1lIjoxNjUzNTA4OTgwLCJzdWIiOiJwZXJzb25pY2xlLmRlbW8uYWNjdEBnbWFpbC5jb20ifQ.lG4m4ml6MQ5fkRAdQb02wzxXnuSDLl-A2awYXTsTCa5Orn9LMpS-Rq74xvMuu98Xlo0n5YdtEiVGDRgHgbtBe7PfNBIWz-IMA8eoaOMyvtboQbXKk87YmwsWLVoWh8Lwz5MyYa8TvSeb8mbH9E6fZfoj8jMThXnKkg-fM48NuUS52PZkeRIg840pK-g8gJdlWU2D9spDud-9NJlL1DLu7Et85fUDBIrXAc_cuD7h2jm32fGL9ocW4EhK9E-KrS_LXqoziwzhVXi7RRyLRuJ9VC3mV_mSUfzo6Rzzg6YuBWOAjoMDbfgpzns990337eczwJiuYpsVtyWR36cDjHt3uQ')
        //  window.location.replace("https://dev-01936861.okta.com/oauth2/default/v1/authorize?client_id=0oa44d8plhBY7vOc85d7&redirect_uri=http://localhost:3000/users/auth/oktaoauth/callback&response_type=token&scope=openid+profile+email&state=anyRandomString&nonce=anyRandomString&idp=0oa3v658b8VCLoy3L5d7")
      }
    },
  }
</script>
