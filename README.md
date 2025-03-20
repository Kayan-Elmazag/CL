<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نموذج عرض سعر فخم</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/lucide/1.3.0/lucide.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.29.1/moment.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.29.1/locale/ar.js"></script>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f2f4f8;
            direction: rtl;
        }
        .container {
            background-color: #ffffff;
            padding: 1.5rem;
            max-width: 900px;
            margin: auto;
            border-radius: 12px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
            position: relative;
        }
        .header {
            text-align: center;
            margin-bottom: 1.5rem;
            border-bottom: 2px solid #1d4ed8;
            padding-bottom: 0.5rem;
        }
        .header h1 {
            color: #1d4ed8;
            margin: 0;
            font-size: 1.5rem;
        }
        .controls {
            display: flex;
            justify-content: space-between;
            margin-bottom: 1rem;
        }
        .info-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 1rem;
        }
        .info-header input {
            width: 48%;
            padding: 0.5rem;
            border: 1px solid #d1d5db;
            border-radius: 5px;
        }
        .btn {
            padding: 0.5rem 1rem;
            border: none;
            border-radius: 5px;
            color: white;
            cursor: pointer;
            font-size: 0.9rem;
            transition: background-color 0.3s;
        }
        .btn-purple { background-color: #9333ea; }

        .btn:hover {
            filter: brightness(90%);
        }

        .info-container {
            display: flex;
            justify-content: space-between;
            margin-bottom: 1rem;
        }
        .info-box {
            flex: 1;
            padding: .5rem;
            border: 1px solid #e0e0e0;
            border-radius: 2px;
            margin: 0 0.5rem;
            background-color: #fafafa;
        }
        .info-box h2 {
            color: #1d4ed8;
            margin-bottom: 0.5rem;
        }
        .info-field {
            margin-bottom: 0.5rem;
        }
        input[type="text"], input[type="number"], input[type="date"] {
            width: 100%;
            padding: 0.5rem;
            border: 1px solid #d1d5db;
            border-radius: 5px;
        }
        .table-container {
            margin-bottom: 1rem;
            border: 1px solid #d1d5db;
            border-radius: 5px;
            padding: 1rem;
            background-color: #fafafa;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            border: 1px solid #d1d5db;
            padding: 0.5rem;
            text-align: center;
            height: 40px;
        }
        th {
            background-color: #e0f2fe;
            color: #1d4ed8;
        }
        td:first-child {
            width: 40%;
        }
        td:nth-child(2),
        td:nth-child(3),
        td:nth-child(4) {
            width: 15%;
        }
        .footer {
            text-align: center;
            margin-top: 1rem;
            color: #666;
            font-size: 0.875rem;
            padding: 0;
        }
        .totals {
            display: flex;
            justify-content: space-between;
            margin-top: 0;
            font-weight: bold;
        }
        #backgroundImage {
            display: inline-block;
            margin-right: 1rem;
        }
        .image-container {
            text-align: center;
            margin-top: 0;
        }
        .image-container img {
            max-width: 100%;
            height: auto;
        }
        
        /* تعديل جديد لتعليمات الطباعة */
        @media print {
            /* طباعة الحاوية فقط */
            html, body {
                margin: 0 !important;
                padding: 0 !important;
                visibility: hidden !important;
                background-color: white !important;
            }
            
            .container {
                visibility: visible !important;
                position: absolute !important;
                left: 0 !important;
                top: 0 !important;
                width: 100% !important;
                max-width: none !important;
                box-shadow: none !important;
                padding: 10px !important;
                margin: 0 !important;
                border-radius: 0 !important;
            }
            
            /* إخفاء أزرار التحكم */
            .controls, #addItemBtn {
                display: none !important;
            }
            
            /* إخفاء عمود الإجراء */
            th:nth-child(5), 
            td:nth-child(5) {
                display: none !important;
            }
        }
    </style>
</head>
<body>
    <div class="container" id="container">
        <div class="header">
            <h1>عرض سعر</h1>
            <div class="info-header">
                <input type="text" id="offerNumber" placeholder="رقم العرض">
                <input type="date" id="offerDate">
            </div>
        </div>

        <div class="controls">
            <input type="file" id="backgroundImage" accept="image/*" onchange="setBackgroundImage(event)">
            <button id="printBtn" class="btn btn-purple">طباعة</button>
        </div>

        <div class="info-container">
            <div class="info-box">
                <h2>ﻣؤﺳﺳﺔ ﺷيخه ﻋﺑدﷲ اﻟﻧﺗﯾﻔﺎت ﻟﻠﻧﻘﻠﯾﺎت</h2>
                <div class="info-field">
                    <input type="text" id="companyName" placeholder="الرياض">
                </div>
                <div class="info-field">
                    <input type="text" id="companyAddress" placeholder="310822816500003">
                </div>
                <div class="info-field">
                    <input type="text" id="companyPhone" placeholder="0592026994">
                </div>
            </div>
            <div class="info-box">
                <h2>معلومات العميل</h2>
                <div class="info-field">
                    <input type="text" id="clientName" placeholder="اسم العميل">
                </div>
                <div class="info-field">
                    <input type="text" id="clientAddress" placeholder="العنوان">
                </div>
                <div class="info-field">
                    <input type="text" id="clientPhone" placeholder="الهاتف ">
                </div>
            </div>
        </div>

        <div class="table-container">
            <table>
                <thead>
                    <tr>
                        <th>الوصف</th>
                        <th>الكمية</th>
                        <th>السعر (ريال سعودي)</th>
                        <th>الإجمالي (ريال سعودي)</th>
                        <th>إجراء</th>
                    </tr>
                </thead>
                <tbody id="itemsTable">
                    <!-- Items will be added here -->
                </tbody>
            </table>
            <button id="addItemBtn" class="btn btn-purple">إضافة خدمة</button>
        </div>

        <div class="totals">
            <div>
                <strong>المجموع الفرعي:</strong> <span id="subtotal">0.00 ريال سعودي</span><br>
                <strong>الضريبة (15%):</strong> <span id="tax">0.00 ريال سعودي</span><br>
                <strong>الإجمالي:</strong> <span id="total">0.00 ريال سعودي</span>
            </div>
        </div>

        <div class="image-container">
            <img id="background" src="" alt="صورة تحت المجموع" style="display:none;">
        </div>
        
        <div class="footer">
            <p>شكرًا لاختياركم خدمتنا في نقل وتخزين الأثاث. نحن ملتزمون بتقديم أفضل الخدمات. </p>

لأي استفسارات، يرجى الاتصال بنا على الرقم: 0592026994. نتطلع لخدمتكم قريبًا</p>
        </div>
    </div>

    <script>
        // تهيئة التاريخ الحالي
        document.addEventListener('DOMContentLoaded', function() {
            // تعيين التاريخ الحالي
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('offerDate').value = today;
            
            // إضافة عنصر افتراضي عند التحميل
            if (items.length === 0) {
                addItem();
            }
        });

        let items = [];

        // عرض العناصر
        function renderItems() {
            const tbody = document.getElementById('itemsTable');
            tbody.innerHTML = '';
            items.forEach(item => {
                const tr = document.createElement('tr');
                const total = item.quantity * item.price;
                tr.innerHTML = `
                    <td><input type="text" value="${item.description}" placeholder="وصف" onchange="updateItem(${item.id}, 'description', this.value)"></td>
                    <td><input type="number" value="${item.quantity}" onchange="updateItem(${item.id}, 'quantity', this.value)"></td>
                    <td><input type="number" value="${item.price}" onchange="updateItem(${item.id}, 'price', this.value)"></td>
                    <td>${total.toFixed(2)}</td>
                    <td><button onclick="removeItem(${item.id})" class="btn btn-purple">مسح</button></td>
                `;
                tbody.appendChild(tr);
            });
            calculateTotals();
        }

        // حساب المجاميع
        function calculateTotals() {
            let subtotal = items.reduce((sum, item) => sum + (item.quantity * item.price), 0);
            let tax = subtotal * 0.15;
            let total = subtotal + tax;

            document.getElementById('subtotal').textContent = `${subtotal.toFixed(2)} ريال سعودي`;
            document.getElementById('tax').textContent = `${tax.toFixed(2)} ريال سعودي`;
            document.getElementById('total').textContent = `${total.toFixed(2)} ريال سعودي`;
        }

        // إضافة عنصر
        function addItem() {
            const newId = Date.now();
            items.push({ id: newId, description: '', quantity: 1, price: 0 });
            renderItems();
        }

        // زر إضافة عنصر
        document.getElementById('addItemBtn').addEventListener('click', function() {
            addItem();
        });

        // تحديث عنصر
        function updateItem(id, field, value) {
            const item = items.find(i => i.id === id);
            if (item) {
                if (field === 'quantity' || field === 'price') {
                    item[field] = parseFloat(value) || 0;
                } else {
                    item[field] = value;
                }
                renderItems();
            }
        }

        // حذف عنصر
        function removeItem(id) {
            items = items.filter(item => item.id !== id);
            renderItems();
        }

        // دالة الطباعة باستخدام iframe
        document.getElementById('printBtn').addEventListener('click', function() {
            // استخدام طريقة مختلفة للطباعة - مناسبة للموقع
            printDocument();
        });

        // دالة طباعة محسنة
        function printDocument() {
            // إخفاء أزرار التحكم مؤقتًا
            const controls = document.querySelector('.controls');
            const addItemBtn = document.querySelector('#addItemBtn');
            const actionCells = document.querySelectorAll('th:nth-child(5), td:nth-child(5)');
            
            if (controls) controls.style.display = 'none';
            if (addItemBtn) addItemBtn.style.display = 'none';
            actionCells.forEach(cell => {
                if (cell) cell.style.display = 'none';
            });
            
            // طباعة الصفحة
            window.print();
            
            // إعادة العناصر بعد الطباعة
            setTimeout(() => {
                if (controls) controls.style.display = 'flex';
                if (addItemBtn) addItemBtn.style.display = 'block';
                actionCells.forEach(cell => {
                    if (cell) cell.style.display = '';
                });
            }, 1000);
        }

        // تعيين صورة الخلفية
        function setBackgroundImage(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const img = document.getElementById('background');
                    img.src = e.target.result;
                    img.style.display = 'block';
                };
                reader.readAsDataURL(file);
            }
        }
    </script>
</body>
</html>
