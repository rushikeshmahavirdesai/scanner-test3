<template>
  <video id="stream" style="width: 100vw; height: 100vh" />
</template>
<script>
(async () => {
  const stream = await navigator.mediaDevices.getUserMedia({
    video: {
      facingMode: {
        ideal: "environment",
      },
    },
    audio: false,
  });
  const videoEl = document.querySelector("#stream");
  videoEl.srcObject = stream;
  await videoEl.play();

  const barcodeDetector = new BarcodeDetector({ formats: ["qr_code", "code_128", "code_39", "code_93", "codabar", "ean_13"] });
  window.setInterval(async () => {
    const barcodes = await barcodeDetector.detect(videoEl);
    if (barcodes.length <= 0) return;
    alert(barcodes.map((barcode) => barcode.rawValue));
  }, 1000);
})();
</script>
