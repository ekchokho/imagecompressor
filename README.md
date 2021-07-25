# imagecompress.github.io

<html>
<title>Convert Image to Webp Format</title>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta name="description" content="Jpeg To Webp Converter, Jpeg To Webp Converter Tool, Convert Jpeg To Webp, Compress Webp, Jpg To Webp Python, Jpg To Url, Webp Converter Download Free Convert Jpeg To Webp"/>
	<meta name="robots" content="index,follow" />
	<meta name="keywords" content="Jpeg To Webp Converter, Jpeg To Webp Converter Tool, Convert Jpeg To Webp, Compress Webp, Jpg To Webp Python, Jpg To Url, Webp Converter Download Free Convert Jpeg To Webp" />
     <meta http-equiv="Content-Type" content="text/html;charset=utf-8">
	
	 <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js"></script>
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.1.3/js/bootstrap.min.js"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
  <link rel="icon" href="favicon.png" sizes="16x16" type="image/png">
  <style>
  body {
  width: 100%;
  margin: 0 auto;
  padding: 20px;
  font-family: sans-serif;
}
h1 {
  margin-top: 0;
}
input[type=file] {
  margin: 20px 0;
  margin-left: 10px;
}
img {
  max-height: 100%;
  max-width: 100%;
 
}
.dropTarget {
  position: relative;
  border: 3px dashed silver;
  flex-basis: auto;
  flex-grow: 20;
}
.dropTarget::before {
  content: 'Drop files here';
  color: silver;
  font-size: 5vh;
  height: 5vh;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
  text-align: center;
  pointer-events: none;
  user-select: none;
}
#previews > div {
  box-sizing: border-box;
  height: 240px;
  width: 240px;
  padding: 20px;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  vertical-align: top;
}
#previews > div > progress {
  width: 80%;
}
.layout {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: stretch;
  align-content: stretch;
  height: calc(100vh - 40px);
  margin: 2% auto;
  padding: 15px;
  background-color: #FFFFFF;
  -webkit-box-shadow: 0px 1px 4px 0px rgba(0, 0, 0, 0.2);
  box-shadow: 0px 1px 4px 0px rgba(0, 0, 0, 0.2);
}
.ads {  
   margin: auto;
   padding: 60px 0; 
   max-width: 640px;   
   box-shadow: 0 5px 15px rgba(0,0,0,.16);  
   border-radius: 5px;  
   margin-top: 1em;  
   background: #fff;  
   text-align: left;  
 }
  </style>
</head>
<body style="background-image: linear-gradient(to right, #2d75e1, #00a3ff, #00c6da, #00df87, #a8eb12);">
<div class="container">
  <div class="layout">
  <h1>Convert Image to Webp Format</h1>
  <div>
 
    <input type="file" multiple accept="image/*">
  </div>
  <div id="previews"></div>
  <div class="dropTarget"></div>
</div>
</div>
 </div>
<br>

</body>
<script>
let refs = {};
refs.imagePreviews = document.querySelector('#previews');
refs.fileSelector = document.querySelector('input[type=file]');

function addImageBox(container) {
  let imageBox = document.createElement("div");
  let progressBox = document.createElement("progress");
  imageBox.appendChild(progressBox);
  container.appendChild(imageBox);
  
  return imageBox;
}

function processFile(file) {
  if (!file) {
    return;
  }
  console.log(file);

  let imageBox = addImageBox(refs.imagePreviews);

  // Load the data into an image
  new Promise(function (resolve, reject) {
    let rawImage = new Image();

    rawImage.addEventListener("load", function () {
      resolve(rawImage);
    });

    rawImage.src = URL.createObjectURL(file);
  })
  .then(function (rawImage) {
    // Convert image to webp ObjectURL via a canvas blob
    return new Promise(function (resolve, reject) {
      let canvas = document.createElement('canvas');
      let ctx = canvas.getContext("2d");

      canvas.width = rawImage.width;
      canvas.height = rawImage.height;
      ctx.drawImage(rawImage, 0, 0);

      canvas.toBlob(function (blob) {
        resolve(URL.createObjectURL(blob));
      }, "image/webp");
    });
  })
  .then(function (imageURL) {
    // Load image for display on the page
    return new Promise(function (resolve, reject) {
      let scaledImg = new Image();

      scaledImg.addEventListener("load", function () {
        resolve({imageURL, scaledImg});
      });

      scaledImg.setAttribute("src", imageURL);
    });
  })
  .then(function (data) {
    // Inject into the DOM
    let imageLink = document.createElement("a");

    imageLink.setAttribute("href", data.imageURL);
    imageLink.setAttribute('download', `${file.name}.webp`);
    imageLink.appendChild(data.scaledImg);

    imageBox.innerHTML = "";
    imageBox.appendChild(imageLink);
  });
}

function processFiles(files) {
  for (let file of files) {
    processFile(file);
  }
}

function fileSelectorChanged() {
  processFiles(refs.fileSelector.files);
  refs.fileSelector.value = "";
}

refs.fileSelector.addEventListener("change", fileSelectorChanged);

// Set up Drag and Drop
function dragenter(e) {
  e.stopPropagation();
  e.preventDefault();
}

function dragover(e) {
  e.stopPropagation();
  e.preventDefault();
}

function drop(callback, e) {
  e.stopPropagation();
  e.preventDefault();
  callback(e.dataTransfer.files);
}

function setDragDrop(area, callback) {
  area.addEventListener("dragenter", dragenter, false);
  area.addEventListener("dragover", dragover, false);
  area.addEventListener("drop", function (e) { drop(callback, e); }, false);
}
setDragDrop(document.documentElement, processFiles);
</script>
</html>
© 2021 Ekchokho
