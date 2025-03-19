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

        fetch('https://script.google.com/macros/s/AKfycbyNM_JpKQPMr3WRv0ffIvbeS8tTKPGtvm7AkgCmFM8kaEdVjIuTpAAhQ5T53lN7VYg7/exec', {
            method: 'POST',
            body: JSON.stringify(data),
            headers: {
                'Content-Type': 'application/json'
            }
        })
        .then(response => response.json())
        .then(data => {
            document.getElementById('response').innerText = 'تم إرسال البيانات بنجاح!';
            this.reset();
        })
        .catch(error => {
            console.error('خطأ:', error);
            document.getElementById('response').innerText = 'حدث خطأ أثناء إرسال البيانات: ' + error.message;
        });
    };
</script>
