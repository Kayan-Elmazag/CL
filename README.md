<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نموذج جمع البيانات</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        form {
            max-width: 500px;
            margin: 0 auto;
        }
        label {
            display: block;
            margin-top: 10px;
            margin-bottom: 5px;
        }
        input, textarea {
            width: 100%;
            padding: 8px;
            margin-bottom: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        #response {
            margin-top: 20px;
            padding: 10px;
            border-radius: 4px;
        }
        .success {
            background-color: #d4edda;
            color: #155724;
        }
        .error {
            background-color: #f8d7da;
            color: #721c24;
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
    
    <div id="response"></div>
    
    <script>
        document.getElementById('dataForm').addEventListener('submit', function(event) {
            event.preventDefault();
            
            const responseDiv = document.getElementById('response');
            responseDiv.innerHTML = 'جاري إرسال البيانات...';
            responseDiv.className = '';
            
            const formData = new FormData(this);
            const data = Object.fromEntries(formData.entries());
            
            fetch('https://script.google.com/macros/s/AKfycbwCxHlOfIBT0CUgbZZoqpw2AIrMc66yaLF1JwbVWAU0bg7R0dBIkYHdBhKzbko6zyZEgA/exec', {
                method: 'POST',
                body: JSON.stringify(data),
                headers: {
                    'Content-Type': 'application/json'
                },
                mode: 'no-cors' // هذا مهم للتعامل مع Google Apps Script
            })
            .then(response => {
                // نظرًا لاستخدام no-cors، لن نتمكن من قراءة الاستجابة
                // لذلك نفترض أن العملية نجحت إذا لم تكن هناك أخطاء
                responseDiv.innerHTML = 'تم إرسال البيانات بنجاح!';
                responseDiv.className = 'success';
                this.reset();
            })
            .catch(error => {
                console.error('خطأ:', error);
                responseDiv.innerHTML = 'حدث خطأ أثناء إرسال البيانات: ' + error.message;
                responseDiv.className = 'error';
            });
        });
    </script>
</body>
</html>
