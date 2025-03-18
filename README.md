<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ZATCA Compliant Invoice System</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            direction: rtl;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid #ccc;
        }

        .tab {
            padding: 10px 20px;
            cursor: pointer;
            background-color: #f1f1f1;
            margin-left: 5px;
        }

        .tab.active {
            background-color: #4CAF50;
            color: white;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        .form-group {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }

        input,
        select,
        textarea {
            width: 100%;
            padding: 8px;
            box-sizing: border-box;
            direction: rtl;
        }

        .form-row {
            display: flex;
            gap: 15px;
            margin-bottom: 15px;
        }

        .form-col {
            flex: 1;
        }

        .item-row {
            display: flex;
            gap: 10px;
            margin-bottom: 10px;
        }

        .item-col {
            flex: 1;
        }

        .item-actions {
            width: 80px;
            text-align: center;
        }

        button {
            padding: 10px 20px;
            cursor: pointer;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 4px;
            font-size: 16px;
            margin-right: 5px;
        }

        button.danger {
            background-color: #f44336;
        }

        button.secondary {
            background-color: #2196F3;
        }

        button:hover {
            opacity: 0.9;
        }

        .invoice-container {
            max-width: 800px;
            margin: 0 auto;
            border: 1px solid #ddd;
            padding: 20px;
            background-color: white;
        }

        .header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            border-bottom: 2px solid #eee;
            padding-bottom: 10px;
        }

        .logo {
            width: 300px;
            height: 250px;
            background-color: white;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .logo img {
            max-width: 100%;
            max-height: 100%;
        }

        .invoice-title {
            text-align: center;
            font-size: 24px;
            margin-bottom: 20px;
        }

        .company-details,
        .customer-details {
            margin-bottom: 20px;
        }

        .details-row {
            display: flex;
            margin-bottom: 10px;
        }

        .details-label {
            width: 150px;
            font-weight: bold;
        }

        .details-value {
            flex-grow: 1;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 20px;
        }

        table,
        th,
        td {
            border: 1px solid #ddd;
        }

        th,
        td {
            padding: 8px;
            text-align: right;
        }

        th {
            background-color: #00cccc;
        }

        .totals {
            margin-left: auto;
            width: 300px;
        }

        .totals-row {
            display: flex;
            justify-content: space-between;
            padding: 5px 0;
            border-bottom: 1px solid #eee;
        }

        .bold {
            font-weight: bold;
        }

        .footer {
    margin-top: 30px;
    text-align: center;
    font-size: 12px;
    color: #666;
    position: relative; /* لتسهيل وضع النص فوقها */
    padding: 20px; /* إضافة حشوة لتوفير مساحة للنص */
}


        .buttons {
            display: flex;
            justify-content: center;
            margin-top: 20px;
            gap: 10px;
        }

        .invoice-notes {
            margin-top: 20px;
            padding: 10px;
            border: 1px dashed #ccc;
        }

        .dual-lang {
            display: flex;
            justify-content: space-between;
        }

        .ar {
            text-align: right;
        }

        .en {
            text-align: left;
            direction: ltr;
        }

        #invoiceList {
            border: 1px solid #ddd;
            margin-bottom: 20px;
        }

        #invoiceList th {
            cursor: pointer;
        }

        .saved-invoice {
            cursor: pointer;
        }

        .saved-invoice:hover {
            background-color: #f5f5f5;
        }

        .company-customer-details {
            display: flex;
            gap: 20px;
            margin-bottom: 20px;
        }

        .company-customer-details > div {
            flex: 1;
                }

        @media print {
            .tabs,
            .buttons,
            .tab-content:not(.active) {
                display: none !important;
            }

            .invoice-container {
                border: none;
            }

            body * {
                visibility: hidden;
            }

            #invoicePreview,
            #invoicePreview * {
                visibility: visible;
            }

            #invoicePreview {
                position: absolute;
                left: 0;
                top: 0;
                width: 100%;
            }

            /* إخفاء الزر والصورة عند الطباعة */
            @media print {
    .upload-image,
    #footerImageUpload {
        display: none !important; /* إخفاء الزر */
    }
    #footerImageContainer {
        display: block !important; /* تأكد من أن الصورة تظهر */
    }
}
    </style>
</head>
<body>
    <div class="container">
        <h1>نظام الفواتير المتوافق مع هيئة الزكاة والضريبة والجمارك</h1>
        <div class="tabs">
            <div class="tab active" data-tab="create">إنشاء فاتورة جديدة</div>
            <div class="tab" data-tab="view">عرض الفواتير السابقة</div>
            <div class="tab" data-tab="settings">إعدادات الشركة</div>
        </div>

        <div class="tab-content active" id="createTab">
            <h2>إنشاء فاتورة جديدة</h2>
            <div class="form-group">
                            </div>
            <div class="form-group">
                <label for="invoiceType">نوع الفاتورة:</label>
                <select id="invoiceType">
                    <option value="standard">فاتورة ضريبية</option>
                    <option value="simplified">فاتورة مبسطة</option>
                    <option value="debit">إشعار مدين</option>
                    <option value="credit">إشعار دائن</option>
                </select>
            </div>
            <div class="form-row">
                <div class="form-col">
                    <div class="form-group">
                        <label for="invoiceNumber">رقم الفاتورة:</label>
                        <input type="text" id="invoiceNumber" value="INV-2023-0001">
                    </div>
                </div>
                <div class="form-col">
                    <div class="form-group">
                        <label for="invoiceDate">تاريخ الفاتورة:</label>
                        <input type="date" id="invoiceDate">
                    </div>
                </div>
                <div class="form-col">
                    <div class="form-group">
                        <label for="supplyDate">تاريخ التوريد:</label>
                        <input type="date" id="supplyDate">
                    </div>
                </div>
            </div>
            <h3>بيانات العميل</h3>
            <div class="form-row">
                <div class="form-col">
                    <div class="form-group">
                        <label for="customerName">اسم العميل:</label>
                        <input type="text" id="customerName" value="شركة العميل النموذجية">
                    </div>
                </div>
                <div class="form-col">
                    <div class="form-group">
                        <label for="customerVatNumber">رقم التسجيل الضريبي للعميل:</label>
                        <input type="text" id="customerVatNumber" value="100000000000003">
                    </div>
                </div>
            </div>
            <div class="form-row">
                <div class="form-col">
                    <div class="form-group">
                        <label for="customerCommercialNumber">رقم السجل التجاري للعميل:</label>
                        <input type="text" id="customerCommercialNumber" value="123456789">
                    </div>
                </div>
                <div class="form-col">
                    <div class="form-group">
                        <label for="customerAddress">عنوان العميل:</label>
                        <textarea id="customerAddress" rows="2">الرياض، المملكة العربية السعودية</textarea>
                    </div>
                </div>
            </div>
            <h3>البنود والخدمات</h3>
            <div id="itemsContainer">
                <div class="item-row" data-item-id="1">
                    <div class="item-col">
                        <input type="text" placeholder="الوصف" value="منتج 1" class="item-desc">
                    </div>
                    <div class="item-col">
                        <input type="number" placeholder="الكمية" value="2" min="1" class="item-quantity">
                    </div>
                    <div class="item-col">
                        <input type="number" placeholder="سعر الوحدة" value="100" step="0.01" class="item-price">
                    </div>
                    <div class="item-col">
                        <select class="item-tax">
                            <option value="15">15% ضريبة القيمة المضافة</option>
                            <option value="0">معفى من الضريبة</option>
                            <option value="5">5% ضريبة مخفضة</option>
                        </select>
                    </div>
                    <div class="item-actions">
                        <button class="danger remove-item">حذف</button>
                    </div>
                </div>
            </div>
            <button id="addItem" class="secondary">إضافة بند جديد</button>
            <div class="form-group">
                <label for="notes">ملاحظات:</label>
                <textarea id="notes" rows="3"></textarea>
            </div>
            <div class="buttons">
                <button id="previewInvoice">معاينة الفاتورة</button>
                <button id="saveInvoice">حفظ الفاتورة</button>
            </div>
        </div>

        <div class="tab-content" id="viewTab">
            <h2>عرض الفواتير السابقة</h2>
            <table id="invoiceList">
                <thead>
                    <tr>
                        <th>رقم الفاتورة</th>
                        <th>تاريخ الفاتورة</th>
                        <th>اسم العميل</th>
                        <th>المبلغ الإجمالي</th>
                        <th>الإجراءات</th>
                    </tr>
                </thead>
                <tbody id="savedInvoicesList">
                </tbody>
            </table>
        </div>

        <div class="tab-content" id="settingsTab">
            <h2>إعدادات الشركة</h2>
            <div class="form-row">
                <div class="form-col">
                    <div class="form-group">
                        <label for="companyName">اسم الشركة:</label>
                        <input type="text" id="companyName" value="شركة نموذجية">
                    </div>
                </div>
                <div class="form-col">
                    <div class="form-group">
                        <label for="companyVatNumber">رقم التسجيل الضريبي:</label>
                        <input type="text" id="companyVatNumber" value="300000000000003">
                    </div>
                </div>
            </div>
            <div class="form-row">
                <div class="form-col">
                    <div class="form-group">
                        <label for="companyCommercialNumber">رقم السجل التجاري:</label>
                        <input type="text" id="companyCommercialNumber" value="987654321">
                    </div>
                </div>
                <div class="form-col">
                    <div class="form-group">
                        <label for="companyAddress">عنوان الشركة:</label>
                        <textarea id="companyAddress" rows="2">الرياض، المملكة العربية السعودية</textarea>
                    </div>
                </div>
            </div>
            <div class="form-group">
                <label for="companyLogo">شعار الشركة:</label>
                <input type="file" id="companyLogo" accept="image/*">
            </div>
            <div class="form-group">
                <label for="invoiceFooter">نص تذييل الفاتورة:</label>
                <textarea id="invoiceFooter" rows="3">هذه الفاتورة صادرة وفقاً لأنظمة هيئة الزكاة والضريبة والجمارك في المملكة العربية السعودية</textarea>
            </div>
            <div class="buttons">
                <button id="saveSettings">حفظ الإعدادات</button>
            </div>
        </div>

        <div id="invoicePreview" style="display: none;">
            <div class="invoice-container">
                <div class="header">
                    <div>
                        <div class="logo" id="previewLogo">
                            <span>شعار الشركة</span>
                        </div>
                    </div>
                    <div>
                        <h2 id="previewCompanyName">شركة نموذجية</h2>
                        <p id="previewCompanyAddress">الرياض، المملكة العربية السعودية</p>
                    </div>
                </div>
                <h1 class="invoice-title ar" id="previewInvoiceTypeAr">فاتورة ضريبية</h1>
                <div class="company-customer-details">
                    <div>
                        <div class="details-row">
                            <div class="details-label">رقم التسجيل الضريبي:</div>
                            <div class="details-value" id="previewCompanyVatNumber">300000000000003</div>
                        </div>
                        <div class="details-row">
                            <div class="details-label">رقم السجل التجاري:</div>
                            <div class="details-value" id="previewCompanyCommercialNumber">987654321</div>
                        </div>
                        <div class="details-row">
                            <div class="details-label">رقم الفاتورة:</div>
                            <div class="details-value" id="previewInvoiceNumber">INV-2023-0001</div>
                        </div>
                        <div class="details-row">
                            <div class="details-label">تاريخ الفاتورة:</div>
                            <div class="details-value" id="previewInvoiceDate">18/03/2025</div>
                        </div>
                        <div class="details-row">
                            <div class="details-label">تاريخ التوريد:</div>
                            <div class="details-value" id="previewSupplyDate">18/03/2025</div>
                        </div>
                    </div>
                    <div>
                        <div class="details-row">
                            <div class="details-label">اسم العميل:</div>
                            <div class="details-value" id="previewCustomerName">شركة العميل النموذجية</div>
                        </div>
                        <div class="details-row">
                            <div class="details-label">رقم التسجيل الضريبي:</div>
                            <div class="details-value" id="previewCustomerVatNumber">100000000000003</div>
                        </div>
                        <div class="details-row">
                            <div class="details-label">رقم السجل التجاري:</div>
                            <div class="details-value" id="previewCustomerCommercialNumber">123456789</div>
                        </div>
                        <div class="details-row">
                            <div class="details-label">العنوان:</div>
                            <div class="details-value" id="previewCustomerAddress">الرياض، المملكة العربية السعودية</div>
                        </div>
                    </div>
                </div>
                <table>
                    <thead>
                        <tr>
                            <th>#</th>
                            <th>الوصف</th>
                            <th>الكمية</th>
                            <th>سعر الوحدة</th>
                            <th>الإجمالي قبل الضريبة</th>
                            <th>قيمة الضريبة</th>
                            <th>الإجمالي شامل الضريبة</th>
                        </tr>
                    </thead>
                    <tbody id="previewItems">
                    </tbody>
                </table>
                <div class="totals">
                    <div class="totals-row">
                        <span>الإجمالي قبل الضريبة:</span>
                        <span id="previewSubtotal">0.00 ريال</span>
                    </div>
                    <div class="totals-row">
                        <span>إجمالي ضريبة القيمة المضافة:</span>
                        <span id="previewVatAmount">0.00 ريال</span>
                    </div>
                    <div class="totals-row bold">
                        <span>الإجمالي النهائي:</span>
                        <span id="previewTotal">0.00</span>
                    </div>
                </div>
                <div class="invoice-notes" id="previewNotes" style="display:none;">
                    <strong>ملاحظات:</strong>
                    <p id="previewNotesText"></p>
                </div>
                <div class="footer">
                    <p id="previewFooter">هذه الفاتورة صادرة وفقاً لأنظمة هيئة الزكاة والضريبة والجمارك في المملكة العربية السعودية</p>
                    <p>شكراً لتعاملكم معنا</p>
                    
                    <!-- زر رفع الصورة -->
                    <div class="upload-image">
                        <label for="footerImageUpload" class="upload-button">رفع صورة</label>
<input type="file" id="footerImageUpload" accept="image/*" style="display: none;">
                    </div>

                    <!-- مكان عرض الصورة -->
                    <div class="footer-image" id="footerImageContainer">
                        <img id="footerImage" src="" alt="Footer Image" style="width: 100%; height: 100px; display: none;">
                    </div>
                </div>
                <div class="buttons">
                    <button id="printBtn">طباعة الفاتورة</button>
                    <button id="backToEdit" class="secondary">العودة للتعديل</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            loadCompanySettings();
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('invoiceDate').value = today;
            document.getElementById('supplyDate').value = today;

            document.querySelectorAll('.tab').forEach(tab => {
                tab.addEventListener('click', function() {
                    document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
                    document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
                    this.classList.add('active');
                    const tabId = this.getAttribute('data-tab') + 'Tab';
                    document.getElementById(tabId).classList.add('active');
                });
            });

            document.getElementById('addItem').addEventListener('click', function() {
                addNewItemRow();
            });

            document.getElementById('itemsContainer').addEventListener('click', function(e) {
                if (e.target.classList.contains('remove-item')) {
                    const itemRow = e.target.closest('.item-row');
                    if (document.querySelectorAll('.item-row').length > 1) {
                        itemRow.remove();
                    } else {
                        itemRow.querySelector('.item-desc').value = '';
                        itemRow.querySelector('.item-quantity').value = '1';
                        itemRow.querySelector('.item-price').value = '0';
                    }
                }
            });

            document.getElementById('previewInvoice').addEventListener('click', function() {
                generateInvoicePreview();
                document.getElementById('createTab').style.display = 'none';
                document.getElementById('invoicePreview').style.display = 'block';
            });

            document.getElementById('backToEdit').addEventListener('click', function() {
                document.getElementById('invoicePreview').style.display = 'none';
                document.getElementById('createTab').style.display = 'block';
            });

            document.getElementById('printBtn').addEventListener('click', function() {
                window.print();
            });

            document.getElementById('saveInvoice').addEventListener('click', function() {
                saveInvoice();
            });

            document.getElementById('saveSettings').addEventListener('click', function() {
                saveCompanySettings();
            });

            document.getElementById('companyLogo').addEventListener('change', handleLogoUpload);
            loadSavedInvoices();
        });

        function addNewItemRow() {
            const container = document.getElementById('itemsContainer');
            const itemCount = container.querySelectorAll('.item-row').length + 1;
            const newRow = document.createElement('div');
            newRow.className = 'item-row';
            newRow.setAttribute('data-item-id', itemCount);
            newRow.innerHTML = `
                <div class="item-col">
                    <input type="text" placeholder="الوصف" class="item-desc">
                </div>
                <div class="item-col">
                    <input type="number" placeholder="الكمية" value="1" min="1" class="item-quantity">
                </div>
                <div class="item-col">
                    <input type="number" placeholder="سعر الوحدة" value="0" step="0.01" class="item-price">
                </div>
                <div class="item-col">
                    <select class="item-tax">
                        <option value="15">15% ضريبة القيمة المضافة</option>
                        <option value="0">معفى من الضريبة</option>
                        <option value="5">5% ضريبة مخفضة</option>
                    </select>
                </div>
                <div class="item-actions">
                    <button class="danger remove-item">حذف</button>
                </div>
            `;
            container.appendChild(newRow);
        }

        function generateInvoicePreview() {
            document.getElementById('previewCompanyName').textContent = document.getElementById('companyName').value;
            document.getElementById('previewCompanyAddress').textContent = document.getElementById('companyAddress').value;
            document.getElementById('previewCompanyVatNumber').textContent = document.getElementById('companyVatNumber').value;
            document.getElementById('previewCompanyCommercialNumber').textContent = document.getElementById('companyCommercialNumber').value;

            const invoiceType = document.getElementById('invoiceType').value;
            let invoiceTypeTextAr = 'فاتورة ضريبية';

            switch(invoiceType) {
                case 'simplified':
                    invoiceTypeTextAr = 'فاتورة مبسطة';
                    break;
                case 'debit':
                    invoiceTypeTextAr = 'إشعار مدين';
                    break;
                case 'credit':
                    invoiceTypeTextAr = 'إشعار دائن';
                    break;
            }

            document.getElementById('previewInvoiceTypeAr').textContent = invoiceTypeTextAr;

            document.getElementById('previewInvoiceNumber').textContent = document.getElementById('invoiceNumber').value;

            const invoiceDate = new Date(document.getElementById('invoiceDate').value);
            document.getElementById('previewInvoiceDate').textContent = formatDate(invoiceDate);

            const supplyDate = new Date(document.getElementById('supplyDate').value);
            document.getElementById('previewSupplyDate').textContent = formatDate(supplyDate);

            document.getElementById('previewCustomerName').textContent = document.getElementById('customerName').value;
            document.getElementById('previewCustomerVatNumber').textContent = document.getElementById('customerVatNumber').value;
            document.getElementById('previewCustomerCommercialNumber').textContent = document.getElementById('customerCommercialNumber').value;
            document.getElementById('previewCustomerAddress').textContent = document.getElementById('customerAddress').value;

            const itemsContainer = document.getElementById('itemsContainer');
            const itemRows = itemsContainer.querySelectorAll('.item-row');
            const previewItems = document.getElementById('previewItems');
            previewItems.innerHTML = '';

            let subtotal = 0;
            let totalVat = 0;

            itemRows.forEach((row, index) => {
                const description = row.querySelector('.item-desc').value;
                const quantity = parseFloat(row.querySelector('.item-quantity').value);
                const unitPrice = parseFloat(row.querySelector('.item-price').value);
                const taxRate = parseFloat(row.querySelector('.item-tax').value);

                const lineTotal = quantity * unitPrice;
                const lineTax = lineTotal * (taxRate / 100);
                const lineTotalWithTax = lineTotal + lineTax;

                subtotal += lineTotal;
                totalVat += lineTax;

                const newRow = document.createElement('tr');
                newRow.innerHTML = `
                    <td>${index + 1}</td>
                    <td>${description}</td>
                    <td>${quantity}</td>
                    <td>${formatCurrency(unitPrice)}</td>
                    <td>${formatCurrency(lineTotal)}</td>
                    <td>${formatCurrency(lineTax)} (${taxRate}%)</td>
                    <td>${formatCurrency(lineTotalWithTax)}</td>
                `;
                previewItems.appendChild(newRow);
            });

            const total = subtotal + totalVat;
            document.getElementById('previewSubtotal').textContent = formatCurrency(subtotal);
            document.getElementById('previewVatAmount').textContent = formatCurrency(totalVat);
            document.getElementById('previewTotal').textContent = formatCurrency(total);

            const notes = document.getElementById('notes').value;
            if (notes.trim()) {
                document.getElementById('previewNotes').style.display = 'block';
                document.getElementById('previewNotesText').textContent = notes;
            } else {
                document.getElementById('previewNotes').style.display = 'none';
            }

            document.getElementById('previewFooter').textContent = document.getElementById('invoiceFooter').value;
        }

        function formatDate(date) {
            return `${date.getDate().toString().padStart(2, '0')}/${(date.getMonth() + 1).toString().padStart(2, '0')}/${date.getFullYear()}`;
        }

        function formatCurrency(amount) {
            return amount.toFixed(2) + ' ريال';
        }

        function saveInvoice() {
            const invoiceData = {
                invoiceNumber: document.getElementById('invoiceNumber').value,
                invoiceDate: document.getElementById('invoiceDate').value,
                supplyDate: document.getElementById('supplyDate').value,
                customerName: document.getElementById('customerName').value,
                customerVatNumber: document.getElementById('customerVatNumber').value,
                customerCommercialNumber: document.getElementById('customerCommercialNumber').value,
                customerAddress: document.getElementById('customerAddress').value,
                items: [],
                notes: document.getElementById('notes').value,
                subtotal: parseFloat(document.getElementById('previewSubtotal').textContent.replace(/[^0-9.]/g, '')),
                vatAmount: parseFloat(document.getElementById('previewVatAmount').textContent.replace(/[^0-9.]/g, '')),
                total: parseFloat(document.getElementById('previewTotal').textContent.replace(/[^0-9.]/g, ''))
            };

            const itemRows = document.querySelectorAll('.item-row');
            itemRows.forEach(row => {
                const item = {
                    description: row.querySelector('.item-desc').value,
                    quantity: parseFloat(row.querySelector('.item-quantity').value),
                    unitPrice: parseFloat(row.querySelector('.item-price').value),
                    taxRate: parseFloat(row.querySelector('.item-tax').value)
                };
                invoiceData.items.push(item);
            });

            let savedInvoices = JSON.parse(localStorage.getItem('savedInvoices')) || [];
            savedInvoices.push(invoiceData);
            localStorage.setItem('savedInvoices', JSON.stringify(savedInvoices));

            alert('تم حفظ الفاتورة بنجاح!');
            loadSavedInvoices();
        }

        function loadSavedInvoices() {
            const savedInvoices = JSON.parse(localStorage.getItem('savedInvoices')) || [];
            const savedInvoicesList = document.getElementById('savedInvoicesList');
            savedInvoicesList.innerHTML = '';

            savedInvoices.forEach((invoice, index) => {
                const row = document.createElement('tr');
                row.className = 'saved-invoice';
                row.setAttribute('data-index', index);
                row.innerHTML = `
                    <td>${invoice.invoiceNumber}</td>
                    <td>${invoice.invoiceDate}</td>
                    <td>${invoice.customerName}</td>
                    <td>${formatCurrency(invoice.total)}</td>
                    <td>
                        <button onclick="viewSavedInvoice(${index})">عرض</button>
                        <button onclick="deleteSavedInvoice(${index})" class="danger">حذف</button>
                    </td>
                `;
                savedInvoicesList.appendChild(row);
            });
        }

        function viewSavedInvoice(index) {
            const savedInvoices = JSON.parse(localStorage.getItem('savedInvoices')) || [];
            const invoice = savedInvoices[index];

            document.getElementById('invoiceNumber').value = invoice.invoiceNumber;
            document.getElementById('invoiceDate').value = invoice.invoiceDate;
            document.getElementById('supplyDate').value = invoice.supplyDate;
            document.getElementById('customerName').value = invoice.customerName;
            document.getElementById('customerVatNumber').value = invoice.customerVatNumber;
            document.getElementById('customerCommercialNumber').value = invoice.customerCommercialNumber;
            document.getElementById('customerAddress').value = invoice.customerAddress;
            document.getElementById('notes').value = invoice.notes;

            const itemsContainer = document.getElementById('itemsContainer');
            itemsContainer.innerHTML = '';

            invoice.items.forEach(item => {
                addNewItemRow();
                const lastRow = itemsContainer.lastElementChild;
                lastRow.querySelector('.item-desc').value = item.description;
                lastRow.querySelector('.item-quantity').value = item.quantity;
                lastRow.querySelector('.item-price').value = item.unitPrice;
                lastRow.querySelector('.item-tax').value = item.taxRate;
            });

            document.querySelector('.tab.active').classList.remove('active');
            document.querySelector('.tab-content.active').classList.remove('active');
            document.querySelector('[data-tab="create"]').classList.add('active');
            document.getElementById('createTab').classList.add('active');

            alert('تم تحميل الفاتورة للعرض والتعديل');
        }

        function deleteSavedInvoice(index) {
            if (confirm('هل أنت متأكد من حذف هذه الفاتورة؟')) {
                let savedInvoices = JSON.parse(localStorage.getItem('savedInvoices')) || [];
                savedInvoices.splice(index, 1);
                localStorage.setItem('savedInvoices', JSON.stringify(savedInvoices));
                loadSavedInvoices();
            }
        }

        function loadCompanySettings() {
            const companySettings = JSON.parse(localStorage.getItem('companySettings')) || {};
            if (companySettings.companyName) {
                document.getElementById('companyName').value = companySettings.companyName;
                document.getElementById('companyVatNumber').value = companySettings.companyVatNumber;
                document.getElementById('companyCommercialNumber').value = companySettings.companyCommercialNumber;
                document.getElementById('companyAddress').value = companySettings.companyAddress;
                document.getElementById('invoiceFooter').value = companySettings.invoiceFooter;

                if (companySettings.companyLogo) {
                    document.getElementById('previewLogo').innerHTML = `<img src="${companySettings.companyLogo}" alt="Company Logo">`;
                }
            }
        }

        function saveCompanySettings() {
            const companySettings = {
                companyName: document.getElementById('companyName').value,
                companyVatNumber: document.getElementById('companyVatNumber').value,
                companyCommercialNumber: document.getElementById('companyCommercialNumber').value,
                companyAddress: document.getElementById('companyAddress').value,
                invoiceFooter: document.getElementById('invoiceFooter').value,
                companyLogo: document.getElementById('previewLogo').querySelector('img')?.src || ''
            };

            localStorage.setItem('companySettings', JSON.stringify(companySettings));
            alert('تم حفظ إعدادات الشركة بنجاح!');
        }

        function handleLogoUpload(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    document.getElementById('previewLogo').innerHTML = `<img src="${e.target.result}" alt="Company Logo">`;
                    const companySettings = JSON.parse(localStorage.getItem('companySettings')) || {};
                    companySettings.companyLogo = e.target.result;
                    localStorage.setItem('companySettings', JSON.stringify(companySettings));
                };
                reader.readAsDataURL(file);
            }
        }

        // حدث لرفع الصورة وعرضها
        document.getElementById('footerImageUpload').addEventListener('change', function(event) {
    const file = event.target.files[0];
    if (file) {
        const reader = new FileReader();
        reader.onload = function(e) {
            // تعيين الخلفية
            document.querySelector('.footer').style.backgroundImage = `url(${e.target.result})`;
            document.querySelector('.footer').style.backgroundSize = 'cover';
            document.querySelector('.footer').style.backgroundPosition = 'center';
            document.getElementById('footerImageContainer').style.display = 'none'; // إخفاء العنصر
        };
        reader.readAsDataURL(file);
    }
});

    </script>
</body>
</html>
