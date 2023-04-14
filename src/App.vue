<!-- Use preprocessors via the lang attribute! e.g. <template lang="pug"> -->
<template>
  <div id="app">
    <h1>Type to Search</h1>
  
    <div class="body">
      <input id="searchbox" type="search" placeholder="Search here..." name="text" class="input" autocomplete="off" autofocus>
      <div class="checkbox-wrapper-33">
        <label class="checkbox" >
          <input type="checkbox" class="checkbox__trigger visuallyhidden" v-model="checkedItems.google">
          <span class="checkbox__symbol">
            <svg xmlns="http://www.w3.org/2000/svg" version="1" viewBox="0 0 28 28" height="28px" width="28px"
              class="icon-checkbox" aria-hidden="true">
              <path d="M4 14l8 7L24 7"></path>
            </svg>
          </span>
          <p class="checkbox__textwrapper">Google</p>
        </label>
      </div>
      <div class="checkbox-wrapper-33">
        <label class="checkbox">
          <input type="checkbox" class="checkbox__trigger visuallyhidden" v-model="checkedItems.bing">
          <span class="checkbox__symbol">
            <svg xmlns="http://www.w3.org/2000/svg" version="1" viewBox="0 0 28 28" height="28px" width="28px"
              class="icon-checkbox" aria-hidden="true">
              <path d="M4 14l8 7L24 7"></path>
            </svg>
          </span>
          <p class="checkbox__textwrapper">Bing</p>
        </label>
      </div>
      <div class="checkbox-wrapper-33">
        <label class="checkbox">
          <input type="checkbox" class="checkbox__trigger visuallyhidden" v-model="checkedItems.you">
          <span class="checkbox__symbol">
            <svg xmlns="http://www.w3.org/2000/svg" version="1" viewBox="0 0 28 28" height="28px" width="28px"
              class="icon-checkbox" aria-hidden="true">
              <path d="M4 14l8 7L24 7"></path>
            </svg>
          </span>
          <p class="checkbox__textwrapper">You.com</p>
        </label>
      </div>
      <div class="checkbox-wrapper-33">
          <label class="checkbox" >
            <input type="checkbox" class="checkbox__trigger visuallyhidden" v-model="checkedItems.youtube">
            <span class="checkbox__symbol">
              <svg xmlns="http://www.w3.org/2000/svg" version="1" viewBox="0 0 28 28" height="28px" width="28px"
                class="icon-checkbox" aria-hidden="true">
                <path d="M4 14l8 7L24 7"></path>
              </svg>
            </span>
            <p class="checkbox__textwrapper">Youtube</p>
          </label>
        </div>
      <div class="checkbox-wrapper-33">
        <label class="checkbox">
          <input type="checkbox" class="checkbox__trigger visuallyhidden" v-model="checkedItems.github">
          <span class="checkbox__symbol">
            <svg xmlns="http://www.w3.org/2000/svg" version="1" viewBox="0 0 28 28" height="28px" width="28px"
              class="icon-checkbox" aria-hidden="true">
              <path d="M4 14l8 7L24 7"></path>
            </svg>
          </span>
          <p class="checkbox__textwrapper">GitHub</p>
        </label>
      </div>
      <div class="checkbox-wrapper-33">
        <label class="checkbox">
          <input type="checkbox" class="checkbox__trigger visuallyhidden" v-model="checkedItems.stack">
          <span class="checkbox__symbol">
            <svg xmlns="http://www.w3.org/2000/svg" version="1" viewBox="0 0 28 28" height="28px" width="28px"
              class="icon-checkbox" aria-hidden="true">
              <path d="M4 14l8 7L24 7"></path>
            </svg>
          </span>
          <p class="checkbox__textwrapper">StackOverflow</p>
        </label>
      </div>
      <ButtonPlate @get-checked-values="GetTextFromSearchBox" />
    </div>
    <!-- <button @click="printSelectedItems">Say hello.</button> -->
    <div id="snackbar"></div>
  </div>
</template>

<script>

import ButtonPlate from './components/buttonPlate.vue';


export default {
  components: {
    ButtonPlate,
    
  },
  data() {
    return {
      tabs: 1,
      checkedItems: {
        google: true,
        bing: false,
        you: false,
        github: false,
        stack: false,
        youtube: false
      },
      selectedItems: [],
      searchURLmap: {
        google: 'https://www.google.com/search?q=',
        bing: 'https://www.bing.com/search?q=',
        you: 'https://you.com/search?q=',
        youtube: 'https://www.youtube.com/results?search_query=',
        github: 'https://github.com/search?q=',
        stack: 'https://stackoverflow.com/search?q='
      }
    };
  },
  methods: {
    openTab(link) {
      window.open(link, "_blank");
    },
    Alert(html) {
      var x = document.getElementById("snackbar");
      x.className = "show";
      x.innerHTML = html
      setTimeout(function () { x.className = x.className.replace("show", ""); }, 3000);
    },
    GetTextFromSearchBox() {
      var text = document.getElementById("searchbox").value;
      if (text == "") {
        this.Alert("Enter a search term")
      }
      else {
        this.printSelectedItems(text);
      }
    },
    printSelectedItems(text) {
      this.selectedItems = [];
      Object.keys(this.checkedItems).forEach(key => {
        if (this.checkedItems[key]) {
          this.selectedItems.push(key);
          console.log(key);
        }
      });
      if (this.selectedItems.length == 0) {
        this.Alert("Select atleast One engine")
      }
      else if (this.selectedItems.length == 1) {
        window.location.href=this.searchURLmap[(this.selectedItems[0])]+text
      } else {
        this.selectedItems.forEach(element => {
          this.openTab(this.searchURLmap[element] + text);
        });
      }
    }
  },
  watch:
    {
      checkedItems (val) {
        console.log(val);
      }
    }
  
}
</script>

<!-- Use preprocessors via the lang attribute! e.g. <style lang="scss"> -->
<style>
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  align-items: center;
  justify-content: space-evenly;
  display: flex;
  flex-direction: column;
  background-color: #212121;
}

a,
button {
  color: #4fc08d;
}

button {
  background: none;
  border: solid 1px;
  border-radius: 2em;
  font: inherit;
  padding: 0.75em 2em;
}

h1 {
  font-size: 2em;
  font-weight: normal;
  color: #4fc08d;
}

.input {
  border-radius: 10px;
  outline: 2px solid #63f07f;
  border: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  background-color: #352b2b;
  outline-offset: 3px;
  padding: 10px 1rem;
  transition: 0.5s;
  width: 100%;
  max-width: 500px;
  font-size: 1.5rem;
  margin-bottom: 5%;
  color: rgb(86, 232, 255);
}

.input:focus {
  outline-offset: 10px;
  background-color: #352b2b
}

.checkbox-wrapper-33 {
  --s-xsmall: 0.625em;
  --s-small: 1.2em;
  --border-width: 1px;
  --c-primary: #11e8e1;
  --c-primary-20-percent-opacity: rgba(0, 221, 255, 0.734);
  --c-primary-10-percent-opacity: rgba(0, 255, 55, 0.638);
  --t-base: 0.4s;
  --t-fast: 0.2s;
  --e-in: ease-in;
  --e-out: cubic-bezier(.11, .29, .18, .98);
  margin: 3%;
}

.checkbox-wrapper-33 .visuallyhidden {
  border: 0;
  clip: rect(0 0 0 0);
  height: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
  width: 1px;
}

.checkbox-wrapper-33 .checkbox {
  display: flex;
  align-items: center;
  justify-content: flex-start;
}

.checkbox-wrapper-33 .checkbox+.checkbox {
  margin-top: var(--s-small);
}

.checkbox-wrapper-33 .checkbox__symbol {
  display: inline-block;
  display: flex;
  margin-right: calc(var(--s-small) * 0.7);
  border: var(--border-width) solid var(--c-primary);
  position: relative;
  border-radius: 0.1em;
  width: 1.5em;
  height: 1.5em;
  transition: box-shadow var(--t-base) var(--e-out), background-color var(--t-base);
  box-shadow: 0 0 0 0 var(--c-primary-10-percent-opacity);
}

.checkbox-wrapper-33 .checkbox__symbol:after {
  content: "";
  position: absolute;
  top: 0.5em;
  left: 0.5em;
  width: 0.25em;
  height: 0.25em;
  background-color: var(--c-primary-20-percent-opacity);
  opacity: 0;
  border-radius: 3em;
  transform: scale(1);
  transform-origin: 50% 50%;
}

.checkbox-wrapper-33 .checkbox .icon-checkbox {
  width: 1em;
  height: 1em;
  margin: auto;
  fill: none;
  stroke-width: 3;
  stroke: currentColor;
  stroke-linecap: round;
  stroke-linejoin: round;
  stroke-miterlimit: 10;
  color: var(--c-primary);
  display: inline-block;
}

.checkbox-wrapper-33 .checkbox .icon-checkbox path {
  transition: stroke-dashoffset var(--t-fast) var(--e-in);
  stroke-dasharray: 30px, 31px;
  stroke-dashoffset: 31px;
}

.checkbox-wrapper-33 .checkbox__textwrapper {
  margin: 0;
  color: #11e8e1;
}

.checkbox-wrapper-33 .checkbox__trigger:checked+.checkbox__symbol:after {
  -webkit-animation: ripple-33 1.5s var(--e-out);
  animation: ripple-33 1.5s var(--e-out);
}

.checkbox-wrapper-33 .checkbox__trigger:checked+.checkbox__symbol .icon-checkbox path {
  transition: stroke-dashoffset var(--t-base) var(--e-out);
  stroke-dashoffset: 0px;
}

.checkbox-wrapper-33 .checkbox__trigger:focus+.checkbox__symbol {
  box-shadow: 0 0 0 0.25em var(--c-primary-20-percent-opacity);
}

@-webkit-keyframes ripple-33 {
  from {
    transform: scale(0);
    opacity: 1;
  }

  to {
    opacity: 0;
    transform: scale(20);
  }
}

@keyframes ripple-33 {
  from {
    transform: scale(0);
    opacity: 1;
  }

  to {
    opacity: 0;
    transform: scale(20);
  }
}
#snackbar {
  visibility: hidden; /* Hidden by default. Visible on click */
  min-width: 250px; /* Set a default minimum width */
  margin-left: -125px; /* Divide value of min-width by 2 */
  background-color: #333; /* Black background color */
  color: #fff; /* White text color */
  text-align: center; /* Centered text */
  border-radius: 2px; /* Rounded borders */
  padding: 16px; /* Padding */
  position: fixed; /* Sit on top of the screen */
  z-index: 1; /* Add a z-index if needed */
  left: 50%; /* Center the snackbar */
  bottom: 30px; /* 30px from the bottom */
}

/* Show the snackbar when clicking on a button (class added with JavaScript) */
#snackbar.show {
  visibility: visible; /* Show the snackbar */
  /* Add animation: Take 0.5 seconds to fade in and out the snackbar.
  However, delay the fade out process for 2.5 seconds */
  -webkit-animation: fadein 0.5s, fadeout 0.5s 2.5s;
  animation: fadein 0.5s, fadeout 0.5s 2.5s;
}

/* Animations to fade the snackbar in and out */
@-webkit-keyframes fadein {
  from {bottom: 0; opacity: 0;}
  to {bottom: 30px; opacity: 1;}
}

@keyframes fadein {
  from {bottom: 0; opacity: 0;}
  to {bottom: 30px; opacity: 1;}
}

@-webkit-keyframes fadeout {
  from {bottom: 30px; opacity: 1;}
  to {bottom: 0; opacity: 0;}
}

@keyframes fadeout {
  from {bottom: 30px; opacity: 1;}
  to {bottom: 0; opacity: 0;}
}
</style>