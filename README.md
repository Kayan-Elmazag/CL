<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نموذج جمع البيانات</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 20px;
            background-color: #f4f4f4;
            border-radius: 8px;
        }
        input, textarea {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            background-color: #28a745;
            color: white;
            padding: 10px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
    </style>
</head>
<body>
    <h2>نموذج جمع البيانات</h2>
    <form id="dataForm">
        <label for="name">الاسم:</label>
        <input type="text" id="name" name="name" required>

        <label for="email">البريد الإلكتروني:</label>
        <input type="email" id="email" name="email" required>

        <label for="message">الرسالة:</label>
        <textarea id="message" name="message" rows="4" required></textarea>

        <button type="submit">إرسال</button>
    </form>

    <script>
        document.getElementById('dataForm').onsubmit = function(event) {
            event.preventDefault();

            const formData = new FormData(this);
            const data = {};
            formData.forEach((value, key) => {
                data[key] = value;
            });

            fetch('https://script.google.com/macros/s/AKfycbxXAi-u5T8XWNIrTJIUBmb0JCbIAutpiTGLYr2vPUqAceTryqMXwzRmRYwIw5hpVNa_/exec', {
                method: 'POST',
                body: JSON.stringify(data),
                headers: {
                    'Content-Type': 'application/json'
                }
            })
            .then(response => response.json())
            .then(data => {
                alert('تم إرسال البيانات بنجاح!');
                this.reset();
            })
            .catch(error => {
                console.error('خطأ:', error);
                alert('حدث خطأ أثناء إرسال البيانات.');
            });
        };
    </script>
</body>
</html>
