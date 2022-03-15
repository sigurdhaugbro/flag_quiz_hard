<template>
   <div class="app">
      <header class="header">
         <button  @click="reload" class="header__reload-button">
            <svg width="34" height="34" viewBox="0 0 34 34" fill="none" xmlns="http://www.w3.org/2000/svg">
               <g clip-path="url(#clip0_2_26)">
               <path d="M33.225 5.0773e-07H30.0767C29.9688 -0.0001213 29.862 0.021675 29.7628 0.0640678C29.6635 0.10646 29.5739 0.168566 29.4994 0.246619C29.4249 0.324672 29.367 0.417046 29.3293 0.518139C29.2915 0.619233 29.2747 0.726939 29.2798 0.834727L29.5455 6.33051C28.0011 4.51063 26.0787 3.0491 23.9122 2.04758C21.7456 1.04607 19.3868 0.528622 17 0.53125C7.92492 0.53125 0.524614 7.93754 0.531254 17.0126C0.537895 26.1023 7.90899 33.4687 17 33.4687C21.078 33.4745 25.0121 31.9615 28.0354 29.2247C28.1162 29.1524 28.1813 29.0644 28.2269 28.9661C28.2725 28.8678 28.2976 28.7612 28.3005 28.6529C28.3035 28.5445 28.2844 28.4367 28.2443 28.336C28.2042 28.2353 28.1439 28.1439 28.0673 28.0673L25.8095 25.8094C25.6666 25.6666 25.4747 25.5834 25.2728 25.5766C25.0708 25.5698 24.8739 25.64 24.7217 25.7729C22.9377 27.3425 20.7176 28.3311 18.3574 28.6067C15.9973 28.8824 13.6091 28.4321 11.5114 27.3159C9.41367 26.1996 7.70602 24.4705 6.61608 22.359C5.52614 20.2475 5.10571 17.8539 5.41083 15.4974C5.71595 13.1408 6.73213 10.9333 8.32389 9.16899C9.91566 7.40471 12.0074 6.16752 14.3202 5.62237C16.6331 5.07722 19.0571 5.24999 21.2693 6.11767C23.4814 6.98534 25.3765 8.50669 26.702 10.4789L19.9597 10.1555C19.8519 10.1504 19.7442 10.1672 19.6431 10.2049C19.542 10.2427 19.4497 10.3006 19.3716 10.3751C19.2936 10.4496 19.2315 10.5392 19.1891 10.6384C19.1467 10.7377 19.1249 10.8445 19.125 10.9524V14.1007C19.125 14.312 19.209 14.5147 19.3584 14.6642C19.5078 14.8136 19.7105 14.8976 19.9219 14.8976H33.225C33.4364 14.8976 33.6391 14.8136 33.7885 14.6642C33.938 14.5147 34.0219 14.312 34.0219 14.1007V0.796875C34.0219 0.585531 33.938 0.382843 33.7885 0.2334C33.6391 0.0839567 33.4364 5.0773e-07 33.225 5.0773e-07Z" fill="black"/>
               </g>
               <defs>
               <clipPath id="clip0_2_26">
               <rect width="34" height="34" fill="white"/>
               </clipPath>
               </defs>
            </svg>
         </button>
         <h2 class="header__points">{{ points }}/{{ numberOfQuestions }} </h2>
      </header>
      <main class="main">
         <figure class="main__flag">
            <img :src="flag" alt="">
         </figure>
         <div class="main__correct">{{ correct }}</div>
         <input class="main__answer" v-model="input" type="text" @keyup.enter="answer" >
      </main>

      <div v-if="finished" class="finished">
         <h1>Good job you got {{ points }} flags correct!</h1>
         <button  @click="reload" class="finished__reload-button">
            <svg width="100" height="100" viewBox="0 0 34 34" fill="none" xmlns="http://www.w3.org/2000/svg">
               <g clip-path="url(#clip0_2_26)">
               <path d="M33.225 5.0773e-07H30.0767C29.9688 -0.0001213 29.862 0.021675 29.7628 0.0640678C29.6635 0.10646 29.5739 0.168566 29.4994 0.246619C29.4249 0.324672 29.367 0.417046 29.3293 0.518139C29.2915 0.619233 29.2747 0.726939 29.2798 0.834727L29.5455 6.33051C28.0011 4.51063 26.0787 3.0491 23.9122 2.04758C21.7456 1.04607 19.3868 0.528622 17 0.53125C7.92492 0.53125 0.524614 7.93754 0.531254 17.0126C0.537895 26.1023 7.90899 33.4687 17 33.4687C21.078 33.4745 25.0121 31.9615 28.0354 29.2247C28.1162 29.1524 28.1813 29.0644 28.2269 28.9661C28.2725 28.8678 28.2976 28.7612 28.3005 28.6529C28.3035 28.5445 28.2844 28.4367 28.2443 28.336C28.2042 28.2353 28.1439 28.1439 28.0673 28.0673L25.8095 25.8094C25.6666 25.6666 25.4747 25.5834 25.2728 25.5766C25.0708 25.5698 24.8739 25.64 24.7217 25.7729C22.9377 27.3425 20.7176 28.3311 18.3574 28.6067C15.9973 28.8824 13.6091 28.4321 11.5114 27.3159C9.41367 26.1996 7.70602 24.4705 6.61608 22.359C5.52614 20.2475 5.10571 17.8539 5.41083 15.4974C5.71595 13.1408 6.73213 10.9333 8.32389 9.16899C9.91566 7.40471 12.0074 6.16752 14.3202 5.62237C16.6331 5.07722 19.0571 5.24999 21.2693 6.11767C23.4814 6.98534 25.3765 8.50669 26.702 10.4789L19.9597 10.1555C19.8519 10.1504 19.7442 10.1672 19.6431 10.2049C19.542 10.2427 19.4497 10.3006 19.3716 10.3751C19.2936 10.4496 19.2315 10.5392 19.1891 10.6384C19.1467 10.7377 19.1249 10.8445 19.125 10.9524V14.1007C19.125 14.312 19.209 14.5147 19.3584 14.6642C19.5078 14.8136 19.7105 14.8976 19.9219 14.8976H33.225C33.4364 14.8976 33.6391 14.8136 33.7885 14.6642C33.938 14.5147 34.0219 14.312 34.0219 14.1007V0.796875C34.0219 0.585531 33.938 0.382843 33.7885 0.2334C33.6391 0.0839567 33.4364 5.0773e-07 33.225 5.0773e-07Z" fill="black"/>
               </g>
               <defs>
               <clipPath id="clip0_2_26">
               <rect width="34" height="34" fill="white"/>
               </clipPath>
               </defs>
            </svg>
         </button>
      </div>
   </div>
   
</template>

<script>
   export default {
         data() {
            return {
               index: 0,
               flag: '',
               countries: [
                  'correctCountry',
               ],
               points: 0,
               numberOfQuestions: 250,
               numberOfAnswers: 0,
               finished: false,
               input: '',
               correct: '',
            }
         },

      async created() {
         this.fetchNew();
      },

      methods: {
         
         answer() {
            if (this.input === this.countries[0]) {
               this.points = (this.points + 1);
            } else {
               console.log(this.countries[0])
               this.correct = this.countries[0]
               // setTimeout(function(){
               //    console.log('blablabla')
               //    this.correct = ''
               // }, 2000)
            }
            this.input = ''
            this.fetchNew()
         },

         async fetchNew() {
            
            const url = 'https://restcountries.com/v3.1/all';
            const res = await fetch(url);
            const result = await res.json();
            
            const correct = Math.floor(Math.random() * this.numberOfQuestions)

            this.flag = result[correct].flags.png
            this.countries[0] = result[correct].name.common

            this.numberOfAnswers += 1

            if(this.numberOfAnswers === this.numberOfQuestions) {
               this.finished = true
            }
         },

         correctAnswer() {
            this.points = (this.points + 1);
            this.fetchNew()
         }, 

         reload() {
            this.fetchNew()
            this.points = 0
            this.finished = false
            this.numberOfAnswers = 0
         },

      }
   }
</script>

<style scoped>
   .app {
      display: grid;
      justify-content: center;
   }

   .header {
      display: flex;
      justify-content: space-between;
      margin: 10px;
      margin-top: 50px;
   }

   .header__reload-button {
      border: none;
      background: none;
   }

   .header__points {
      text-align: right;
      margin: 10px;
      width: fit-content;
      height: fit-content;
   }

   .main {
      display: grid;
      justify-content: center;
   }

   .main__flag {
      margin-top: 20px;
      height: 250px;
   }

   .main__correct {
      text-align: center;
      font-size: 30px;
   }

   .main__answer {
      justify-self: center;
      height: 50px;
      width: 320px;
      margin-top: 20px;
      border: none;
      background: blue;
      font-size: var(--font-size-large)
   }

   .finished {
      position: absolute;
      top: 0;
      left: 0;
      height: 100vh;
      width: 100vw;
      background: rgb(123, 255, 0);
      text-align: center;
   }

   .finished h1 {
      margin-top: 50%;
   }

   .finished__reload-button {
      border: none;
      background: none;
      margin-top: 50%;
   }

</style>