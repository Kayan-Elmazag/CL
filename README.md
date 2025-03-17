<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>فاتورة ضريبية - شركة نقل أثاث</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.17.5/xlsx.full.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/FileSaver.js/2.0.5/FileSaver.min.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700&display=swap');
        
        * {
            font-family: 'Tajawal', sans-serif;
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            padding: 20px;
            background-color: #f8f9fa;
            color: #333;
        }
        
        .invoice-container {
            max-width: 800px;
            margin: 0 auto;
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
            position: relative;
            overflow: hidden;
        }
        
        .corner-icon {
            position: absolute;
            width: 80px;
            height: 80px;
            opacity: 0.1;
            color: #28a745;
        }
        
        .top-right {
            top: 0;
            right: 0;
        }
        
        .top-left {
            top: 0;
            left: 0;
        }
        
        .bottom-right {
            bottom: 0;
            right: 0;
        }
        
        .bottom-left {
            bottom: 0;
            left: 0;
        }
        
        .header {
            text-align: center;
            margin-bottom: 20px;
            position: relative;
        }
        
        h1 {
            color: #28a745;
            font-size: 20px;
            margin-bottom: 5px;
            text-align: center;
        }
        
        .invoice-title {
            display: flex;
            justify-content: space-between;
            margin-bottom: 15px;
            border-bottom: 2px solid #28a745;
            padding-bottom: 10px;
        }
        
        .invoice-number {
            font-weight: bold;
            color: #28a745;
            font-size: 14px;
        }
        
        .section {
            margin-bottom: 15px;
            padding: 10px;
            border-radius: 5px;
            background-color: #f8f9fa;
            border: 1px solid #e9ecef;
        }
        
        .section h2 {
            margin-bottom: 8px;
            color: #28a745;
            font-size: 16px;
            border-bottom: 1px solid #dee2e6;
            padding-bottom: 5px;
        }
        
        .flex-container {
            display: flex;
            gap: 15px;
            margin-bottom: 15px;
        }
        
        .flex-container .section {
            flex: 1;
            padding: 8px;
            margin-bottom: 8px;
        }
        
        .field {
            margin-bottom: 6px;
        }
        
        label {
            display: block;
            margin-bottom: 3px;
            font-weight: 500;
            font-size: 12px;
        }
        
        input, textarea {
            width: 100%;
            padding: 5px;
            border: 1px solid #ced4da;
            border-radius: 4px;
            font-size: 12px;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 15px;
        }
        
        th, td {
            padding: 8px 5px;
            text-align: right;
            border-bottom: 1px solid #dee2e6;
            font-size: 12px;
        }
        
        th {
            background-color: #f1f8e9;
            color: #28a745;
            font-weight: 600;
        }
        
        tfoot td {
            font-weight: bold;
            border-top: 2px solid #28a745;
        }
        
        .action-buttons {
            text-align: center;
            margin: 15px 0;
        }
        
        button {
            padding: 6px 12px;
            margin: 0 5px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.3s;
            font-size: 12px;
        }
        
        .btn-primary {
            background-color: #28a745;
            color: white;
        }
        
        .btn-secondary {
            background-color: #6c757d;
            color: white;
        }
        
        .btn-danger {
            background-color: #dc3545;
            color: white;
        }
        
        button:hover {
            opacity: 0.9;
            transform: translateY(-2px);
        }
        
        .summary-section {
            display: flex;
            justify-content: flex-end;
        }
        
        .summary {
            width: 250px;
        }
        
        .summary-row {
            display: flex;
            justify-content: space-between;
            padding: 6px 0;
            border-bottom: 1px solid #dee2e6;
            font-size: 12px;
        }
        
        .summary-row:last-child {
            border-bottom: 2px solid #28a745;
            font-weight: bold;
            font-size: 14px;
        }
        
        .tax-info {
            margin-top: 15px;
            font-size: 12px;
            text-align: center;
            color: #6c757d;
        }
        
        .hidden-print {
            margin-top: 15px;
            text-align: center;
            font-size: 10px;
            color: #6c757d;
        }
    </style>
</head>
<body>
    <div class="invoice-container">
        <!-- Corner Icons -->
        <i class="fas fa-truck-moving corner-icon top-right"></i>
        <i class="fas fa-couch corner-icon top-left"></i>
        <i class="fas fa-box-open corner-icon bottom-right"></i>
        <i class="fas fa-boxes corner-icon bottom-left"></i>
        
        <!-- Header -->
        <div class="header">
            <h1>ﻣﺆﺳﺴﺔ ﺷﻴﺨﻪ ﻋﺒﺪﺍﻟﻠﻠﻪ ﺍﻟﻨﺘﻴﻔﺎﺕ ﻟﻠﻨﻘﻠﻴﺎﺕ</h1>
            <p>خدمات نقل احترافية - سرعة ودقة في التنفيذ</p>
        </div>
        
        <div class="invoice-title">
            <div>
                <h2>فاتورة ضريبية</h2>
                <p>--------------------------------</p>
            </div>
            <div class="invoice-number">
                <p>رقم الفاتورة: <input type="text" id="invoiceNumber" value="INV-2025-0001"></p>
                <p>تاريخ الإصدار: <input type="date" id="invoiceDate" value="2025-03-14"></p>
            </div>
        </div>
        
        <!-- Company and Client Info -->
        <div class="flex-container">
            <div class="section">
                <h2>بيانات الشركة</h2>
                <div class="field">
                    <label for="companyName">اسم الشركة:</label>
                    <input type="text" id="companyName" value="ﻣؤﺳﺳﺔ ﺷيخه ﻋﺑدﷲ اﻟﻧﺗﯾﻔﺎت ﻟﻠﻧﻘﻠﯾﺎت">
                </div>
                <div class="field">
                    <label for="companyTaxNumber">الرقم الضريبي:</label>
                    <input type="text" id="companyTaxNumber" value="310822816500003">
                </div>
                <div class="field">
                    <label for="companyAddress">العنوان:</label>
                    <textarea id="companyAddress" rows="2">الرياض، المملكة العربية السعودية</textarea>
                </div>
                <div class="field">
                    <label for="companyContact">رقم التواصل:</label>
                    <input type="text" id="companyContact" value="0592026994">
                </div>
            </div>
            
            <div class="section">
                <h2>بيانات العميل</h2>
                <div class="field">
                    <label for="clientName">اسم العميل:</label>
                    <input type="text" id="clientName" value="">
                </div>
                <div class="field">
                    <label for="clientTaxNumber">الرقم الضريبي / رقم الهوية:</label>
                    <input type="text" id="clientTaxNumber" value="">
                </div>
                <div class="field">
                    <label for="clientAddress">العنوان:</label>
                    <textarea id="clientAddress" rows="2"></textarea>
                </div>
                <div class="field">
                    <label for="clientContact">رقم التواصل:</label>
                    <input type="text" id="clientContact" value="">
                </div>
            </div>
        </div>
        
        <!-- Invoice Items Table -->
        <div class="section">
            <h2>تفاصيل الخدمات</h2>
            <table id="invoiceTable">
                <thead>
                    <tr>
                        <th width="5%">#</th>
                        <th width="40%">الخدمة / المنتج</th>
                        <th width="15%">الكمية</th>
                        <th width="20%">السعر الوحدة (ريال)</th>
                        <th width="20%">المجموع (ريال)</th>
                        <th width="10%" class="btn-remove-row">حذف</th>
                    </tr>
                </thead>
                <tbody id="invoiceItems">
                    <tr>
                        <td>1</td>
                        <td><input type="text" class="item-name" value="خدمة نقل أثاث منزلي"></td>
                        <td><input type="number" class="item-quantity" value="1" min="1" onchange="calculateRowTotal(this)"></td>
                        <td><input type="number" class="item-price" value="1000" min="0" onchange="calculateRowTotal(this)"></td>
                        <td class="row-total">1000.00</td>
                        <td class="btn-remove-row"><button class="btn-danger" onclick="removeRow(this)">حذف</button></td>
                    </tr>
                </tbody>
            </table>
            
            <button class="btn-primary btn-add-row" onclick="addNewRow()">إضافة منتج / خدمة</button>
            
            <div class="summary-section">
                <div class="summary">
                    <div class="summary-row">
                        <span>المجموع قبل الضريبة:</span>
                        <span id="subtotal">1000.00 ريال</span>
                    </div>
                    <div class="summary-row">
                        <span>ضريبة القيمة المضافة (15%):</span>
                        <span id="tax">150.00 ريال</span>
                    </div>
                    <div class="summary-row">
                        <span>الإجمالي:</span>
                        <span id="total">1150.00 ريال</span>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Terms and Notes -->
        <div class="section">
            <h2>ملاحظات وشروط</h2>
            <textarea id="notes" rows="3" placeholder="أي ملاحظات إضافية..."></textarea>
        </div>
        
        <!-- Action Buttons -->
        <div class="action-buttons">
            <button class="btn-primary" onclick="printInvoice()">طباعة الفاتورة</button>
            <button class="btn-secondary" onclick="exportToExcel()">تصدير إلى Excel</button>
        </div>
        
        <div class="tax-info">
            <p>فاتورة ضريبية صادرة وفق أنظمة الضريبة في المملكة العربية السعودية</p>
        </div>
    </div>

    <script>
        function addNewRow() {
            const table = document.getElementById('invoiceItems');
            const rowCount = table.rows.length;
            const newRow = table.insertRow(rowCount);
            newRow.innerHTML = `
                <td>${rowCount + 1}</td>
                <td><input type="text" class="item-name" value="خدمة جديدة"></td>
                <td><input type="number" class="item-quantity" value="1" min="1" onchange="calculateRowTotal(this)"></td>
                <td><input type="number" class="item-price" value="0" min="0" onchange="calculateRowTotal(this)"></td>
                <td class="row-total">0.00</td>
                <td class="btn-remove-row"><button class="btn-danger" onclick="removeRow(this)">حذف</button></td>
            `;
            calculateTotals();
        }

        function removeRow(button) {
            const row = button.closest('tr');
            row.remove();
            calculateTotals();
        }

        function calculateRowTotal(input) {
            const row = input.closest('tr');
            const quantity = parseFloat(row.querySelector('.item-quantity').value);
            const price = parseFloat(row.querySelector('.item-price').value);
            const total = quantity * price;
            row.querySelector('.row-total').textContent = total.toFixed(2);
            calculateTotals();
        }

        function calculateTotals() {
            let subtotal = 0;
            document.querySelectorAll('.row-total').forEach(cell => {
                subtotal += parseFloat(cell.textContent);
            });
            const tax = subtotal * 0.15;
            const total = subtotal + tax;

            document.getElementById('subtotal').textContent = subtotal.toFixed(2) + ' ريال';
            document.getElementById('tax').textContent = tax.toFixed(2) + ' ريال';
            document.getElementById('total').textContent = total.toFixed(2) + ' ريال';
        }

        function printInvoice() {
            const invoiceContent = document.querySelector('.invoice-container').innerHTML;
            const printWindow = window.open('', '', 'width=800,height=600');
            printWindow.document.write(`
                <html dir="rtl" lang="ar">
                <head>
                    <title>طباعة الفاتورة</title>
                    <style>
                        @import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700&display=swap');
                        * {
                            font-family: 'Tajawal', sans-serif;
                            box-sizing: border-box;
                            margin: 0;
                            padding: 0;
                        }
                        body {
                            padding: 20px;
                            background-color: #fff;
                            color: #333;
                        }
                        .invoice-container {
                            max-width: 800px;
                            margin: 0 auto;
                            background-color: #fff;
                            padding: 20px;
                            border-radius: 10px;
                            box-shadow: none;
                            border: none;
                        }
                        input, textarea {
                            border: none;
                            padding: 0;
                            font-size: 12px;
                        }
                        .section {
                            border: none;
                            padding: 5px 0;
                            background-color: transparent;
                        }
                        .header {
                            margin-bottom: 10px;
                        }
                        .flex-container {
                            margin-bottom: 10px;
                        }
                        table {
                            margin-bottom: 10px;
                        }
                        th, td {
                            padding: 5px 3px;
                        }
                        .action-buttons, .btn-add-row, .btn-remove-row, .hidden-print {
                            display: none !important;
                        }
                    </style>
                </head>
                <body>
                    ${invoiceContent}
                    <script>
                        window.onload = function() {
                            window.print();
                            window.close();
                        };
                    <\/script>
                </body>
                </html>
            `);
            printWindow.document.close();
        }

        function exportToExcel() {
            const table = document.getElementById('invoiceTable');
            const wb = XLSX.utils.table_to_book(table, { sheet: "فاتورة" });
            XLSX.writeFile(wb, "فاتورة.xlsx");
        }
    </script>
</body>
</html>
