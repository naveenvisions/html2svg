# html2svg
This is the code that how to convert html to svg using dom-to-image.js library. The function toSvg is return the svg in charset=utf-8 instead of base64.
Go with the following examples.

domtoimage.toSvg(document.getElementById('my-node'), {filter: filter})
    .then(function (dataUrl) {
        // remove the data:image/svg+xml;charset=utf-8, from the SVG image object
        let s = dataUrl.split("data:image/svg+xml;charset=utf-8,");
        var dataUrl = btoa(unescape(a[1]));
        console.log(dataUrl); // Outputs: "SGVsbG8gV29ybGQh"
        
        // Convert the svg image into base64
        dataUrl = "data:image/svg+xml;base64,"+dataUrl
        console.log(dataUrl); // Outputs: "SGVsbG8gV29ybGQh"
        //Image object
        var img = new Image();
        img.src = dataUrl;
        //append the image in here-appear-theimages div
        document.getElementById("here-appear-theimages").appendChild(img);
        // download the image    
        var downloadLink = document.getElementById('test');
        downloadLink.href = dataUrl;
    });
