<template>
  <div>
    <div class="jumbotron jumbotron-fluid bg-transparent mt-0 mb-0 pb-0">
      <div class="container">
        <div class="row">
          <div class="col-md-6 mb-5 mx-auto">
            <h1 style=" font-family: 'Press Start 2P', 'VT323'; color:#ffffff;text-shadow: 2px 2px #821522; font-size: 22px; font-weight: 700; letter-spacing: 0.1em;" class="text-center title">
            Monokuma - PFP maker
            </h1>
          </div>
        </div>
        <div class="row">
          <div class="col-lg-8 col-xl-6 mx-auto">
            <div class="peep-img-container mx-auto mb-3">
              <Peep style="margin-top:15%; border-radius: 12px;
    border: rgba(0, 0, 0, 0.8)"
                ref="peep"
                :accessories="accessory"
                :body="body"
                :head="head"
                :facial-hair="facial"
                :skin-color="skin"
                :face="face"
                :transparent="transparentOption"
                :background="background"
              />
              <canvas
                ref="canvas"
                class="d-none"
                width="1200"
                height="1200"
              />
            </div>
          </div>
          <div
           style="height: 50%;
  margin: 10%;
  padding: 15px;
           border: 3px outset #5C131F;
  background: rgba(255, 255, 255, 0.9);
  font-family: 'Press Start 2P';font-size: 9px;
  background-clip: padding-box; border-radius: 12px;
    border: 1px solid rgba(255, 255, 255, 0.125);" class="col-lg-8 col-xl-6 mx-auto">
            <div> </div>
            <b-form-group
              label=" Use Transparent background?"
              label-cols-sm="4"
              label-cols-lg="5"
            >
              <b-form-radio-group
                v-model="transparent"
                class="mt-2"
                :options="options"
              />
            </b-form-group>
            <b-form-group
              v-if="transparent === 'no'"
              label="Background color"
              label-cols-sm="4"
              label-cols-lg="5"
            >
              <input
                v-model="background"
                type="color"
                class="mt-2"
                value="#ffffff"
              >
            </b-form-group>
            <b-form-group
              label="🐻 Head"
              label-cols-sm="4"
              label-cols-lg="3"
            >
              <b-form-select
                v-model="accessory"
                :options="accessoryOptions"
                label-field="Head"
              />
            </b-form-group>

            <b-form-group
              label="🕶️ Accessories"
              label-cols-sm="4"
              label-cols-lg="3"
            >
              <b-form-select
                v-model="head"
                :options="headOptions"
                label-field="Head"
              />
            </b-form-group>
            <b-form-group
              label="👕 Clothes"
              label-cols-sm="4"
              label-cols-lg="3"
            >
              <b-form-select
                v-model="face"
                :options="faceOptions"
                label-field="Head"
              />
            </b-form-group>
            <b-form-group
              label="🗡️ Weapons"
              label-cols-sm="4"
              label-cols-lg="3"
            >
              <b-form-select
                v-model="facial"
                :options="facialOptions"
                label-field="Head"
              />
            </b-form-group>

            <b-form-group>
              <button style="border-radius: 12px;
    border: 1px solid rgba(255, 255, 255, 0.125);"
                type="button"
                class="btn btn-block btn-black"
                @click="generateRandom"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  class="mr-3"
                >
                  <polyline points="16 3 21 3 21 8"/>
                  <line
                    x1="4"
                    y1="20"
                    x2="21"
                    y2="3"
                  />
                  <polyline points="21 16 21 21 16 21"/>
                  <line
                    x1="15"
                    y1="15"
                    x2="21"
                    y2="21"
                  />
                  <line
                    x1="4"
                    y1="4"
                    x2="9"
                    y2="9"
                  />
                </svg>
                Random
              </button>
            </b-form-group>
            <b-form-group>
              <button style="border-radius: 12px;
    border: 1px solid rgba(255, 255, 255, 0.125);"
                type="button"
                class="btn btn-block btn-black"
                @click="saveAsPng"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="1.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  class="mr-3"
                >
                  <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/>
                  <polyline points="7 10 12 15 17 10"/>
                  <line
                    x1="12"
                    y1="15"
                    x2="12"
                    y2="3"
                  />
                </svg>
                Png
              </button>
            </b-form-group>

            <b-form-group>

            </b-form-group>

          </div>
        </div>
      </div>
    </div>
    <footer class="text-center pt-4 pb-4">
      <a style="font-size:12px; font-weight:700; padding:3px; background-color: rgba(255, 255, 255, 0.9);"
        href="https://Monokuma.io/"
        target="_blank"
      >return to Main</a>
    </footer>
  </div>
</template>
<script>
import Vue from 'vue'
import dayjs from 'dayjs'
import Canvg from 'canvg'

export default {
  name: 'Home',
  data () {
    return {
      background: '#860606',
      transparent: 'yes',
      options: [
        {
          text: 'Yes',
          value: 'yes'
        },
        {
          text: 'No',
          value: 'no'
        }
      ],
      skinOptions: [
        {
          text: 'Default',
          value: 'white'
        },
        {
          text: 'Skin variation 1',
          value: '#FFDBB4'
        },
        {
          text: 'Skin variation 2',
          value: '#EDB98A'
        },
        {
          text: 'Skin variation 3',
          value: '#D08B5B'
        },
        {
          text: 'Skin variation 4',
          value: '#AE5D29'
        },
        {
          text: 'Skin variation 5',
          value: '#694D3D'
        },
        {
          text: 'Skin variation 6',
          value: '#FFD11B'
        }
      ],
      body: 'BodyTee1',
      head: null,
      face: null,
      skin: null,
      accessory: null,
      facial: null
    }
  },
  computed: {
    transparentOption () {
      return this.transparent === 'no'
    },
    accessoryOptions () {
      const options = [
        {
          value: null,
          text: 'None'
        }
      ]
      return [
        ...options,
        ...Object.keys(Vue.options.components)
          .filter(item => {
            return item.startsWith('Head')
          })
          .map(item => {
            return {
              value: item,
              text: item
            }
          })
      ]
    },
    bodyOptions () {
      return Object.keys(Vue.options.components)
        .filter(item => {
          return item.startsWith('Body')
        })
        .map(item => {
          return {
            value: item,
            text: item
          }
        })
    },
    facialOptions () {
      const options = [
        {
          value: null,
          text: 'None'
        }
      ]
      return [
        ...options,
        ...Object.keys(Vue.options.components)
          .filter(item => {
            return item.startsWith('Weapons')
          })
          .map(item => {
            return {
              value: item,
              text: item
            }
          })
      ]
    },
    headOptions () {
        const options = [
        {
          value: null,
          text: 'None'
        }
      ]
      return [
        ...options,
        ...Object.keys(Vue.options.components)
        .filter(item => {
          return item.startsWith('Accessory')
        })
        .map(item => {
          return {
            value: item,
            text: item
          }
        })
        ]
    },
    faceOptions () {
      const options = [
        {
          value: null,
          text: 'None'
        }
      ]
      return [
        ...options,
      ...Object.keys(Vue.options.components)
        .filter(item => {
          return item.startsWith('Clothes')
        })
        .map(item => {
          return {
            value: item,
            text: item
          }
        })
        ]
    }
  },
  methods: {
    generateRandom () {
      this.head = this.headOptions[Math.floor(Math.random() * this.headOptions.length)].value
      this.body = this.bodyOptions[Math.floor(Math.random() * this.bodyOptions.length)].value
      this.accessory = this.accessoryOptions[Math.floor(Math.random() * this.accessoryOptions.length)].value
      this.facial = this.facialOptions[Math.floor(Math.random() * this.facialOptions.length)].value
      this.face = this.faceOptions[Math.floor(Math.random() * this.faceOptions.length)].value
    },
    async saveAsPng () {
      const html = this.$refs.peep.$el.outerHTML
      var context = this.$refs.canvas.getContext('2d')
      var v = await Canvg.from(context, html)
      v.render()
      this.$refs.canvas.toBlob((blob) => {
        const url = URL.createObjectURL(blob)
        const link = document.createElement('a')
        link.href = url
        link.setAttribute('download', `monokumaBSC.io-pfp-${dayjs().valueOf()}.png`)
        document.body.appendChild(link)
        link.click()
        document.body.removeChild(link)
      }, 'image/png')
    },
    saveAsSvg () {
      const svgData = this.$refs.peep.$el.outerHTML
      console.log(typeof svgData)
      const blob = new Blob([svgData], { type: 'image/svg+xml' })
      const url = URL.createObjectURL(blob)
      const link = document.createElement('a')
      link.href = url
      link.setAttribute('download', `monokumaBSC.io-pfp-${dayjs().valueOf()}.svg`)
      document.body.appendChild(link)
      link.click()
      document.body.removeChild(link)
    }
  }
}
</script>
<style lang="scss" scoped>
.peep-img-container {
  max-height: 500px;

  svg {
    display: block;
    max-width: 500px;
    max-height: 500px;
    margin: 0 auto;

    /*@media (max-width: 800px) {*/
    /*  max-height: 350px;*/
    /*}*/
  }

  /*@media (max-width: 800px) {*/
  /*  max-height: 350px;*/
  /*}*/
}

.btn-black {
  background: #000;
  color: #fff;
  border-color: #000;
  font-weight: 600;
  text-transform: uppercase;
  outline: none;

  &:hover {
    color: #fff;
  }
}

.title {
  font-family: "Playfair Display";
  font-weight: 900;

  @media (max-width: 800px) {
    font-size: 26px;
  }
}

.alt-text {
  font-family: "Ubuntu";
  font-weight: normal;
}

footer {
  font-size: 13px;
}
</style>
