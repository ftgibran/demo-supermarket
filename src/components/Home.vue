<template>
  <div class="supermarket-demo">
    <div class="container">
      <div class="card bg-dark text-white supermarket-panel">
        <div class="card-header">
          <div class="pull-right">
            <a href="//github.com/ftgibran/demo-supermarket" target="_blank" class="btn btn-primary btn-sm">
              <i class="fa fa-github"></i>
              Github
            </a>
          </div>
          <div class="title">
            <i class="fa fa-shopping-cart"></i>
            Supermarket Demo
            <small>by Felipe Gibran</small>
          </div>
        </div>
        <div class="card-body">

          <div class="row h-100">
            <div class="col-lg-7">
              <div class="panel-list text-dark">
                  <div class="row">


                    <div v-for="(item, i) in list" :key="i" class="col-sm-6 col-md-4">
                      <div class="list-item">
                        <div class="icon">
                          <img :src="`./static/img/foods/${item.icon}.svg`" alt="icon"/>
                        </div>
                        <div class="content">
                          <h6 class="mb-1">{{item.name}}</h6>
                          <div class="text-muted">{{(item.price / 100) | R$}}</div>
                          <button @click="addToCart(item)" class="btn btn-primary btn-sm mt-3">
                            <i class="fa fa-plus"></i>
                            Adicionar
                          </button>
                        </div>
                      </div>
                    </div>


                  </div>
              </div>
            </div>
            <div class="col-lg-5">
              <div class="panel-cart card">
                <div class="card-body">
                  <div class="list-group">


                    <div v-for="(cartItem, i) in cart" :key="i" class="cart-item list-group-item list-group-item-action">
                      <div class="icon" v-if="cartItem.item">
                        <img :src="`../static/img/foods/${cartItem.item.icon}.svg`" alt="icon"/>
                      </div>
                      <div class="content" v-if="cartItem.item">
                        <h6 class="mb-1">{{cartItem.item.name}}</h6>
                        <div class="text-muted">{{(cartItem.quant * cartItem.item.price / 100) | R$}}</div>
                        <div class="pull-right">
                          <button @click="removeFromCart(cartItem.item)" class="btn btn-outline-danger btn-sm">
                            <i class="fa fa-trash"></i>
                          </button>
                          <button @click="decrease(cartItem.item)" class="btn btn-outline-danger btn-sm">
                            <i class="fa fa-minus"></i>
                          </button>
                          <button class="btn btn-secondary btn-sm" disabled>{{cartItem.quant}} unid.</button>
                          <button @click="increase(cartItem.item)" class="btn btn-outline-success btn-sm">
                            <i class="fa fa-plus"></i>
                          </button>
                        </div>
                      </div>
                    </div>


                  </div>
                </div>
                <div class="card-footer text-dark">
                  <button class="btn btn-primary btn-sm pull-right">
                    Checkout
                    <i class="fa fa-arrow-right"></i>
                  </button>
                  <strong>Total: </strong>
                  <span>{{(total / 100) | R$}}</span>
                </div>
              </div>
            </div>
          </div>

        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .supermarket-demo {
    height: 100vh;
    padding: 1em 0;
    overflow: hidden;

    @media only screen and (max-width: 991px) {
      height: auto;
      overflow: auto;
    }

    .supermarket-panel {
      display: flex;
      height: calc(100vh - 2em);

      @media only screen and (max-width: 991px) {
        height: auto;
      }

      > .card-header {
        flex: 0;
        .title {
          font-size: 20px;
        }
      }
      > .card-body {
        flex: 1;

        .panel-list {
          background: white;
          border-radius: 0.5em;
          overflow-y: scroll;
          height: calc(100vh - 130px);

          @media only screen and (max-width: 991px) {
            margin-bottom: 1em;
          }

          .row {
            margin: 0;
          }

          .list-item {
            text-align: center;
            margin: 1em 0;
            padding: 1em;
            border-radius: 1em;
            background: whitesmoke;
            &:hover {
              background: antiquewhite;
            }
            > .icon {
              margin-bottom: 0.5em;
              img {
                width: 50%;
              }
            }
          }
        }

        .panel-cart {
          background: white;
          border-radius: 0.5em;

          > .card-body {
            overflow-y: scroll;
            height: calc(100vh - 190px);
            padding: 4px;

            .cart-item {
              display: flex;

              > .icon {
                flex: 0;
                margin-right: 0.5em;
                align-self: center;
                img {
                  width: 50px;
                }
              }

              > .content {
                flex: 1;
              }
            }
          }

        }
      }
      > .card-footer {
        flex: 0;
      }
    }
  }
</style>

<script>
  import _ from 'lodash'
  import list from '../data/supermarket.json'

  export default {
    data () {
      return {
        list,
        cart: []
      }
    },

    filters: {
      /**
       * @return {string}
       */
      R$ (value) {
        let pref = 'R$ '
        let div = ','
        let decimal = commaDecimal(value)

        function commaDecimal (value, precision = 2) {
          let result = Math.round(Number(value) * 10 ** precision) / 10 ** precision
          return result.toString().replace('.', ',')
        }

        // Two Cases: #,% (e.g. 1,9) or #,%% (e.g. 1,99)
        if (decimal.indexOf(div) > 0) {
          let integer = decimal.split(div)[0] // # (e.g. 1)
          let cents = decimal.split(div)[1] // % or %% (e.g. 9 or 99)
          if (cents.length === 1) cents = `${cents}0`

          return `${pref}${integer}${div}${cents}`
        }

        // One Case: # (e.g. 1)
        return `${pref}${decimal}${div}00`
      }
    },

    computed: {
      total () {
        return _.sum(this.cart.map(el => el.item.price * el.quant))
      }
    },

    mounted () {
    },

    methods: {
      itemInCart (item) {
        return this.cart.find(el => el.item === item)
      },
      addToCart (item) {
        let itemInCart = this.itemInCart(item)

        if (!itemInCart) {
          this.cart.push({ item, quant: 1 })
        } else {
          itemInCart.quant += 1
        }
      },
      removeFromCart (item) {
        let itemInCart = this.itemInCart(item)

        if (itemInCart) {
          let i = this.cart.indexOf(itemInCart)
          if (i !== -1) {
            this.cart.splice(i, 1)
          }
        }
      },
      increase (item) {
        let itemInCart = this.itemInCart(item)

        if (itemInCart) {
          itemInCart.quant += 1
        }
      },
      decrease (item) {
        let itemInCart = this.itemInCart(item)

        if (itemInCart && --itemInCart.quant <= 0) {
          let i = this.cart.indexOf(itemInCart)
          if (i !== -1) {
            this.cart.splice(i, 1)
          }
        }
      }
    }
  }
</script>
