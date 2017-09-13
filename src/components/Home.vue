<template>
  <div class="supermarket-demo">
    <div class="container">
      <div class="card bg-dark text-white supermarket-panel">
        <div class="card-header">
          <div class="pull-right">
            <a href="#" class="btn btn-primary btn-sm">
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


                    <div class="col-sm-6 col-md-4">
                      <div class="list-item">
                        <div class="icon">
                          <img src="../assets/img/foods/apple-1.svg" alt="icon"/>
                        </div>
                        <div class="content">
                          <h6 class="mb-1">List group item heading</h6>
                          <div class="text-muted">R$ 90,00</div>
                          <button class="btn btn-primary btn-sm mt-3">
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


                    <div class="cart-item list-group-item list-group-item-action">
                      <div class="icon">
                        <img src="../assets/img/foods/apple-1.svg" alt="icon"/>
                      </div>
                      <div class="content">
                        <h6 class="mb-1">List group item heading</h6>
                        <div class="text-muted">R$ 90,00</div>
                        <div class="pull-right">
                          <button class="btn btn-outline-danger btn-sm">
                            <i class="fa fa-trash"></i>
                          </button>
                          <button class="btn btn-outline-danger btn-sm">
                            <i class="fa fa-minus"></i>
                          </button>
                          <button class="btn btn-secondary btn-sm" disabled>3 unid.</button>
                          <button class="btn btn-outline-success btn-sm">
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
                  <span>R$ 1000,00</span>
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
  export default {
    data () {
      return {}
    }
  }
</script>
