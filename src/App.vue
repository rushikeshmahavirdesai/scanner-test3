<!-- <template>
  <div id="{qrcodeRegionId}"></div>
</template>
<script setup>
import { Html5QrcodeScanner } from "html5-qrcode";
</script> -->
<template>
  <div>
    <div id="qr-code-full-region"></div>
    test
    <textarea name="" id="" cols="30" rows="10">{{ this.barcodeDt }}</textarea>
  </div>
</template>

<script>
import { Html5QrcodeScanner } from "html5-qrcode";

export default {
  name: "stream-barcode-reader",
  props: {
    qrbox: {
      type: Number,
      default: 250,
    },
    fps: {
      type: Number,
      default: 10,
    },
  },
  data() {
    return {
      barcodeDt: null,
    };
  },

  mounted() {
    const config = {
      fps: this.fps,
      qrbox: this.qrbox,
    };
    const html5QrcodeScanner = new Html5QrcodeScanner("qr-code-full-region", config);
    html5QrcodeScanner.render(this.onScanSuccess);
  },

  beforeUnmount() {
    this.codeReader.reset();
  },

  methods: {
    onScanSuccess(decodedText, decodedResult) {
      this.barcodeDt = decodedResult;
      this.$emit("result", decodedText, decodedResult);
    },
  },
};
</script>
