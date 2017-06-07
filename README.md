# svg_to_pdf

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/0.4.1/html2canvas.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/1.0.272/jspdf.debug.js"></script>

<div id="to-pdf">
  <svg id="myViewer1" width="100px" height="100px" width="1400" height="1400" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
    stroke="green" stroke-width="4" fill="yellow" />
  </svg>
  <hr>
  <canvas id="canvas" width=1800 height=1600>
  </canvas>
</div>

<script type="text/javascript">
var svgText = document.getElementById("myViewer1").outerHTML;
var myCanvas = document.getElementById("canvas");
var ctxt = myCanvas.getContext("2d");

function drawInlineSVG(ctx, rawSVG, callback) {
  var svg = new Blob([rawSVG], {type:"image/svg+xml;charset=utf-8"}),
      domURL = self.URL || self.webkitURL || self,
      url = domURL.createObjectURL(svg),
      img = new Image;

  img.onload = function () {
    ctx.drawImage(this, 0, 0);     
    domURL.revokeObjectURL(url);
    callback(this);
  };
  img.src = url;
}
// usage:
drawInlineSVG(ctxt, svgText, function() {
    console.log(canvas.toDataURL());  // -> PNG
});
var pdf = new jsPDF('p', 'pt', 'a4');
pdf.addHTML(document.body, function() {
  pdf.save('web.pdf');
});


</script>
