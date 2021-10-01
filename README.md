# html2svg
This is the code that how to convert html to svg using dom-to-image.js library. The function toSvg is return the svg in charset=utf-8 instead of base64.
Go with the following examples.

    
    domtoimage.toSvg(document.getElementById('my-node'), {filter: filter})
    .then(function (dataUrl){
        // remove the data:image/svg+xml;charset=utf-8, from the SVG image object
        let s = dataUrl.split("data:image/svg+xml;charset=utf-8,");
        var dataUrl = btoa(unescape(a[1]));
        console.log(dataUrl); // Outputs: "PHN2ZyB4bWxucz0iaHR0"
        // Convert the svg image into base64
        dataUrl = "data:image/svg+xml;base64,"+dataUrl
        console.log(dataUrl); // Outputs: "data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0"
        //Image object
        var img = new Image();
        img.src = dataUrl;
        //append the image in here-appear-theimages div
        document.getElementById("here-appear-theimages").appendChild(img);
        // download the image    
        var downloadLink = document.getElementById('test');
        downloadLink.href = dataUrl;
    });

[toPng](https://github.com/naveenvisions/html2svg#toPixelData)
All the top level functions accept DOM node and rendering options, and return a promise fulfilled with corresponding dataURL:

    •   [toPng](https://github.com/naveenvisions/html-to-image#toPng)
    • toSvg
    • toJpeg 
    • toBlob 
    • toCanvas 
    • toPixelData 

Go with the following examples.

# toPng
Get a PNG image base64-encoded data URL and display it right away:

    var node = document.getElementById('my-node');
    htmlToImage.toPng(node)
      .then(function (dataUrl) {
        var img = new Image();
        img.src = dataUrl;
        document.body.appendChild(img);
      })
      .catch(function (error) {
        console.error('oops, something went wrong!', error);
      });
  
Get a PNG image base64-encoded data URL and download it (using download):

    htmlToImage.toPng(document.getElementById('my-node'))
      .then(function (dataUrl) {
        download(dataUrl, 'my-node.png');
      });
  
# toSvg
Get an SVG data URL, but filter out all the <i> elements:
    
    function filter (node) {
      return (node.tagName !== 'i');
    }
    htmlToImage.toSvg(document.getElementById('my-node'), { filter: filter })
      .then(function (dataUrl) {
        /* do something */
      });
    
# toJpeg
Save and download a compressed JPEG image:
    
    htmlToImage.toJpeg(document.getElementById('my-node'), { quality: 0.95 })
      .then(function (dataUrl) {
        var link = document.createElement('a');
        link.download = 'my-image-name.jpeg';
        link.href = dataUrl;
        link.click();
      });
    
# toBlob
Get a PNG image blob and download it (using FileSaver):
    
    htmlToImage.toBlob(document.getElementById('my-node'))
      .then(function (blob) {
        window.saveAs(blob, 'my-node.png');
      });
    
# toCanvas
Get a HTMLCanvasElement, and display it right away:

    htmlToImage.toCanvas(document.getElementById('my-node'))
      .then(function (canvas) {
        document.body.appendChild(canvas);
      });
    
# toPixelData
Get the raw pixel data as a Uint8Array with every 4 array elements representing the RGBA data of a pixel:
    
    var node = document.getElementById('my-node');
    htmlToImage.toPixelData(node)
      .then(function (pixels) {
        for (var y = 0; y < node.scrollHeight; ++y) {
          for (var x = 0; x < node.scrollWidth; ++x) {
            pixelAtXYOffset = (4 * y * node.scrollHeight) + (4 * x);
            /* pixelAtXY is a Uint8Array[4] containing RGBA values of the pixel at (x, y) in the range 0..255 */
            pixelAtXY = pixels.slice(pixelAtXYOffset, pixelAtXYOffset + 4);
          }
        }
      });
