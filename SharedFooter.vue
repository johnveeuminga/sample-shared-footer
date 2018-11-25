<template>
  <footer 
    class="footer" 
    id="footer"
  >
    <div class="footer__contents pb-4">
      <div class="container">
        <div class="columns is-mobile is-multiline">
          <div class="footer__col footer__navigation-col column is-one-third-desktop is-full-mobile">
            <template>
              <ul class="footer__navigation" v-if="footerNav.length > 0">
                <li v-for="(navLink, index) in footerNav" :key="`navLink-${index}`">
                  <router-link :to="navLink.link" :target="navLink.openInNewTab &&'_blank' ">{{navLink.label}}</router-link>
                </li>
              </ul>
            </template>
          </div>
          <div class="column is-one-third-desktop is-full-mobile">
            <div class="footer__col footer__logo-col">
              <div class="footer__logo-container" v-if='imgUrl'>
                A project of: <br/>
                <router-link to='/'>
                  <img
                    class='footer__logo'
                    :src="imgUrl"
                    alt="Maximum for Good Logo"
                  >
                </router-link>
              </div>
            </div>
          </div>
          <div class="column is-one-third-desktop is-full-mobile">
            <div class="footer__col footer__logo-col">
              <div class="footer__motto">
                <template v-if="$slots.footer__motto">
                  <slot name="footer__motto"></slot>
                </template>
                <template v-else>
                  <p> Helping non-profits and their supporters <br/> <strong>RAISE MONEY.  RAISE AWARENESS. <br/> CHANGE THE WORLD</strong>  </p>
                  <router-link :to='learnMoreLink' class="button is-primary is-small">Learn More</router-link>
                </template>
             </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="footer__copyright">
      <div class="container-fluid">
        <template v-if="$slots.footer__copyright">
          <slot name="footer__copyright"></slot>
        </template>
        <p> <small>Copyright (c) 2006-2019 DailySource.  All rights reserved.  Terms of Service.</small> </p>
      </div>
    </div>
  </footer>
</template>

<script>
  export default {
    name: 'SharedFooter',

    props: {
      imgUrl: {
        type: String,
      },
      navOptions: {
        type: NavOptions,
      },
      navLinks: {
        type: Array,
        default: () => {
          return []
        },
      },
      learnMoreLink: {
        type: String,
        default: '#'
      }
    },

    data () {
      return {
        defaultNavLinks: [
          {
            link: '#',
            label: 'News',
            openInNewTab: true,
          },
          {
            link: '#',
            label: 'Discussions',
          },
          {
            link: '#',
            label: 'Donate',
          },
          {
            link: '#',
            label: 'Volunteer',
          },
          {
            link: '#',
            label: 'About Us',
          },
          {
            link: '#',
            label: 'Tech Support',
          },
          {
            link: '#',
            label: 'Site Feedback',
          },
          {
            link: '#',
            label: 'Contact Us',
          },
        ]
      }
    },

    methods: {
    },

    computed: {
      footerNav () {
        let navLinks = []
        if (this.footerNavOptions.useDefaultNavLinks) {
          if (this.footerNavOptions.prependLinks) {
            navLinks = [
              ...this.navLinks,
              ...this.defaultNavLinks
            ]
          } else {
            navLinks = [
              ...this.defaultNavLinks,
              ...this.navLinks,
            ]
          }
        } else {
          navLinks = this.navLinks
        }

        return navLinks
      },

      footerNavOptions () {
        return {
          prependLinks: true,
          useDefaultNavLinks: true,
          ...this.navOptions
        }
      }
    },
  }

  /**
   *Footer options object defined here.
   */
  const NavOptions = ({prependLinks, useDefaultNavLinks}) => {
    this.prependLinks = prependLinks
    this.useDefaultNavLinks = useDefaultNavLinks
  }
  
</script>

<style lang="scss">
  #footer {
    padding: 0;
    background-color: $footer-bg;
    border-top: 1px solid darken($footer-bg, 20%);

    p {
      margin-top: 0;
    }
  }

  .footer__contents {
    display: flex;
    justify-content: space-between;
    padding-top: 1em;
    padding-bottom: 1em;
  }

  .footer__navigation {
    list-style: none;
    columns: $footer-nav-columns;
    margin-left: 0;
    padding: 0;
    margin-top: .75em;
  }

  .footer__navigation a,
  .footer__navigation a:visited {
    text-transform: none;
    transition: all .2s ease;
    color: $footer-nav-link-color;

    &:hover {
      color: $footer-nav-link-hover-color;
      font-weight: 700;
    }
  }

  .footer__logo-container { 
    text-align: center; 

    p {
      margin-bottom: .5em;
    }
  }

  .footer__logo-container img { 
    max-width: $footer-logo-max-width; 
    width: 100%;
    margin-top: 0.5em;
  }


  .footer__motto {
    text-align: center;
    line-height: 30px;
  }

  .footer__copyright {
    text-align: center;
    background-color: $footer-copyright-bg;
    padding-bottom: .375em;
    padding-top: .375em;

    p {
      margin-bottom: 0;
      color: #fff;
      text-align: center;
    }
  }
</style>
