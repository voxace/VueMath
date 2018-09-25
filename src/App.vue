<template>
  <div class="outer">
      <div class="container inner">
          <div class="row">
              <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                  <h1 class="text-center">VueMath</h1>
              </div>
          </div>
          <div class="row">
              <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                  <transition name="flip" mode="out-in">
                      <component :is="mode" @answered="answered($event)" @confirmed="mode = 'app-question'"></component>
                  </transition>
              </div>
              <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 feedback-empty">
                  <transition name="reveal" mode="out-in" v-on:after-enter="afterEnter">
                      <div v-if="feedback" class="alert alert-danger text-center" role="alert">Wrong answer, try again...</div>
                  </transition>
              </div>
          </div>
      </div>
    </div>
</template>

<script>
    import Question from './components/Question.vue';
    import Answer from './components/Answer.vue';

    export default {
        data() {
            return {
                mode: 'app-question',
                feedback: false
            }
        },
        methods: {
          answered(isCorrect) {
              if (isCorrect) {
                  this.mode = 'app-answer';
              } else {
                  this.mode = 'app-question';
                  this.feedback = true;
              }
          },
          afterEnter: function (el) {
            setTimeout(()=>{ this.feedback = false; }, 2000);
          },
        },
        components: {
            appQuestion: Question,
            appAnswer: Answer
        }
    }
</script>

<style>
    @import url('https://fonts.googleapis.com/css?family=Coming+Soon|Rock+Salt');

    body {
        background-image: url(./assets/blackboard.jpg);
        background-position: center;
        background-repeat: no-repeat;
        background-size: auto;
        font-family: 'Coming Soon', cursive;
    }

    h1 {
      color: white;
      padding: 20px;
      font-size: 45px;
      font-family: 'Rock Salt';
      text-shadow: 2px 2px 5px black;
    }

    div.outer {
      height: 95vh;
    }

    div.inner {
      position: relative;
      top: 50%;
      -webkit-transform: translateY(-50%);
      -ms-transform: translateY(-50%);
      transform: translateY(-50%);
    }

    .feedback-empty {
      height: 30px;
    }

    .alert-danger {
      background-color: Red;
      border-color: Black;
      box-shadow: 0px 0px 10px rgba(0,0,0,0.5);
      color: white;
      text-shadow: 2px 2px 5px black;
    }

    .flip-enter {

    }

    .flip-enter-active {
        animation: flip-in  0.5s ease-out forwards;
    }

    .flip-leave {
        /*transform: rotateY(0deg);*/
    }

    .flip-leave-active {
        animation: flip-out 0.5s ease-out forwards;
    }

    @keyframes flip-out {
        from {
            transform: rotateY(0deg);
        }
        to {
            transform: rotateY(90deg);
        }
    }

    @keyframes flip-in {
        from {
            transform: rotateY(90deg);
        }
        to {
            transform: rotateY(0deg);
        }
    }

    .reveal-enter {
        opacity: 0;
    }

    .reveal-enter-active {
        transition: opacity 1s;

    }

    .reveal-leave {

    }

    .reveal-leave-active {
        transition: opacity 1s;
        opacity: 0;
    }
</style>
