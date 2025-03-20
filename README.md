import React, { useState, useEffect } from 'react';
import { Save, Printer, FileSpreadsheet, Upload, Trash2, Plus, Truck, Home, User, Phone, Mail, MapPin } from 'lucide-react';
import _ from 'lodash';

const QuotationForm = () => {
  const [companyInfo, setCompanyInfo] = useState({
    name: 'شركة النقل السريع للأثاث',
    logo: 'شعار الشركة',
    address: 'الرياض - المملكة العربية السعودية',
    phone: '0123456789',
    email: 'info@fastmoving.sa',
    website: 'www.fastmoving.sa'
  });

  const [clientInfo, setClientInfo] = useState({
    name: '',
    address: '',
    phone: '',
    email: '',
    date: new Date().toISOString().split('T')[0],
    quotationNumber: 'QT-' + Math.floor(Math.random() * 10000)
  });

  const [items, setItems] = useState([
    { id: 1, description: 'نقل أثاث منزلي', quantity: 1, price: 1000, total: 1000 },
    { id: 2, description: 'فك وتركيب', quantity: 1, price: 500, total: 500 },
    { id: 3, description: 'تغليف', quantity: 1, price: 300, total: 300 }
  ]);

  const [subtotal, setSubtotal] = useState(0);
  const [tax, setTax] = useState(0);
  const [total, setTotal] = useState(0);

  useEffect(() => {
    calculateTotals();
  }, [items]);

  const calculateTotals = () => {
    const calculatedSubtotal = items.reduce((sum, item) => sum + item.total, 0);
    const calculatedTax = calculatedSubtotal * 0.15;
    const calculatedTotal = calculatedSubtotal + calculatedTax;
    
    setSubtotal(calculatedSubtotal);
    setTax(calculatedTax);
    setTotal(calculatedTotal);
  };

  const handleItemChange = (id, field, value) => {
    setItems(items.map(item => {
      if (item.id === id) {
        const updatedItem = { ...item, [field]: value };
        if (field === 'quantity' || field === 'price') {
          updatedItem.total = updatedItem.quantity * updatedItem.price;
        }
        return updatedItem;
      }
      return item;
    }));
  };

  const addItem = () => {
    const newId = items.length > 0 ? Math.max(...items.map(item => item.id)) + 1 : 1;
    setItems([...items, { id: newId, description: '', quantity: 1, price: 0, total: 0 }]);
  };

  const removeItem = (id) => {
    setItems(items.filter(item => item.id !== id));
  };

  const handleClientInfoChange = (field, value) => {
    setClientInfo({ ...clientInfo, [field]: value });
  };

  const handleCompanyInfoChange = (field, value) => {
    setCompanyInfo({ ...companyInfo, [field]: value });
  };

  const handlePrint = () => {
    window.print();
  };

  const exportToExcel = () => {
    // Prepare data for Excel export
    const excelData = [
      ['معلومات الشركة', '', '', '', ''],
      ['اسم الشركة', companyInfo.name, '', '', ''],
      ['العنوان', companyInfo.address, '', '', ''],
      ['الهاتف', companyInfo.phone, '', '', ''],
      ['البريد الإلكتروني', companyInfo.email, '', '', ''],
      ['الموقع الإلكتروني', companyInfo.website, '', '', ''],
      ['', '', '', '', ''],
      ['معلومات العميل', '', '', '', ''],
      ['اسم العميل', clientInfo.name, '', '', ''],
      ['العنوان', clientInfo.address, '', '', ''],
      ['الهاتف', clientInfo.phone, '', '', ''],
      ['البريد الإلكتروني', clientInfo.email, '', '', ''],
      ['التاريخ', clientInfo.date, '', '', ''],
      ['رقم العرض', clientInfo.quotationNumber, '', '', ''],
      ['', '', '', '', ''],
      ['المنتجات', '', '', '', ''],
      ['الوصف', 'الكمية', 'السعر', 'الإجمالي', ''],
      ...items.map(item => [item.description, item.quantity, item.price, item.total, '']),
      ['', '', '', '', ''],
      ['المجموع الفرعي', '', '', subtotal, ''],
      ['الضريبة (15%)', '', '', tax, ''],
      ['الإجمالي', '', '', total, '']
    ];
    
    // Convert to CSV
    const csvContent = excelData.map(row => row.join(',')).join('\n');
    const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
    const url = URL.createObjectURL(blob);
    
    // Create download link
    const link = document.createElement('a');
    link.href = url;
    link.setAttribute('download', `عرض_سعر_${clientInfo.quotationNumber}.csv`);
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
  };

  const importFromExcel = (event) => {
    const file = event.target.files[0];
    if (!file) return;

    const reader = new FileReader();
    reader.onload = (e) => {
      const content = e.target.result;
      const rows = content.split('\n');
      
      // Parse company info
      if (rows.length > 1) {
        const companyName = rows[1].split(',')[1];
        const companyAddress = rows[2].split(',')[1];
        const companyPhone = rows[3].split(',')[1];
        const companyEmail = rows[4].split(',')[1];
        const companyWebsite = rows[5].split(',')[1];
        
        setCompanyInfo({
          name: companyName || companyInfo.name,
          address: companyAddress || companyInfo.address,
          phone: companyPhone || companyInfo.phone,
          email: companyEmail || companyInfo.email,
          website: companyWebsite || companyInfo.website
        });
      }
      
      // Parse client info
      if (rows.length > 8) {
        const clientName = rows[8].split(',')[1];
        const clientAddress = rows[9].split(',')[1];
        const clientPhone = rows[10].split(',')[1];
        const clientEmail = rows[11].split(',')[1];
        const clientDate = rows[12].split(',')[1];
        const quotationNumber = rows[13].split(',')[1];
        
        setClientInfo({
          name: clientName || clientInfo.name,
          address: clientAddress || clientInfo.address,
          phone: clientPhone || clientInfo.phone,
          email: clientEmail || clientInfo.email,
          date: clientDate || clientInfo.date,
          quotationNumber: quotationNumber || clientInfo.quotationNumber
        });
      }
      
      // Parse items
      if (rows.length > 17) {
        const itemsData = [];
        let i = 17;
        while (i < rows.length && rows[i].trim() !== '') {
          const rowData = rows[i].split(',');
          if (rowData.length >= 4) {
            itemsData.push({
              id: i - 16,
              description: rowData[0],
              quantity: parseFloat(rowData[1]) || 0,
              price: parseFloat(rowData[2]) || 0,
              total: parseFloat(rowData[3]) || 0
            });
          }
          i++;
        }
        
        if (itemsData.length > 0) {
          setItems(itemsData);
        }
      }
    };
    
    reader.readAsText(file);
  };

  return (
    <div className="bg-white p-6 max-w-4xl mx-auto">
      {/* Header with decorative elements */}
      <div className="border-2 border-blue-500 p-6 rounded-lg shadow-lg mb-6 print:shadow-none">
        <div className="flex justify-between items-center">
          <div className="flex items-center">
            <Truck className="w-12 h-12 text-blue-500 mr-2" />
            <div>
              <h1 className="text-2xl font-bold text-blue-700">عرض سعر</h1>
              <p className="text-sm text-gray-600">رقم العرض: {clientInfo.quotationNumber}</p>
            </div>
          </div>
          <div className="flex flex-col items-end">
            <p className="text-sm text-gray-600">التاريخ: {clientInfo.date}</p>
          </div>
        </div>
      </div>

      {/* Controls - Will be hidden during printing */}
      <div className="mb-6 flex justify-between items-center print:hidden">
        <div>
          <button onClick={exportToExcel} className="bg-green-500 text-white px-4 py-2 rounded-lg flex items-center mr-2">
            <FileSpreadsheet className="mr-2" size={16} />
            تصدير إلى Excel
          </button>
        </div>
        <div className="flex">
          <label className="bg-blue-500 text-white px-4 py-2 rounded-lg flex items-center mr-2 cursor-pointer">
            <Upload className="mr-2" size={16} />
            تحميل من Excel
            <input type="file" accept=".csv" onChange={importFromExcel} className="hidden" />
          </label>
          <button onClick={handlePrint} className="bg-purple-500 text-white px-4 py-2 rounded-lg flex items-center">
            <Printer className="mr-2" size={16} />
            طباعة
          </button>
        </div>
      </div>

      {/* Company and Client Information */}
      <div className="flex flex-col md:flex-row gap-6 mb-6">
        {/* Company Information */}
        <div className="flex-1 border-2 border-blue-200 p-4 rounded-lg">
          <div className="flex items-center mb-2">
            <Home className="text-blue-500 mr-2" size={20} />
            <h2 className="text-xl font-bold text-blue-700">معلومات الشركة</h2>
          </div>
          <div className="space-y-2">
            <div className="flex items-center">
              <input
                type="text"
                value={companyInfo.name}
                onChange={(e) => handleCompanyInfoChange('name', e.target.value)}
                className="w-full border border-gray-300 rounded px-2 py-1 print:border-none"
                placeholder="اسم الشركة"
              />
            </div>
            <div className="flex items-center">
              <MapPin className="text-gray-400 mr-2" size={16} />
              <input
                type="text"
                value={companyInfo.address}
                onChange={(e) => handleCompanyInfoChange('address', e.target.value)}
                className="w-full border border-gray-300 rounded px-2 py-1 print:border-none"
                placeholder="العنوان"
              />
            </div>
            <div className="flex items-center">
              <Phone className="text-gray-400 mr-2" size={16} />
              <input
                type="text"
                value={companyInfo.phone}
                onChange={(e) => handleCompanyInfoChange('phone', e.target.value)}
                className="w-full border border-gray-300 rounded px-2 py-1 print:border-none"
                placeholder="الهاتف"
              />
            </div>
            <div className="flex items-center">
              <Mail className="text-gray-400 mr-2" size={16} />
              <input
                type="text"
                value={companyInfo.email}
                onChange={(e) => handleCompanyInfoChange('email', e.target.value)}
                className="w-full border border-gray-300 rounded px-2 py-1 print:border-none"
                placeholder="البريد الإلكتروني"
              />
            </div>
            <div className="flex items-center">
              <input
                type="text"
                value={companyInfo.website}
                onChange={(e) => handleCompanyInfoChange('website', e.target.value)}
                className="w-full border border-gray-300 rounded px-2 py-1 print:border-none"
                placeholder="الموقع الإلكتروني"
              />
            </div>
          </div>
        </div>

        {/* Client Information */}
        <div className="flex-1 border-2 border-blue-200 p-4 rounded-lg">
          <div className="flex items-center mb-2">
            <User className="text-blue-500 mr-2" size={20} />
            <h2 className="text-xl font-bold text-blue-700">معلومات العميل</h2>
          </div>
          <div className="space-y-2">
            <div className="flex items-center">
              <input
                type="text"
                value={clientInfo.name}
                onChange={(e) => handleClientInfoChange('name', e.target.value)}
                className="w-full border border-gray-300 rounded px-2 py-1 print:border-none"
                placeholder="اسم العميل"
              />
            </div>
            <div className="flex items-center">
              <MapPin className="text-gray-400 mr-2" size={16} />
              <input
                type="text"
                value={clientInfo.address}
                onChange={(e) => handleClientInfoChange('address', e.target.value)}
                className="w-full border border-gray-300 rounded px-2 py-1 print:border-none"
                placeholder="العنوان"
              />
            </div>
            <div className="flex items-center">
              <Phone className="text-gray-400 mr-2" size={16} />
              <input
                type="text"
                value={clientInfo.phone}
                onChange={(e) => handleClientInfoChange('phone', e.target.value)}
                className="w-full border border-gray-300 rounded px-2 py-1 print:border-none"
                placeholder="الهاتف"
              />
            </div>
            <div className="flex items-center">
              <Mail className="text-gray-400 mr-2" size={16} />
              <input
                type="text"
                value={clientInfo.email}
                onChange={(e) => handleClientInfoChange('email', e.target.value)}
                className="w-full border border-gray-300 rounded px-2 py-1 print:border-none"
                placeholder="البريد الإلكتروني"
              />
            </div>
            <div className="flex items-center">
              <input
                type="date"
                value={clientInfo.date}
                onChange={(e) => handleClientInfoChange('date', e.target.value)}
                className="w-full border border-gray-300 rounded px-2 py-1 print:border-none"
              />
            </div>
          </div>
        </div>
      </div>

      {/* Items Table */}
      <div className="border-2 border-blue-200 rounded-lg p-4 mb-6">
        <div className="overflow-x-auto">
          <table className="w-full border-collapse">
            <thead>
              <tr className="bg-blue-100">
                <th className="border border-blue-200 py-2 px-4 text-right">الوصف</th>
                <th className="border border-blue-200 py-2 px-4 text-center">الكمية</th>
                <th className="border border-blue-200 py-2 px-4 text-center">السعر (ريال)</th>
                <th className="border border-blue-200 py-2 px-4 text-center">الإجمالي (ريال)</th>
                <th className="border border-blue-200 py-2 px-4 text-center print:hidden">إجراء</th>
              </tr>
            </thead>
            <tbody>
              {items.map((item) => (
                <tr key={item.id}>
                  <td className="border border-blue-200 py-2 px-4">
                    <input
                      type="text"
                      value={item.description}
                      onChange={(e) => handleItemChange(item.id, 'description', e.target.value)}
                      className="w-full border-none focus:outline-none"
                      placeholder="وصف الخدمة"
                    />
                  </td>
                  <td className="border border-blue-200 py-2 px-4 text-center">
                    <input
                      type="number"
                      value={item.quantity}
                      onChange={(e) => handleItemChange(item.id, 'quantity', parseInt(e.target.value) || 0)}
                      className="w-16 border-none text-center focus:outline-none"
                      min="1"
                    />
                  </td>
                  <td className="border border-blue-200 py-2 px-4 text-center">
                    <input
                      type="number"
                      value={item.price}
                      onChange={(e) => handleItemChange(item.id, 'price', parseFloat(e.target.value) || 0)}
                      className="w-24 border-none text-center focus:outline-none"
                      min="0"
                    />
                  </td>
                  <td className="border border-blue-200 py-2 px-4 text-center">
                    {item.total.toFixed(2)}
                  </td>
                  <td className="border border-blue-200 py-2 px-4 text-center print:hidden">
                    <button onClick={() => removeItem(item.id)} className="text-red-500 hover:text-red-700">
                      <Trash2 size={18} />
                    </button>
                  </td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
        
        <div className="mt-4 print:hidden">
          <button onClick={addItem} className="bg-blue-500 text-white px-4 py-2 rounded-lg flex items-center">
            <Plus className="mr-2" size={16} />
            إضافة خدمة
          </button>
        </div>
      </div>

      {/* Totals */}
      <div className="flex justify-end">
        <div className="w-64 border-2 border-blue-200 rounded-lg p-4">
          <div className="flex justify-between mb-2">
            <span className="font-bold">المجموع الفرعي:</span>
            <span>{subtotal.toFixed(2)} ريال</span>
          </div>
          <div className="flex justify-between mb-2">
            <span className="font-bold">الضريبة (15%):</span>
            <span>{tax.toFixed(2)} ريال</span>
          </div>
          <div className="flex justify-between font-bold text-lg text-blue-700">
            <span>الإجمالي:</span>
            <span>{total.toFixed(2)} ريال</span>
          </div>
        </div>
      </div>

      {/* Footer */}
      <div className="mt-6 border-t-2 border-blue-200 pt-4 text-center text-sm text-gray-600">
        <p>شكراً لثقتكم في خدماتنا. هذا العرض صالح لمدة 30 يوماً من تاريخ إصداره.</p>
      </div>

      <style jsx>{`
        @media print {
          @page {
            size: A4;
            margin: 0.5cm;
          }
          body {
            padding: 0;
            margin: 0;
          }
          .print\\:hidden {
            display: none !important;
          }
          .print\\:border-none {
            border: none !important;
          }
          .print\\:shadow-none {
            box-shadow: none !important;
          }
        }
      `}</style>
    </div>
  );
};

export default QuotationForm;
