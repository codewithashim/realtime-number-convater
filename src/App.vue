<template>
  <div id="app">
    <main id="container">
      <header id="main_header">
        <h1>Neno Convatrer 👨‍💻</h1>
      </header>
      <section class="number_convater">
        <h1>Number System Convarction</h1>
        <div class="input_grup">
          <label for="desimel">Desimel</label>
          <input
            type="text"
            id="desimel"
            placeholder="Enter Any Desimel Number"
            v-model="number.desimel"
          />
        </div>
        <div class="input_grup">
          <label for="bainary">Baionary</label>
          <input
            type="text"
            id="bainary"
            placeholder="Enter Any Bainary Number"
            v-model="number.bainary"
          />
        </div>
        <div class="input_grup">
          <label for="octal">Octal</label>
          <input
            type="text"
            id="octal"
            placeholder="Enter Any Octal Number"
            v-model="number.octal"
          />
        </div>
        <div class="input_grup">
          <label for="hexadesimel">HexaDesimel</label>
          <input
            type="text"
            id="hexadesime"
            placeholder="Enter Any Baionary Number"
            v-model="number.hexadesimel"
          />
        </div>
        <div class="como_btn">
          <p v-if="invalidNumber" style="color: red">Invalid Input</p>
          <button class="reset_btn" @click="resetNumber">Reset</button>
        </div>
      </section>
      <!-- text convarter -->
      <section class="text_convater">
        <h1>Text System Convarction</h1>

        <div class="input_grup">
          <label for="text_section">Enter Your Text Below</label>
          <textarea
            name=""
            id="text_section"
            cols="30"
            rows="10"
            placeholder="Enter Your Text Hear"
            v-model="lines.text"
          ></textarea>
        </div>
        <div class="height_1_rem"></div>
        <div class="input_grup">
          <label for="bainary_section">Enter Your Bainary Below</label>
          <textarea
            name=""
            id="bainary_section"
            cols="30"
            rows="10"
            placeholder="Enter Your Bainar Hear"
            v-model="lines.bainary"
          ></textarea>
        </div>
        <div class="como_btn text_grupsection">
          <p v-if="invalidLine" style="color: red">Invalid Input</p>
          <button class="reset_btn" @click="resetLines">Reset</button>
        </div>
      </section>
      <footer style="display: flex; justify-content: center; align-items: center;">
			<a href="" style="color:#434343;">&copy; Developed By Codewithashim</a>
		</footer>
    </main>
  </div>
</template>

<script>
// require("@/assets/css/style.css");
require("@/assets/css/style.css");

// comon function

function isBainary(text) {
  for (let t of text) {
    if (t !== "0" && t !== "1") return false;
  }
  return true;
}

function isOctal(text) {
  for (let t of text) {
    if (t < "0" || t > "7") return false;
  }
  return true;
}

function isHexadesimel(text) {
  for (let t of text) {
    if ((t < "0" || t > "9") && (t < "A" || t > "F") && (t < "a" || t > "f"))
      return false;
  }
  return true;
}

//  text convarter start here

function textToBainary(text) {
  const charCodeArray = [];
  for (let i in text) {
    charCodeArray.push(text.charCodeAt(i));
  }

  const bainaryArray = charCodeArray.map((charCode) => {
    return charCode.toString(2);
  });
  return bainaryArray;
}

function bainaryToText(codeArray) {
  let text = "";
  for (let code of codeArray) {
    const char = String.fromCharCode(parseInt(code, 2));
    text = text.concat(char);
  }
  return text;
}

// number convarter end here

export default {
  name: "App",

  created() {
    document.title = "Neno Convatrer";
  },

  // bainding data  of vue

  data() {
    return {
      number: {
        desimel: 0,
        bainary: 0,
        octal: 0,
        hexadesimel: 0,
      },

      lines: {
        text: "",
        bainary: "",
      },
      invalidNumber: false,
      invalidLine: false,
    };
  },
  // use of mathode of vue to reset the data
  methods: {
    resetNumber() {
      (this.number = {
        desimel: 0,
        bainary: 0,
        octal: 0,
        hexadesimel: 0,
      }),
        (this.invalidNumber = false);
    },

    resetLines() {
      (this.lines = {
        text: "",
        bainary: "",
      }),
        (this.invalidLine = false);
    },
  },
  // use of mathode of vue to reset the data
  // use of watcher

  watch: {
    "number.desimel": function (value) {
      this.number.desimel = parseInt(value) || 0;
      this.number.bainary = value.toString(2);
      this.number.octal = value.toString(8);
      this.number.hexadesimel = value.toString(16);
    },
    // end desimel to all

    // start bainary to all
    "number.bainary": function (value) {
      let desimel = parseInt(value, 2);

      if (!isBainary(value)) {
        this.invalidNumber = true;
      } else {
        this.invalidNumber = false;
      }

      this.number.desimel = desimel || 0;
      this.number.bainary = value || 0;
      this.number.octal = desimel.toString(8);
      this.number.hexadesimel = desimel.toString(16);
    },
    // end bainary to all
    // start octal to all
    "number.octal": function (value) {
      let desimel = parseInt(`0${value}`, 8);

      if (!isOctal(value)) {
        this.invalidNumber = true;
      } else {
        this.invalidNumber = false;
      }

      this.number.desimel = desimel || 0;
      this.number.bainary = desimel.toString(2) || 0;
      this.number.octal = value || 0;
      this.number.hexadesimel = desimel.toString(16);
    },
    // end octal to all
    // start hexadesimel to all
    "number.hexadesimel": function (value) {
      let desimel = parseInt(`0x${value}`, 16);

      if (!isHexadesimel(value)) {
        this.invalidNumber = true;
      } else {
        this.invalidNumber = false;
      }
      this.number.desimel = desimel || 0;
      this.number.bainary = desimel.toString(2) || 0;
      this.number.octal = desimel.toString(8) || 0;
      this.number.hexadesimel = value || 0;
    },
    // end hexadesimel to all
    // convar text to bainary
    "lines.text": function (value) {
      if (value.lenght === 0) {
        this.lines.bainary = "";
      } else {
        const codeArray = textToBainary(value);
        this.lines.bainary = codeArray.join(" ");
      }
    },
    // end convar text to bainary
    // start convart bainary to text
    "lines.bainary": function (value) {
      if (value.lenght === 0) {
        this.lines.text = "";
      } else {
        const codeArray = value.split(" ");
        const text = bainaryToText(codeArray);
        this.lines.text = text;
      }
    },

    // end convart bainary to text
  },
};
// end of watcher
</script>
