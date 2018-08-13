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
          v-for="item in bottomItems"
          :key="item.text"
          :disabled="item.disabled"
        >
          {{ item.text }}
        </v-breadcrumbs-item>
      </v-breadcrumbs>

      <v-breadcrumbs divider="-">
        <v-breadcrumbs-item
          v-for="item in bottomItems"
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
          v-for="item in bottomItems"
          :disabled="item.disabled"
          :key="item.text"
        >
          {{ item.text }}
        </v-breadcrumbs-item>
      </v-breadcrumbs>

      <v-breadcrumbs>
        <v-icon slot="divider">chevron_right</v-icon>

        <v-breadcrumbs-item
          v-for="item in bottomItems"
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

    <div>
      <v-btn small color="primary">Primary</v-btn>
      <v-btn color="error">Error</v-btn>
      <v-btn large>Normal</v-btn>
      <v-btn large disabled>Disabled</v-btn>
    </div>

    <div>
      <v-btn depressed small color="primary">Primary</v-btn>
      <v-btn depressed color="error">Error</v-btn>
      <v-btn depressed large>Normal</v-btn>
      <v-btn depressed large disabled>Disabled</v-btn>
    </div>

    <div>
      <span>button dropdown</span>
      <v-container id="dropdown-example" grid-list-xl>
        <v-layout row wrap>
          <v-flex xs12 sm4>
            <p>Overflow</p>

            <v-overflow-btn
              :items="dropdown_font"
              label="Overflow Btn"
              target="#dropdown-example"
            ></v-overflow-btn>
          </v-flex>

          <v-flex xs12 sm4>
            <p>Segmented</p>

            <v-overflow-btn
              :items="dropdown_icon"
              label="Segmented Btn"
              segmented
              target="#dropdown-example"
            ></v-overflow-btn>
          </v-flex>

          <v-flex xs12 sm4>
            <p>Editable</p>

            <v-overflow-btn
              :items="dropdown_edit"
              label="Editable Btn"
              editable
              item-value="text"
            ></v-overflow-btn>
          </v-flex>
        </v-layout>
      </v-container>

      <v-card flat class="py-5">
        <v-card-text>
          <v-container fluid class="pa-0">
            <v-layout row wrap>
              <v-flex xs12 sm6 class="py-2">
                <p>Exclusive</p>
                <v-btn-toggle v-model="toggle_exclusive">
                  <v-btn flat>
                    <v-icon>format_align_left</v-icon>
                  </v-btn>
                  <v-btn flat>
                    <v-icon>format_align_center</v-icon>
                  </v-btn>
                  <v-btn flat>
                    <v-icon>format_align_right</v-icon>
                  </v-btn>
                  <v-btn flat>
                    <v-icon>format_align_justify</v-icon>
                  </v-btn>
                </v-btn-toggle>
              </v-flex>
              <v-flex xs12 sm6 class="py-2">
                <p>Multiple</p>
                <v-btn-toggle v-model="toggle_multiple" multiple>
                  <v-btn flat>
                    <v-icon>format_bold</v-icon>
                  </v-btn>
                  <v-btn flat>
                    <v-icon>format_italic</v-icon>
                  </v-btn>
                  <v-btn flat>
                    <v-icon>format_underlined</v-icon>
                  </v-btn>
                  <v-btn flat>
                    <v-icon>format_color_fill</v-icon>
                  </v-btn>
                </v-btn-toggle>
              </v-flex>
              <v-flex xs12 sm6 class="py-2">
                <p>No Options Selected</p>
                <v-btn-toggle v-model="toggle_none">
                  <v-btn flat>
                    <v-icon>format_align_left</v-icon>
                  </v-btn>
                  <v-btn flat>
                    <v-icon>format_align_center</v-icon>
                  </v-btn>
                  <v-btn flat>
                    <v-icon>format_align_right</v-icon>
                  </v-btn>
                  <v-btn flat>
                    <v-icon>format_align_justify</v-icon>
                  </v-btn>
                </v-btn-toggle>
              </v-flex>
              <v-flex xs12 sm6 class="py-2">
                <p>Mandatory</p>
                <v-btn-toggle v-model="toggle_one" mandatory>
                  <v-btn flat>
                    <v-icon>format_align_left</v-icon>
                  </v-btn>
                  <v-btn flat>
                    <v-icon>format_align_center</v-icon>
                  </v-btn>
                  <v-btn flat>
                    <v-icon>format_align_right</v-icon>
                  </v-btn>
                  <v-btn flat>
                    <v-icon>format_align_justify</v-icon>
                  </v-btn>
                </v-btn-toggle>
              </v-flex>
              <v-flex xs12 sm6 class="py-2">
                <p>Text Options</p>
                <v-btn-toggle v-model="text">
                  <v-btn flat value="left">
                    Left
                  </v-btn>
                  <v-btn flat value="center">
                    Center
                  </v-btn>
                  <v-btn flat value="right">
                    Right
                  </v-btn>
                  <v-btn flat value="justify">
                    Justify
                  </v-btn>
                </v-btn-toggle>
              </v-flex>
              <v-flex xs12 sm6 class="py-2">
                <p>Text &amp; Icon Options</p>
                <v-btn-toggle v-model="icon">
                  <v-btn flat value="left">
                    <span>Left</span>
                    <v-icon>format_align_left</v-icon>
                  </v-btn>
                  <v-btn flat value="center">
                    <span>Center</span>
                    <v-icon>format_align_center</v-icon>
                  </v-btn>
                  <v-btn flat value="right">
                    <span>Right</span>
                    <v-icon>format_align_right</v-icon>
                  </v-btn>
                  <v-btn flat value="justify">
                    <span>Justify</span>
                    <v-icon>format_align_justify</v-icon>
                  </v-btn>
                </v-btn-toggle>
              </v-flex>
            </v-layout>
          </v-container>
        </v-card-text>
      </v-card>
    </div>

    <div>
      <v-btn flat icon color="pink">
        <v-icon>favorite</v-icon>
      </v-btn>
      <v-btn flat icon color="indigo">
        <v-icon>star</v-icon>
      </v-btn>
      <v-btn flat icon color="green">
        <v-icon>cached</v-icon>
      </v-btn>
      <v-btn flat icon color="deep-orange">
        <v-icon>thumb_up</v-icon>
      </v-btn>
      <v-btn icon disabled>
        <v-icon>thumb_up</v-icon>
      </v-btn>
    </div>

    <div>
      <v-btn fab dark small color="primary">
        <v-icon dark>remove</v-icon>
      </v-btn>
      <v-btn fab dark color="teal">
        <v-icon dark>list</v-icon>
      </v-btn>
      <v-btn fab dark large color="purple">
        <v-icon dark>android</v-icon>
      </v-btn>
    </div>

    <div>
      <v-btn
        :loading="loading3"
        :disabled="loading3"
        color="blue-grey"
        class="white--text"
        @click.native="loader = 'loading3'"
      >
        Upload
        <v-icon right dark>cloud_upload</v-icon>
      </v-btn>

      <v-btn
        :loading="loading2"
        :disabled="loading2"
        color="success"
        @click.native="loader = 'loading2'"
      >
        Custom Loader
        <span slot="loader">Loading...</span>
      </v-btn>

      <v-btn
        :loading="loading4"
        :disabled="loading4"
        color="info"
        @click.native="loader = 'loading4'"
      >
        Icon Loader
        <span slot="loader" class="custom-loader">
          <v-icon light>cached</v-icon>
        </span>
      </v-btn>
    </div>

    <div>
      <v-btn outline color="indigo">Outline Button</v-btn>
      <v-btn outline fab color="teal">
        <v-icon>list</v-icon>
      </v-btn>
      <v-btn outline large fab color="indigo">
        <v-icon>edit</v-icon>
      </v-btn>
    </div>

    <div>
      <v-btn round color="primary" dark>Rounded Button</v-btn>
      <v-btn block color="secondary" dark>Block Button</v-btn>
    </div>
  </v-flex>

  <v-flex>
    <span>card</span>
    <div>
      <v-flex xs6 sm3>
        <v-card>
          <v-card-media
            class="white--text"
            height="200px"
            src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
          >
            <v-container fill-height fluid>
              <v-layout fill-height>
                <v-flex xs12 align-end flexbox>
                  <span class="headline">Top 10 Australian beaches</span>
                </v-flex>
              </v-layout>
            </v-container>
          </v-card-media>
          <v-card-title>
            <div>
              <span class="grey--text">Number 10</span><br>
              <span>Whitehaven Beach</span><br>
              <span>Whitsunday Island, Whitsunday Islands</span>
            </div>
          </v-card-title>
          <v-card-actions>
            <v-btn flat color="orange">Share</v-btn>
            <v-btn flat color="orange">Explore</v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>

      <v-flex xs6 sm5>
        <v-card>
          <v-card-media
            src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
            height="200px"
          >
          </v-card-media>

          <v-card-title primary-title>
            <div>
              <div class="headline">Top western road trips</div>
              <span class="grey--text">1,000 miles of wonder</span>
            </div>
          </v-card-title>

          <v-card-actions>
            <v-btn flat>Share</v-btn>
            <v-btn flat color="purple">Explore</v-btn>
            <v-spacer></v-spacer>
            <v-btn icon @click="show = !show">
              <v-icon>{{ show ? 'keyboard_arrow_down' : 'keyboard_arrow_up' }}</v-icon>
            </v-btn>
          </v-card-actions>

          <v-slide-y-transition>
            <v-card-text v-show="show">
              I'm a thing. But, like most politicians, he promised more than he could deliver. You won't have time for sleeping, soldier, not with all the bed making you'll be doing. Then we'll go with that data file! Hey, you add a one and two zeros to that or we walk! You're going to do his laundry? I've got to find a way to escape.
            </v-card-text>
          </v-slide-y-transition>
        </v-card>
      </v-flex>
    </div>
  </v-flex>

  <v-flex>
    <span>carousel</span>
    <v-carousel>
      <!-- <v-carousel
    delimiter-icon="stop"
    prev-icon="mdi-arrow-left"
    next-icon="mdi-arrow-right"
  > -->
      <v-carousel-item
        v-for="(item,i) in carousels"
        :key="i"
        :src="item.src"
      ></v-carousel-item>
    </v-carousel>
  </v-flex>

  <v-flex>
    <span>chip</span>
    <v-chip color="secondary" text-color="white">Secondary</v-chip>
    <v-chip color="primary" text-color="white">
      1 Year
      <v-icon right>cake</v-icon>
    </v-chip>
    <v-chip outline color="primary">Colored</v-chip>
    <v-chip label color="pink" text-color="white">
      <v-icon left>label</v-icon>Tags
    </v-chip>
    <v-chip v-model="chip" close color="green" outline>Success</v-chip>

    <v-combobox v-model="chips" :items="chipsItems" label="Your favorite hobbies" chips clearable prepend-icon="filter_list" solo multiple>
      <template slot="selection" slot-scope="data">
        <v-chip :selected="data.selected" close @input="remove(data.item)">
          <strong>{{ data.item }}</strong>&nbsp;
          <span>(interest)</span>
        </v-chip>
      </template>
    </v-combobox>
  </v-flex>

  <v-flex>
    <span>data iterator</span>
    <v-container fluid grid-list-md>
    <v-data-iterator
      :items="dataItems"
      :rows-per-page-items="rowsPerPageItems"
      :pagination.sync="pagination"
      content-tag="v-layout"
      row
      wrap
    >
      <v-flex slot="item" slot-scope="props" xs12 sm6 md4 lg3>
        <v-card>
          <v-card-title><h4>{{ props.item.name }}</h4></v-card-title>
          <v-divider></v-divider>
          <v-list dense>
            <v-list-tile>
              <v-list-tile-content>Calories:</v-list-tile-content>
              <v-list-tile-content class="align-end">{{ props.item.calories }}</v-list-tile-content>
            </v-list-tile>
            <v-list-tile>
              <v-list-tile-content>Fat:</v-list-tile-content>
              <v-list-tile-content class="align-end">{{ props.item.fat }}</v-list-tile-content>
            </v-list-tile>
            <v-list-tile>
              <v-list-tile-content>Carbs:</v-list-tile-content>
              <v-list-tile-content class="align-end">{{ props.item.carbs }}</v-list-tile-content>
            </v-list-tile>
            <v-list-tile>
              <v-list-tile-content>Protein:</v-list-tile-content>
              <v-list-tile-content class="align-end">{{ props.item.protein }}</v-list-tile-content>
            </v-list-tile>
            <v-list-tile>
              <v-list-tile-content>Sodium:</v-list-tile-content>
              <v-list-tile-content class="align-end">{{ props.item.sodium }}</v-list-tile-content>
            </v-list-tile>
            <v-list-tile>
              <v-list-tile-content>Calcium:</v-list-tile-content>
              <v-list-tile-content class="align-end">{{ props.item.calcium }}</v-list-tile-content>
            </v-list-tile>
            <v-list-tile>
              <v-list-tile-content>Iron:</v-list-tile-content>
              <v-list-tile-content class="align-end">{{ props.item.iron }}</v-list-tile-content>
            </v-list-tile>
          </v-list>
        </v-card>
      </v-flex>
    </v-data-iterator>
  </v-container>
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
      bottomItems: [
        { text: 'Dashboard', disabled: false },
        { text: 'Link 1', disabled: false },
        { text: 'Link 2', disabled: true }
      ],
      //button dropdown
      dropdown_font: ['Arial', 'Calibri', 'Courier', 'Verdana'],
      dropdown_icon: [
        { text: 'list', callback: () => console.log('list') },
        { text: 'favorite', callback: () => console.log('favorite') },
        { text: 'delete', callback: () => console.log('delete') }
      ],
      dropdown_edit: [
        { text: '100%' },
        { text: '75%' },
        { text: '50%' },
        { text: '25%' },
        { text: '0%' }
      ],
      // toggle button
      text: 'center',
      icon: 'justify',
      toggle_none: null,
      toggle_one: 0,
      toggle_exclusive: 2,
      toggle_multiple: [0, 1, 2],
      // loaders
      loader: null,
      loading: false,
      loading2: false,
      loading3: false,
      loading4: false,
      // card
      show: false,
      // carousel
      carousels: [
          { src: 'https://cdn.vuetifyjs.com/images/carousel/squirrel.jpg' },
          { src: 'https://cdn.vuetifyjs.com/images/carousel/sky.jpg' },
          { src: 'https://cdn.vuetifyjs.com/images/carousel/bird.jpg' },
          { src: 'https://cdn.vuetifyjs.com/images/carousel/planet.jpg' }
        ],
      // chip
      chip: true,
      chips: ['Programming', 'Playing video games', 'Watching movies', 'Sleeping'],
      chipsItems: ['Streaming', 'Eating'],
      // data iterator
      rowsPerPageItems: [4, 8, 12],
      pagination: {
        rowsPerPage: 4
      },
      dataItems: [
        {
          value: false,
          name: 'Frozen Yogurt',
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          sodium: 87,
          calcium: '14%',
          iron: '1%'
        },
        {
          value: false,
          name: 'Ice cream sandwich',
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          sodium: 129,
          calcium: '8%',
          iron: '1%'
        },
        {
          value: false,
          name: 'Eclair',
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          sodium: 337,
          calcium: '6%',
          iron: '7%'
        },
        {
          value: false,
          name: 'Cupcake',
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          sodium: 413,
          calcium: '3%',
          iron: '8%'
        },
        {
          value: false,
          name: 'Gingerbread',
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          sodium: 327,
          calcium: '7%',
          iron: '16%'
        },
        {
          value: false,
          name: 'Jelly bean',
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          sodium: 50,
          calcium: '0%',
          iron: '0%'
        },
        {
          value: false,
          name: 'Lollipop',
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          sodium: 38,
          calcium: '0%',
          iron: '2%'
        },
        {
          value: false,
          name: 'Honeycomb',
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          sodium: 562,
          calcium: '0%',
          iron: '45%'
        },
        {
          value: false,
          name: 'Donut',
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          sodium: 326,
          calcium: '2%',
          iron: '22%'
        }
      ]
    }
  },
  watch: {
    loader () {
      const l = this.loader
      this[l] = !this[l]

      setTimeout(() => (this[l] = false), 3000)

      this.loader = null
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
  },
  method: {
    remove (item) {
      this.chips.splice(this.chips.indexOf(item), 1)
      this.chips = [...this.chips]
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

/* loaders */
.custom-loader {
    animation: loader 1s infinite;
    display: flex;
  }
  @-moz-keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
  @-webkit-keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
  @-o-keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
  @keyframes loader {
    from {
      transform: rotate(0);
    }
    to {
      transform: rotate(360deg);
    }
  }
</style>
