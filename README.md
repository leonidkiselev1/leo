<!DOCTYPE html>
<html>
<head>
    <title>Обрезка фото 10×15</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/cropperjs/1.5.12/cropper.min.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/cropperjs/1.5.12/cropper.min.css">
    <style>
        body { font-family: Arial; text-align: center; padding: 20px; }
        #container { max-width: 600px; margin: 0 auto; }
        #image { max-width: 100%; }
        button {
            background: #0088cc;
            color: white;
            border: none;
            padding: 10px 15px;
            margin: 10px;
            cursor: pointer;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <div id="container">
        <h2>Обрежьте фото для печати 10×15</h2>
        <input type="file" id="upload" accept="image/*">
        <div style="margin: 20px 0;">
            <img id="image" style="display: none;">
        </div>
        <button id="crop-btn" disabled>Обрезать</button>
        <a id="download-btn" download="cropped-photo.jpg" style="display: none;">
            <button>Скачать</button>
        </a>
    </div>

    <script>
        let cropper;

        document.getElementById('upload').addEventListener('change', function(e) {
            const file = e.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(event) {
                const img = document.getElementById('image');
                img.src = event.target.result;
                img.style.display = 'block';

                if (cropper) cropper.destroy();
                
                cropper = new Cropper(img, {
                    aspectRatio: 10 / 15,
                    viewMode: 1,
                    autoCropArea: 0.8
                });

                document.getElementById('crop-btn').disabled = false;
            };
            reader.readAsDataURL(file);
        });

        document.getElementById('crop-btn').addEventListener('click', function() {
            const croppedCanvas = cropper.getCroppedCanvas();
            const downloadBtn = document.getElementById('download-btn');
            downloadBtn.href = croppedCanvas.toDataURL('image/jpeg');
            downloadBtn.style.display = 'inline-block';
        });
    </script>
</body>
</html>
