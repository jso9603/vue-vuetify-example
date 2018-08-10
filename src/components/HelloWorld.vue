<template>
  <div class="component">
    <v-flex>
      <span>Alert</span>
      <!-- basic alert -->
      <v-alert
        :value="true"
        type="success"
      >
        This is a success alert.
      </v-alert>
      <v-alert
        :value="true"
        type="info"
      >
        This is a info alert.
      </v-alert>

      <v-alert
        :value="true"
        type="warning"
      >
        This is a warning alert.
      </v-alert>

      <v-alert
        :value="true"
        type="error"
      >
        This is a error alert.
      </v-alert>
      <!-- closable alert -->
      <v-alert
        v-model="alert"
        dismissible
        type="success"
      >
        This is a success alert that is closable.
      </v-alert>

      <div class="text-xs-center">
        <v-btn
          v-if="!alert"
          color="primary"
          dark
          @click="alert = true"
        >
          Reset
        </v-btn>
      </div>
      <div>
        <v-alert
        :value="true"
        color="success"
        icon="check_circle"
        outline
      >
        This is a success alert.
        </v-alert>
        <!-- outline alert -->
        <v-alert
          :value="true"
          color="info"
          icon="info"
          outline
        >
          This is an info alert.
        </v-alert>

        <v-alert
          :value="true"
          color="warning"
          icon="priority_high"
          outline
        >
          This is a warning alert.
        </v-alert>

        <v-alert
          :value="true"
          color="error"
          icon="warning"
          outline
        >
          This is a error alert.
        </v-alert>
      </div>
    </v-flex>

    <!-- avatar -->
    <span>avatar</span>
    <v-container grid-list-md>
      <v-layout row wrap>
        <v-flex xs12 sm6 md4>
          <v-slider
            v-model="slider"
            :min="16"
            :max="256"
            label="Size"
            thumb-label
          ></v-slider>

          <v-switch
            v-model="tile"
            label="Tile"
          ></v-switch>
        </v-flex>

        <v-flex xs12 sm6 md8 align-center justify-center layout text-xs-center>
          <v-avatar
            :tile="tile"
            :size="avatarSize"
            color="grey lighten-4"
          >
            <img src="../assets/logo.png" alt="avatar">
          </v-avatar>
        </v-flex>
      </v-layout>
    </v-container>

    <span>advanced usage</span>
    <v-layout column justify-center>
    <v-subheader>Today</v-subheader>

    <v-expansion-panel popout>
      <v-expansion-panel-content
        v-for="(message, i) in messages"
        :key="i"
        hide-actions
      >
        <v-layout
          slot="header"
          align-center
          row
          spacer
        >
          <v-flex xs4 sm2 md1>
            <v-avatar
              slot="activator"
              size="36px"
            >
              <img
                v-if="message.avatar"
                src="https://avatars0.githubusercontent.com/u/9064066?v=4&s=460"
                alt="Avatar"
              >
              <v-icon
                v-else
                :color="message.color"
                v-text="message.icon"
              ></v-icon>
            </v-avatar>
          </v-flex>

          <v-flex sm5 md3 hidden-xs-only>
            <strong v-html="message.name"></strong>
            <span
              v-if="message.total"
              class="grey--text"
            >
              &nbsp;({{ message.total }})
            </span>
          </v-flex>

          <v-flex no-wrap xs5 sm3>
            <v-chip
              v-if="message.new"
              :color="`${message.color} lighten-4`"
              class="ml-0"
              label
              small
            >
              {{ message.new }} new
            </v-chip>
            <strong v-html="message.title"></strong>
          </v-flex>

          <v-flex
            v-if="message.excerpt"
            class="grey--text"
            ellipsis
            hidden-sm-and-down
          >
            &mdash;
            {{ message.excerpt }}
          </v-flex>
        </v-layout>

        <v-card>
          <v-divider></v-divider>
          <v-card-text v-text="lorem"></v-card-text>
        </v-card>
      </v-expansion-panel-content>
    </v-expansion-panel>
  </v-layout>

  <v-flex>
    <span>avator and badge</span>
    <v-avatar color="teal">
      <span class="white--text headline">C</span>
    </v-avatar>

    <v-badge overlap>
      <span slot="badge">3</span>

      <v-avatar color="purple red--after">
        <v-icon dark>notifications</v-icon>
      </v-avatar>
    </v-badge>

    <v-badge left style="margin-left: 30px; margin-top: 10px;">
      <span slot="badge">6</span>
      <v-icon large color="grey lighten-1">
        shopping_cart
      </v-icon>
    </v-badge>
  </v-flex>

  <v-flex>
    <span>bottm nav</span>
    <v-card height="200px" flat>
      <div class="headline text-xs-center pa-5">
        Active: {{ bottomNav }}
      </div>
      <v-bottom-nav
        :active.sync="bottomNav"
        :value="true"
        absolute
        color="transparent"
      >
        <v-btn color="teal" flat value="recent">
          <span>Recent</span>
          <v-icon>history</v-icon>
        </v-btn>

        <v-btn color="teal" flat value="favorites">
          <span>Favorites</span>
          <v-icon>favorite</v-icon>
        </v-btn>

        <v-btn color="teal" flat value="nearby">
          <span>Nearby</span>
          <v-icon>place</v-icon>
        </v-btn>
      </v-bottom-nav>
    </v-card>

    <v-card height="200px">
      <v-bottom-nav
        :active.sync="bottomNav1"
        :color="color"
        :value="true"
        absolute
        shift
      >
        <v-btn dark>
          <span>Video</span>
          <v-icon>ondemand_video</v-icon>
        </v-btn>

        <v-btn dark>
          <span>Music</span>
          <v-icon>music_note</v-icon>
        </v-btn>

        <v-btn dark>
          <span>Book</span>
          <v-icon>book</v-icon>
        </v-btn>

        <v-btn dark>
          <span>Image</span>
          <v-icon>image</v-icon>
        </v-btn>
      </v-bottom-nav>
    </v-card>
  </v-flex>

  <v-flex>
    <span>bottom sheet</span>
    <div class="text-xs-center">
      <v-bottom-sheet v-model="sheet">
        <v-btn slot="activator" color="purple" dark>
          Click me
        </v-btn>

        <v-list>
          <v-subheader>Open in</v-subheader>
          <v-list-tile
            v-for="tile in tiles"
            :key="tile.title"
            @click="sheet = false"
          >
            <v-list-tile-avatar>
              <v-avatar size="32px" tile>
                <img
                  :src="`https://cdn.vuetifyjs.com/images/bottom-sheets/${tile.img}`"
                  :alt="tile.title"
                >
              </v-avatar>
            </v-list-tile-avatar>
            <v-list-tile-title>{{ tile.title }}</v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-bottom-sheet>
    </div>

    <div class="text-xs-center">
      <v-bottom-sheet inset>
        <v-btn slot="activator" color="red" dark>
          Show player
        </v-btn>

        <v-card tile>
          <v-progress-linear
            :value="50"
            class="my-0"
            height="3"
          ></v-progress-linear>

          <v-list>
            <v-list-tile>
              <v-list-tile-content>
                <v-list-tile-title>The Walker</v-list-tile-title>
                <v-list-tile-sub-title>Fitz & The Trantrums</v-list-tile-sub-title>
              </v-list-tile-content>

              <v-spacer></v-spacer>

              <v-list-tile-action>
                <v-btn icon>
                  <v-icon>fast_rewind</v-icon>
                </v-btn>
              </v-list-tile-action>

              <v-list-tile-action :class="{ 'mx-5': $vuetify.breakpoint.mdAndUp }">
                <v-btn icon>
                  <v-icon>pause</v-icon>
                </v-btn>
              </v-list-tile-action>

              <v-list-tile-action :class="{ 'mr-3': $vuetify.breakpoint.mdAndUp }">
                <v-btn icon>
                  <v-icon>fast_forward</v-icon>
                </v-btn>
              </v-list-tile-action>
            </v-list-tile>
          </v-list>
        </v-card>
      </v-bottom-sheet>
    </div>
  </v-flex>

  <v-flex>
    <span>breadcrumb</span>
    <div>
      <v-breadcrumbs divider="/">
        <v-breadcrumbs-item
          v-for="item in items"
          :key="item.text"
          :disabled="item.disabled"
        >
          {{ item.text }}
        </v-breadcrumbs-item>
      </v-breadcrumbs>

      <v-breadcrumbs divider="-">
        <v-breadcrumbs-item
          v-for="item in items"
          :key="item.text"
          :disabled="item.disabled"
        >
          {{ item.text }}
        </v-breadcrumbs-item>
      </v-breadcrumbs>
    </div>

    <div>
      <v-breadcrumbs>
        <v-icon slot="divider">forward</v-icon>

        <v-breadcrumbs-item
          v-for="item in items"
          :disabled="item.disabled"
          :key="item.text"
        >
          {{ item.text }}
        </v-breadcrumbs-item>
      </v-breadcrumbs>

      <v-breadcrumbs>
        <v-icon slot="divider">chevron_right</v-icon>

        <v-breadcrumbs-item
          v-for="item in items"
          :disabled="item.disabled"
          :key="item.text"
        >
          {{ item.text }}
        </v-breadcrumbs-item>
      </v-breadcrumbs>
    </div>
  </v-flex>

  <v-flex>
    <span>button</span>
    <div>
      <v-btn color="success">Success</v-btn>
      <v-btn color="error">Error</v-btn>
      <v-btn color="warning">Warning</v-btn>
      <v-btn color="info">Info</v-btn>
    </div>

     <div>
      <v-btn flat small>Normal</v-btn>
      <v-btn flat small color="primary">Primary</v-btn>
      <v-btn flat disabled>Disabled</v-btn>
      <v-btn flat large color="error">Error</v-btn>
    </div>
  </v-flex>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  
  data () {
    return {
      // alert
      alert: true,
      // avatar
      slider: 56,
      tile: false,
      messages: [{
        avatar: 'https://avatars0.githubusercontent.com/u/9064066?v=4&s=460',
        name: 'John Leider',
        title: 'Welcome to Vuetify.js!',
        excerpt: 'Thank you for joining our community...'
      },
      {
        color: 'red',
        icon: 'people',
        name: 'Social',
        new: 1,
        total: 3,
        title: 'Twitter'
      },
      {
        color: 'teal',
        icon: 'local_offer',
        name: 'Promos',
        new: 2,
        total: 4,
        title: 'Shop your way',
        exceprt: 'New deals available, Join Today'
      }
    ],
      lorem: 'Lorem ipsum dolor sit amet, at aliquam vivendum vel, everti delicatissimi cu eos. Dico iuvaret debitis mel an, et cum zril menandri. Eum in consul legimus accusam. Ea dico abhorreant duo, quo illum minimum incorrupte no, nostro voluptaria sea eu.',
      // bottom nav
      bottomNav: 'recent',
      bottomNav1: 3,
      // bottom sheet
      sheet: false,
      tiles: [
        { img: 'keep.png', title: 'Keep' },
        { img: 'inbox.png', title: 'Inbox' },
        { img: 'hangouts.png', title: 'Hangouts' },
        { img: 'messenger.png', title: 'Messenger' },
        { img: 'google.png', title: 'Google+' }
      ],
      items: [
        { text: 'Dashboard', disabled: false },
        { text: 'Link 1', disabled: false },
        { text: 'Link 2', disabled: true }
      ]
    }
  },
  computed: {
    avatarSize() {
      return `${this.slider}px`
    },
    color () {
      switch (this.bottomNav1) {
        case 0: return 'blue-grey'
        case 1: return 'teal'
        case 2: return 'brown'
        case 3: return 'indigo'
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
