<!doctype html>
<html lang="zh-TW">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TePe醫師群組訂單表單</title>
  <script src="/_sdk/data_sdk.js"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      box-sizing: border-box;
      font-family: 'Noto Sans TC', 'Microsoft JhengHei', sans-serif;
      background: linear-gradient(135deg, #e8f7f9 0%, #f0f9ff 100%);
      width: 100%;
      height: 100%;
      overflow-y: auto;
    }

    html, body {
      height: 100%;
    }

    .form-container {
      width: 100%;
      min-height: 100%;
      padding: 20px;
      display: flex;
      justify-content: center;
      align-items: flex-start;
    }

    .form-wrapper {
      width: 100%;
      max-width: 800px;
      background: white;
      border-radius: 16px;
      box-shadow: 0 8px 32px rgba(0, 94, 164, 0.12);
      overflow: hidden;
      margin: 20px 0;
    }

    .form-header {
      background: linear-gradient(135deg, #8aced6 0%, #6ab8c4 100%);
      padding: 30px 20px;
      text-align: center;
      color: white;
    }

    .logo-container {
      margin-bottom: 20px;
      min-height: 60px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .logo-container img {
      max-width: 200px;
      max-height: 80px;
      width: auto;
      height: auto;
      object-fit: contain;
    }

    .form-header h1 {
      font-size: 28px;
      font-weight: 700;
      margin-bottom: 8px;
      text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }

    .form-header p {
      font-size: 14px;
      opacity: 0.95;
    }

    .form-body {
      padding: 30px 20px;
    }

    .section {
      margin-bottom: 30px;
    }

    .section-title {
      color: #005ea4;
      font-size: 20px;
      font-weight: 700;
      margin-bottom: 20px;
      padding-bottom: 10px;
      border-bottom: 3px solid #8aced6;
    }

    .form-group {
      margin-bottom: 20px;
    }

    .form-label {
      display: block;
      color: #005ea4;
      font-weight: 600;
      margin-bottom: 8px;
      font-size: 15px;
    }

    .required {
      color: #e74c3c;
      margin-left: 4px;
    }

    .form-input,
    .form-select,
    .form-textarea {
      width: 100%;
      padding: 12px 16px;
      border: 2px solid #e0e0e0;
      border-radius: 8px;
      font-size: 15px;
      font-family: inherit;
      transition: all 0.3s ease;
      background: white;
    }

    .form-input:focus,
    .form-select:focus,
    .form-textarea:focus {
      outline: none;
      border-color: #8aced6;
      box-shadow: 0 0 0 3px rgba(138, 206, 214, 0.15);
    }

    .form-textarea {
      resize: vertical;
      min-height: 100px;
    }

    .radio-group {
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .radio-option {
      display: flex;
      align-items: center;
      padding: 12px;
      border: 2px solid #e0e0e0;
      border-radius: 8px;
      cursor: pointer;
      transition: all 0.3s ease;
      background: white;
    }

    .radio-option:hover {
      border-color: #8aced6;
      background: #f8fdfe;
    }

    .radio-option input[type="radio"] {
      margin-right: 12px;
      width: 20px;
      height: 20px;
      cursor: pointer;
      accent-color: #8aced6;
    }

    .radio-option label {
      cursor: pointer;
      flex: 1;
      font-size: 15px;
      color: #005ea4;
    }

    .info-box {
      background: #e8f7f9;
      border-left: 4px solid #8aced6;
      padding: 16px;
      margin-top: 12px;
      border-radius: 4px;
      display: none;
    }

    .info-box.show {
      display: block;
    }

    .info-box p {
      color: #005ea4;
      font-size: 14px;
      line-height: 1.6;
      margin-bottom: 8px;
    }

    .info-box p:last-child {
      margin-bottom: 0;
    }

    .address-row {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
    }

    .product-item {
      background: white;
      border: 2px solid #e0e0e0;
      border-radius: 12px;
      padding: 0;
      margin-bottom: 20px;
      overflow: hidden;
      transition: all 0.3s ease;
    }

    .product-item:hover {
      box-shadow: 0 4px 12px rgba(138, 206, 214, 0.2);
    }

    .product-checkbox-container {
      padding: 20px;
    }

    .product-checkbox-header {
      display: flex;
      align-items: center;
      gap: 12px;
      margin-bottom: 16px;
      cursor: pointer;
      user-select: none;
    }

    .product-checkbox {
      width: 24px;
      height: 24px;
      cursor: pointer;
      accent-color: #8aced6;
      flex-shrink: 0;
    }

    .product-checkbox-label {
      color: #005ea4;
      font-weight: 700;
      font-size: 14px;
      cursor: pointer;
      flex: 1;
    }

    .product-gallery {
      position: relative;
      width: 100%;
      height: 280px;
      background: #f5f5f5;
      margin-bottom: 16px;
      border-radius: 8px;
      overflow: hidden;
    }

    .product-gallery-main {
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;
    }

    .product-gallery-image {
      max-width: 100%;
      max-height: 100%;
      object-fit: contain;
      cursor: pointer;
      transition: transform 0.3s ease;
    }

    .product-gallery-image:hover {
      transform: scale(1.05);
    }

    .product-gallery-placeholder {
      color: #999;
      font-size: 14px;
      text-align: center;
    }

    .product-gallery-nav {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      background: rgba(255, 255, 255, 0.9);
      border: none;
      width: 40px;
      height: 40px;
      border-radius: 50%;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #005ea4;
      font-size: 20px;
      font-weight: 700;
      transition: all 0.3s ease;
      z-index: 10;
    }

    .product-gallery-nav:hover {
      background: white;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
    }

    .product-gallery-nav.prev {
      left: 10px;
    }

    .product-gallery-nav.next {
      right: 10px;
    }

    .product-gallery-nav:disabled {
      opacity: 0.3;
      cursor: not-allowed;
    }

    .product-gallery-indicators {
      position: absolute;
      bottom: 10px;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      gap: 6px;
    }

    .gallery-indicator {
      width: 8px;
      height: 8px;
      border-radius: 50%;
      background: rgba(255, 255, 255, 0.5);
      border: 1px solid rgba(0, 94, 164, 0.3);
      transition: all 0.3s ease;
    }

    .gallery-indicator.active {
      background: white;
      border-color: #005ea4;
      width: 24px;
      border-radius: 4px;
    }

    .product-name {
      color: #005ea4;
      font-weight: 700;
      font-size: 18px;
      margin-bottom: 8px;
    }

    .product-subtitle {
      color: #666;
      font-size: 14px;
      margin-bottom: 12px;
      line-height: 1.5;
    }

    .product-price {
      color: #8aced6;
      font-weight: 700;
      font-size: 20px;
      margin-bottom: 16px;
    }

    .product-details {
      display: none;
      border-top: 2px solid #e0f4f7;
      padding: 20px;
      background: #f8fdfe;
    }

    .product-details.show {
      display: block;
    }

    .product-category-title {
      color: #005ea4;
      font-weight: 700;
      font-size: 16px;
      margin-bottom: 16px;
      padding-bottom: 8px;
      border-bottom: 2px solid #8aced6;
    }

    .product-options {
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .option-item {
      display: grid;
      grid-template-columns: 1fr 120px;
      gap: 12px;
      align-items: center;
      padding: 12px;
      background: white;
      border: 2px solid #e0e0e0;
      border-radius: 8px;
      transition: all 0.3s ease;
    }

    .option-item:hover {
      border-color: #8aced6;
      background: #f8fdfe;
    }

    .option-label {
      color: #005ea4;
      font-size: 14px;
      font-weight: 500;
    }

    .quantity-wrapper {
      display: flex;
      flex-direction: column;
      gap: 4px;
      width: 120px;
    }

    .quantity-label {
      color: #005ea4;
      font-size: 12px;
      font-weight: 600;
      text-align: left;
    }

    .quantity-input {
      width: 100%;
      padding: 8px;
      border: 2px solid #e0e0e0;
      border-radius: 6px;
      font-size: 14px;
      text-align: center;
      transition: all 0.3s ease;
    }

    .quantity-input:focus {
      border-color: #8aced6;
      outline: none;
    }

    .image-modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.9);
      z-index: 1000;
      align-items: center;
      justify-content: center;
    }

    .image-modal.show {
      display: flex;
    }

    .image-modal-content {
      max-width: 90%;
      max-height: 90%;
      object-fit: contain;
    }

    .image-modal-close {
      position: absolute;
      top: 20px;
      right: 30px;
      color: white;
      font-size: 40px;
      font-weight: 700;
      cursor: pointer;
      background: none;
      border: none;
      transition: all 0.3s ease;
    }

    .image-modal-close:hover {
      color: #8aced6;
      transform: scale(1.1);
    }

    .order-summary {
      background: linear-gradient(135deg, #e8f7f9 0%, #d4f1f6 100%);
      border-radius: 12px;
      padding: 24px;
      border: 2px solid #8aced6;
    }

    .summary-title {
      color: #005ea4;
      font-size: 20px;
      font-weight: 700;
      margin-bottom: 16px;
      text-align: center;
    }

    .summary-row {
      display: flex;
      justify-content: space-between;
      padding: 10px 0;
      color: #005ea4;
      font-size: 15px;
    }

    .summary-row.total {
      border-top: 2px solid #8aced6;
      margin-top: 12px;
      padding-top: 16px;
      font-size: 20px;
      font-weight: 700;
    }

    .summary-row.discount {
      color: #e74c3c;
      font-weight: 600;
    }

    .gift-section {
      background: #fff9e6;
      border: 2px solid #ffd700;
      border-radius: 12px;
      padding: 20px;
      margin-top: 20px;
      display: none;
    }

    .gift-section.show {
      display: block;
    }

    .gift-title {
      color: #d4a520;
      font-size: 18px;
      font-weight: 700;
      margin-bottom: 12px;
      text-align: center;
    }

    .gift-description {
      text-align: center;
      color: #d4a520;
      margin-bottom: 12px;
    }

    .gift-image {
      width: 100%;
      max-width: 300px;
      height: auto;
      border-radius: 8px;
      margin: 12px auto;
      display: block;
    }

    .submit-button {
      width: 100%;
      padding: 16px;
      background: linear-gradient(135deg, #8aced6 0%, #6ab8c4 100%);
      color: white;
      border: none;
      border-radius: 12px;
      font-size: 18px;
      font-weight: 700;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: 0 4px 12px rgba(138, 206, 214, 0.4);
      margin-top: 30px;
    }

    .submit-button:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 20px rgba(138, 206, 214, 0.5);
    }

    .submit-button:active {
      transform: translateY(0);
    }

    .submit-button:disabled {
      background: #cccccc;
      cursor: not-allowed;
      transform: none;
      box-shadow: none;
    }

    .thankyou-page {
      display: none;
      width: 100%;
      height: 100%;
      background: white;
    }

    .thankyou-page.show {
      display: block;
    }

    .thankyou-content {
      display: grid;
      grid-template-columns: 1fr 2fr;
      height: 100%;
      min-height: 500px;
    }

    .thankyou-text {
      background: linear-gradient(135deg, #8aced6 0%, #6ab8c4 100%);
      padding: 40px 30px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      color: white;
    }

    .thankyou-text h2 {
      font-size: 28px;
      margin-bottom: 20px;
      font-weight: 700;
    }

    .thankyou-text p {
      font-size: 16px;
      line-height: 1.8;
      margin-bottom: 12px;
    }

    .thankyou-bank-info {
      background: rgba(255, 255, 255, 0.15);
      padding: 20px;
      border-radius: 8px;
      margin-top: 20px;
      backdrop-filter: blur(10px);
    }

    .thankyou-bank-info p {
      margin-bottom: 8px;
      font-size: 15px;
    }

    .thankyou-bank-info p:last-child {
      margin-bottom: 0;
    }

    .thankyou-bank-info strong {
      font-weight: 700;
    }

    .thankyou-image {
      background: #f5f5f5;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
    }

    .thankyou-image img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .thankyou-image-placeholder {
      color: #ccc;
      font-size: 18px;
      text-align: center;
    }

    .loading-spinner {
      display: none;
      text-align: center;
      padding: 20px;
    }

    .loading-spinner.show {
      display: block;
    }

    .spinner {
      border: 4px solid #e0f4f7;
      border-top: 4px solid #8aced6;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      animation: spin 1s linear infinite;
      margin: 0 auto;
    }

    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    @media (max-width: 768px) {
      .form-container {
        padding: 10px;
      }

      .form-wrapper {
        margin: 10px 0;
      }

      .form-header {
        padding: 20px 15px;
      }

      .form-header h1 {
        font-size: 24px;
      }

      .form-body {
        padding: 20px 15px;
      }

      .address-row {
        grid-template-columns: 1fr;
      }

      .product-item {
        padding: 0;
      }

      .product-checkbox-container {
        padding: 15px;
      }

      .product-gallery {
        height: 220px;
      }

      .option-item {
        grid-template-columns: 1fr;
        gap: 8px;
      }

      .quantity-wrapper {
        width: 100%;
      }

      .thankyou-content {
        grid-template-columns: 1fr;
      }

      .thankyou-text {
        padding: 30px 20px;
      }

      .thankyou-text h2 {
        font-size: 24px;
      }

      .thankyou-image {
        min-height: 300px;
      }
    }

    @media (max-width: 480px) {
      .form-header h1 {
        font-size: 20px;
      }

      .section-title {
        font-size: 18px;
      }

      .product-name {
        font-size: 16px;
      }

      .product-price {
        font-size: 18px;
      }

      .thankyou-text h2 {
        font-size: 20px;
      }

      .thankyou-text p {
        font-size: 14px;
      }
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
  <script src="https://cdn.tailwindcss.com" type="text/javascript"></script>
 </head>
 <body>
  <div class="form-container">
   <div class="form-wrapper">
    <div class="form-header">
     <div class="logo-container"><img src="https://i.meee.com.tw/4Ojn0aJ.png" alt="TePe Logo" onerror="this.style.display='none';">
     </div>
     <h1 id="formTitle">TePe醫師群組訂單表單</h1>
     <p id="formSubtitle">本月優惠：卡裝與牙刷買1-2盒享9折、3-4盒享7折、5盒以上享6折｜袋裝買2-4袋享9折、6-8袋享7折、10袋以上享6折｜【袋裝與卡裝可合併計算折扣：2包袋裝=1盒】</p>
    </div>
    <div class="form-body">
     <form id="orderForm">
      <div class="section">
       <h2 class="section-title" id="sectionProductTitle">本月優惠產品</h2>
       <div id="productsContainer"></div>
      </div>
      <div class="section">
       <div class="order-summary">
        <h3 class="summary-title">訂單摘要</h3>
        <div id="orderDetails" style="display: none; margin-bottom: 20px; padding-bottom: 20px; border-bottom: 2px solid #8aced6;">
         <h4 style="color: #005ea4; font-size: 16px; font-weight: 700; margin-bottom: 12px;">訂單明細</h4>
         <div id="orderDetailsList" style="display: flex; flex-direction: column; gap: 12px;"></div>
        </div>
        <div id="bagValidationWarning" style="display: none; background: #fff3cd; border: 2px solid #ffc107; color: #856404; padding: 16px; border-radius: 8px; margin-bottom: 20px; text-align: center; font-weight: 600;">
         ⚠️ 注意：【袋裝】產品的總數量必須為2的倍數才能提交訂單！
        </div>
        <div class="summary-row"><span>總盒數：</span> <span id="totalBoxes">0</span>
        </div>
        <div class="summary-row"><span>商品小計：</span> <span id="subtotal">NT$ 0</span>
        </div>
        <div class="summary-row discount"><span id="discountLabel">折扣：</span> <span id="discount">NT$ 0</span>
        </div>
        <div class="summary-row"><span>運費：</span> <span id="shipping">NT$ 0</span>
        </div>
        <div class="summary-row total"><span>總金額：</span> <span id="finalTotal">NT$ 0</span>
        </div>
       </div>
       <div class="gift-section" id="gift3Box">
        <h3 class="gift-title" id="gift3BoxTitle">🎁 贈品選擇</h3>
        <p class="gift-description" id="gift3BoxDescription">只要買滿任意3盒或以上的產品即會送出【治療椅專用展示架】，並且會送展示用的牙刷與牙間刷</p><img src="https://i.meee.com.tw/kUKVJE7.png" class="gift-image" alt="治療椅專用展示架" onerror="this.style.display='none';">
        <div class="form-group"><label class="form-label" id="gift3BoxQuestion">請問您是否會想要這項贈品？<span class="required">*</span></label>
         <div class="radio-group">
          <div class="radio-option"><input type="radio" id="gift3Yes" name="gift3Box" value="是"> <label for="gift3Yes">是</label>
          </div>
          <div class="radio-option"><input type="radio" id="gift3No" name="gift3Box" value="否"> <label for="gift3No">否</label>
          </div>
         </div>
        </div>
       </div>
       <div class="gift-section" id="gift5Box">
        <h3 class="gift-title" id="gift5BoxTitle">🎁 加碼贈品</h3>
        <p class="gift-description" id="gift5BoxDescription">只要買滿任意5盒或以上的產品即會再加送【磁吸階梯式展示架】，並且會送展示用的牙刷與牙間刷</p><img src="https://i.meee.com.tw/XkBN407.png" class="gift-image" alt="磁吸階梯式展示架" onerror="this.style.display='none';">
        <div class="form-group"><label class="form-label" id="gift5BoxQuestion">請問您是否會想要這項贈品？<span class="required">*</span></label>
         <div class="radio-group">
          <div class="radio-option"><input type="radio" id="gift5Yes" name="gift5Box" value="是"> <label for="gift5Yes">是</label>
          </div>
          <div class="radio-option"><input type="radio" id="gift5No" name="gift5Box" value="否"> <label for="gift5No">否</label>
          </div>
         </div>
        </div>
       </div>
      </div>
      <div class="section">
       <h2 class="section-title" id="sectionPaymentTitle">付款與配送方式</h2>
       <div class="form-group"><label class="form-label" id="paymentLabel">請問您是希望先匯款後發貨，還是您的寄送地址於雙北地區，並希望我們送貨到府收款呢？<span class="required">*</span></label>
        <div class="radio-group">
         <div class="radio-option"><input type="radio" id="payment1" name="paymentMethod" value="先匯款後發貨" required> <label for="payment1" id="paymentOption1">先匯款後發貨<span style="color: #e74c3c; font-weight: 700; display: block; margin-top: 4px;">（若選擇此付款方式將會再加贈I型牙間刷（超軟刷毛）綜合8支袋裝）</span></label>
         </div>
         <div class="radio-option"><input type="radio" id="payment2" name="paymentMethod" value="我的地址在雙北地區，並希望貨到付款"> <label for="payment2" id="paymentOption2">我的地址在雙北地區，並希望貨到付款</label>
         </div>
        </div>
        <div class="info-box" id="bankInfoBox">
         <p><strong id="bankInfoTitle">匯款帳戶資訊：</strong></p>
         <p id="bankAccountName">戶名：香港商豐達牙材有限公司台灣分公司</p>
         <p id="bankName">銀行名稱：匯豐銀行台北分行 081</p>
         <p id="bankAccountNumber">帳號：001-591031-031（共12碼）</p>
        </div>
       </div>
      </div>
      <div class="section">
       <h2 class="section-title" id="sectionInvoiceTitle">發票資訊</h2>
       <div class="form-group"><label class="form-label">發票種類<span class="required">*</span></label>
        <div class="radio-group">
         <div class="radio-option"><input type="radio" id="invoice1" name="invoiceType" value="發票二聯" required> <label for="invoice1">發票二聯</label>
         </div>
         <div class="radio-option"><input type="radio" id="invoice2" name="invoiceType" value="發票三聯（需打統編）"> <label for="invoice2">發票三聯（需打統編）</label>
         </div>
        </div>
       </div>
       <div id="invoiceDetailsSection" style="display: none;">
        <div class="form-group"><label class="form-label" for="invoiceTitle">三聯發票抬頭<span class="required">*</span></label> <input type="text" id="invoiceTitle" class="form-input" placeholder="請輸入發票抬頭">
        </div>
        <div class="form-group"><label class="form-label" for="invoiceTaxId">三聯發票統編<span class="required">*</span></label> <input type="text" id="invoiceTaxId" class="form-input" placeholder="請輸入統一編號">
        </div>
       </div>
      </div>
      <div class="section">
       <h2 class="section-title" id="sectionBasicTitle">基本資料</h2>
       <div class="form-group"><label class="form-label" for="doctorName">醫師姓名<span class="required">*</span></label> <input type="text" id="doctorName" class="form-input" placeholder="請輸入醫師姓名" required>
       </div>
       <div class="form-group"><label class="form-label" for="phone">聯絡電話<span class="required">*</span></label> <input type="tel" id="phone" class="form-input" placeholder="請輸入聯絡電話" required>
       </div>
       <div class="form-group"><label class="form-label" for="email">電子郵件<span class="required">*</span></label> <input type="email" id="email" class="form-input" placeholder="請輸入電子郵件" required>
       </div>
       <div class="form-group"><label class="form-label" for="clinicName">醫療院所名稱<span class="required">*</span></label> <input type="text" id="clinicName" class="form-input" placeholder="請輸入醫療院所名稱" required>
       </div>
       <div class="form-group"><label class="form-label">寄送地址<span class="required">*</span></label>
        <div class="address-row"><select id="city" class="form-select" required> <option value="">請選擇縣市</option> </select> <select id="district" class="form-select" required disabled> <option value="">請選擇區域</option> </select>
        </div><input type="text" id="address" class="form-input" placeholder="請輸入詳細地址" required style="margin-top: 12px;">
       </div>
      </div>
      <div class="section">
       <div class="form-group"><label class="form-label" for="notes">備註（選填）</label> <textarea id="notes" class="form-textarea" placeholder="如有其他需求請於此說明..."></textarea>
       </div>
      </div><button type="submit" class="submit-button" id="submitButton">提交訂單</button>
      <div class="loading-spinner" id="loadingSpinner">
       <div class="spinner"></div>
       <p style="margin-top: 12px; color: #005ea4;">正在提交訂單與發送郵件...</p>
      </div>
     </form>
     <div class="thankyou-page" id="thankyouPage">
      <div class="thankyou-content">
       <div class="thankyou-text" id="thankyouText"></div>
       <div class="thankyou-image"><img src="https://i.meee.com.tw/rNHhP4i.png" alt="感謝您的購買" onerror="this.parentElement.innerHTML='<div class=\'thankyou-image-placeholder\'>感謝您的購買</div>';">
       </div>
      </div>
     </div>
    </div>
   </div>
  </div>
  <div class="image-modal" id="imageModal"><button class="image-modal-close" id="modalClose" type="button">×</button> <img class="image-modal-content" id="modalImage" alt="產品圖片">
  </div>
  <script>
    emailjs.init('WT2UlkdZDl6FkW5pb');

    const products = [
      {
        id: 'product1',
        name: '(牙刷)至尊雙層刷毛牙刷',
        subtitle: '最低購買數量為1盒14支',
        price: 1960,
        unit: '盒',
        categoryTitle: '刷頭大小',
        images: [
          'https://i.meee.com.tw/GSxGWjd.png',
          'https://i.meee.com.tw/1PyRwDm.png',
          'https://i.meee.com.tw/vjPDWtQ.png',
          'https://i.meee.com.tw/Qu9sHY0.png'
        ],
        options: [
          { label: '至尊雙層刷毛牙刷' },
          { label: '迷你至尊雙層刷毛牙刷' }
        ]
      },
      {
        id: 'product2',
        name: '【卡裝】I型牙間刷(一般刷毛)',
        subtitle: '最低購買數量為1盒10卡 (一卡內含6支)',
        price: 1780,
        unit: '盒',
        categoryTitle: '尺寸',
        images: [
          'https://i.meee.com.tw/VlWlOXy.jpg',
          'https://i.meee.com.tw/DIEMgls.png',
          'https://i.meee.com.tw/VgRxWsb.png',
          'https://i.meee.com.tw/ASLeogA.png',
          'https://i.meee.com.tw/jIO73WG.png'
        ],
        options: [
          { label: '0號│0.4mm│SSSS│粉紅色' },
          { label: '1號│0.45mm│SSS│橘色' },
          { label: '2號│0.5mm│SS│紅色' },
          { label: '3號│0.6mm│S│藍色' },
          { label: '4號│0.7mm│M│黃色' },
          { label: '5號│0.8mm│L│綠色' },
          { label: '6號│1.1mm│紫色' },
          { label: '7號│1.4mm│灰色' },
          { label: '8號│1.5mm│黑色' },
          { label: '0-5號│0.4-0.8mm│綜合卡裝' }
        ]
      },
      {
        id: 'product3',
        name: '【袋裝】I型牙間刷(一般刷毛)',
        subtitle: '最低購買數量為1包 (一包內含25支，每支皆附上保護蓋)',
        price: 715,
        unit: '包',
        categoryTitle: '尺寸',
        images: [
          'https://i.meee.com.tw/eHcqxqs.jpg',
          'https://i.meee.com.tw/8UfZtfh.png',
          'https://i.meee.com.tw/CnUGgrW.png',
          'https://i.meee.com.tw/VgRxWsb.png',
          'https://i.meee.com.tw/ASLeogA.png',
          'https://i.meee.com.tw/jIO73WG.png'
        ],
        options: [
          { label: '0號│0.4mm│SSSS│粉紅色' },
          { label: '1號│0.45mm│SSS│橘色' },
          { label: '2號│0.5mm│SS│紅色' },
          { label: '3號│0.6mm│S│藍色' },
          { label: '4號│0.7mm│M│黃色' },
          { label: '5號│0.8mm│L│綠色' },
          { label: '6號│1.1mm│紫色' },
          { label: '7號│1.4mm│灰色' },
          { label: '8號│1.5mm│黑色' }
        ]
      },
      {
        id: 'product4',
        name: '【卡裝】I型牙間刷(超軟刷毛)',
        subtitle: '最低購買數量為1盒10卡 (一卡內含6支)',
        price: 1780,
        unit: '盒',
        categoryTitle: '尺寸',
        images: [
          'https://i.meee.com.tw/XYjCtqV.jpg',
          'https://i.meee.com.tw/9pM9GJX.png',
          'https://i.meee.com.tw/eJYmjvb.png',
          'https://i.meee.com.tw/rgGnXmK.png',
          'https://i.meee.com.tw/VgRxWsb.png',
          'https://i.meee.com.tw/ASLeogA.png',
          'https://i.meee.com.tw/jIO73WG.png'
        ],
        options: [
          { label: '1號│0.45mm│SSS│橘色' },
          { label: '2號│0.5mm│SS│紅色' },
          { label: '3號│0.6mm│S│藍色' },
          { label: '4號│0.7mm│M│黃色' },
          { label: '5號│0.8mm│L│綠色' },
          { label: '6號│1.1mm│紫色' },
          { label: '1-6號│0.45-1.1mm│綜合卡裝' }
        ]
      },
      {
        id: 'product5',
        name: '【袋裝】I型牙間刷(超軟刷毛)',
        subtitle: '最低購買數量為1包 (一包內含25支，每支皆附上保護蓋)',
        price: 715,
        unit: '包',
        categoryTitle: '尺寸',
        images: [
          'https://i.meee.com.tw/JMJrNBN.jpg',
          'https://i.meee.com.tw/EwKjvM5.png',
          'https://i.meee.com.tw/eJYmjvb.png',
          'https://i.meee.com.tw/rgGnXmK.png',
          'https://i.meee.com.tw/VgRxWsb.png',
          'https://i.meee.com.tw/ASLeogA.png',
          'https://i.meee.com.tw/jIO73WG.png'
        ],
        options: [
          { label: '1號│0.45mm│SSS│橘色' },
          { label: '2號│0.5mm│SS│紅色' },
          { label: '3號│0.6mm│S│藍色' },
          { label: '4號│0.7mm│M│黃色' },
          { label: '5號│0.8mm│L│綠色' },
          { label: '6號│1.1mm│紫色' }
        ]
      },
      {
        id: 'product6',
        name: '【卡裝】L型牙間刷',
        subtitle: '最低購買數量為1盒10卡 (一卡內含6支)',
        price: 1780,
        unit: '盒',
        categoryTitle: '尺寸',
        images: [
          'https://i.meee.com.tw/rCyJFTu.jpg',
          'https://i.meee.com.tw/LRdHbQS.png',
          'https://i.meee.com.tw/iISzmbI.png',
          'https://i.meee.com.tw/VgRxWsb.png',
          'https://i.meee.com.tw/ASLeogA.png',
          'https://i.meee.com.tw/jIO73WG.png'
        ],
        options: [
          { label: '0號│0.4mm│SSSS│粉紅色' },
          { label: '1號│0.45mm│SSS│橘色' },
          { label: '2號│0.5mm│SS│紅色' },
          { label: '3號│0.6mm│S│藍色' },
          { label: '4號│0.7mm│M│黃色' },
          { label: '5號│0.8mm│L│綠色' },
          { label: '0-5號│0.4-0.8mm│綜合卡裝' }
        ]
      },
      {
        id: 'product7',
        name: '【袋裝】L型牙間刷',
        subtitle: '最低購買數量為1包 (一包內含25支，每支皆附上保護蓋)',
        price: 715,
        unit: '包',
        categoryTitle: '尺寸',
        images: [
          'https://i.meee.com.tw/ycY1Rza.jpg',
          'https://i.meee.com.tw/CG36pfd.png',
          'https://i.meee.com.tw/iISzmbI.png',
          'https://i.meee.com.tw/VgRxWsb.png',
          'https://i.meee.com.tw/ASLeogA.png',
          'https://i.meee.com.tw/jIO73WG.png'
        ],
        options: [
          { label: '0號│0.4mm│SSSS│粉紅色' },
          { label: '1號│0.45mm│SSS│橘色' },
          { label: '2號│0.5mm│SS│紅色' },
          { label: '3號│0.6mm│S│藍色' },
          { label: '4號│0.7mm│M│黃色' },
          { label: '5號│0.8mm│L│綠色' }
        ]
      }
    ];

    const galleryState = {};

    const taiwanRegions = {
      '台北市': ['中正區', '大同區', '中山區', '松山區', '大安區', '萬華區', '信義區', '士林區', '北投區', '內湖區', '南港區', '文山區'],
      '新北市': ['板橋區', '三重區', '中和區', '永和區', '新莊區', '新店區', '樹林區', '鶯歌區', '三峽區', '淡水區', '汐止區', '瑞芳區', '土城區', '蘆洲區', '五股區', '泰山區', '林口區', '深坑區', '石碇區', '坪林區', '三芝區', '石門區', '八里區', '平溪區', '雙溪區', '貢寮區', '金山區', '萬里區', '烏來區'],
      '桃園市': ['桃園區', '中壢區', '平鎮區', '八德區', '楊梅區', '蘆竹區', '大溪區', '龍潭區', '龜山區', '大園區', '觀音區', '新屋區', '復興區'],
      '台中市': ['中區', '東區', '南區', '西區', '北區', '西屯區', '南屯區', '北屯區', '豐原區', '東勢區', '大甲區', '清水區', '沙鹿區', '梧棲區', '后里區', '神岡區', '潭子區', '大雅區', '新社區', '石岡區', '外埔區', '大安區', '烏日區', '大肚區', '龍井區', '霧峰區', '太平區', '大里區', '和平區'],
      '台南市': ['中西區', '東區', '南區', '北區', '安平區', '安南區', '永康區', '歸仁區', '新化區', '左鎮區', '玉井區', '楠西區', '南化區', '仁德區', '關廟區', '龍崎區', '官田區', '麻豆區', '佳里區', '西港區', '七股區', '將軍區', '學甲區', '北門區', '新營區', '後壁區', '白河區', '東山區', '六甲區', '下營區', '柳營區', '鹽水區', '善化區', '大內區', '山上區', '新市區', '安定區'],
      '高雄市': ['楠梓區', '左營區', '鼓山區', '三民區', '鹽埕區', '前金區', '新興區', '苓雅區', '前鎮區', '旗津區', '小港區', '鳳山區', '大寮區', '鳥松區', '林園區', '仁武區', '大樹區', '大社區', '岡山區', '路竹區', '橋頭區', '梓官區', '彌陀區', '永安區', '燕巢區', '田寮區', '阿蓮區', '茄萣區', '湖內區', '旗山區', '美濃區', '內門區', '杉林區', '甲仙區', '六龜區', '茂林區', '桃源區', '那瑪夏區'],
      '基隆市': ['中正區', '七堵區', '暖暖區', '仁愛區', '中山區', '安樂區', '信義區'],
      '新竹市': ['東區', '北區', '香山區'],
      '新竹縣': ['竹北市', '竹東鎮', '新埔鎮', '關西鎮', '湖口鄉', '新豐鄉', '峨眉鄉', '寶山鄉', '北埔鄉', '芎林鄉', '橫山鄉', '尖石鄉', '五峰鄉'],
      '苗栗縣': ['苗栗市', '頭份市', '竹南鎮', '後龍鎮', '通霄鎮', '苑裡鎮', '卓蘭鎮', '造橋鄉', '西湖鄉', '頭屋鄉', '公館鄉', '銅鑼鄉', '三義鄉', '大湖鄉', '獅潭鄉', '三灣鄉', '南庄鄉', '泰安鄉'],
      '彰化縣': ['彰化市', '員林市', '和美鎮', '鹿港鎮', '溪湖鎮', '二林鎮', '田中鎮', '北斗鎮', '花壇鄉', '芬園鄉', '大村鄉', '永靖鄉', '伸港鄉', '線西鄉', '福興鄉', '秀水鄉', '埔心鄉', '埔鹽鄉', '大城鄉', '芳苑鄉', '竹塘鄉', '社頭鄉', '二水鄉', '田尾鄉', '埤頭鄉', '溪州鄉'],
      '南投縣': ['南投市', '埔里鎮', '草屯鎮', '竹山鎮', '集集鎮', '名間鄉', '鹿谷鄉', '中寮鄉', '魚池鄉', '國姓鄉', '水里鄉', '信義鄉', '仁愛鄉'],
      '雲林縣': ['斗六市', '斗南鎮', '虎尾鎮', '西螺鎮', '土庫鎮', '北港鎮', '莿桐鄉', '林內鄉', '古坑鄉', '大埤鄉', '崙背鄉', '二崙鄉', '麥寮鄉', '台西鄉', '東勢鄉', '褒忠鄉', '四湖鄉', '口湖鄉', '水林鄉', '元長鄉'],
      '嘉義市': ['東區', '西區'],
      '嘉義縣': ['太保市', '朴子市', '布袋鎮', '大林鎮', '民雄鄉', '溪口鄉', '新港鄉', '六腳鄉', '東石鄉', '義竹鄉', '鹿草鄉', '水上鄉', '中埔鄉', '竹崎鄉', '梅山鄉', '番路鄉', '大埔鄉', '阿里山鄉'],
      '屏東縣': ['屏東市', '潮州鎮', '東港鎮', '恆春鎮', '萬丹鄉', '長治鄉', '麟洛鄉', '九如鄉', '里港鄉', '鹽埔鄉', '高樹鄉', '萬巒鄉', '內埔鄉', '竹田鄉', '新埤鄉', '枋寮鄉', '新園鄉', '崁頂鄉', '林邊鄉', '南州鄉', '佳冬鄉', '琉球鄉', '車城鄉', '滿州鄉', '枋山鄉', '霧台鄉', '瑪家鄉', '泰武鄉', '來義鄉', '春日鄉', '獅子鄉', '牡丹鄉', '三地門鄉'],
      '宜蘭縣': ['宜蘭市', '羅東鎮', '蘇澳鎮', '頭城鎮', '礁溪鄉', '壯圍鄉', '員山鄉', '冬山鄉', '五結鄉', '三星鄉', '大同鄉', '南澳鄉'],
      '花蓮縣': ['花蓮市', '鳳林鎮', '玉里鎮', '新城鄉', '吉安鄉', '壽豐鄉', '光復鄉', '豐濱鄉', '瑞穗鄉', '富里鄉', '秀林鄉', '萬榮鄉', '卓溪鄉'],
      '台東縣': ['台東市', '成功鎮', '關山鎮', '卑南鄉', '鹿野鄉', '池上鄉', '東河鄉', '長濱鄉', '太麻里鄉', '大武鄉', '綠島鄉', '海端鄉', '延平鄉', '金峰鄉', '達仁鄉', '蘭嶼鄉'],
      '澎湖縣': ['馬公市', '湖西鄉', '白沙鄉', '西嶼鄉', '望安鄉', '七美鄉'],
      '金門縣': ['金城鎮', '金湖鎮', '金沙鎮', '金寧鄉', '烈嶼鄉', '烏坵鄉'],
      '連江縣': ['南竿鄉', '北竿鄉', '莒光鄉', '東引鄉']
    };

    const defaultConfig = {
      form_title: 'TePe醫師群組訂單表單',
      form_subtitle: '本月優惠：卡裝與牙刷買1-2盒享9折、3-4盒享7折、5盒以上享6折｜袋裝買2-4袋享9折、6-8袋享7折、10袋以上享6折｜【袋裝與卡裝可合併計算折扣：2包袋裝=1盒】'
    };

    function updateGallery(productId) {
      const state = galleryState[productId];
      if (!state || state.images.length === 0) return;

      const img = document.getElementById(`gallery-img-${productId}`);
      const prevBtn = document.getElementById(`gallery-prev-${productId}`);
      const nextBtn = document.getElementById(`gallery-next-${productId}`);
      const indicators = document.querySelectorAll(`.gallery-indicator-${productId}`);

      img.src = state.images[state.currentIndex];
      
      prevBtn.disabled = state.currentIndex === 0;
      nextBtn.disabled = state.currentIndex === state.images.length - 1;

      indicators.forEach((ind, idx) => {
        if (idx === state.currentIndex) {
          ind.classList.add('active');
        } else {
          ind.classList.remove('active');
        }
      });
    }

    function navigateGallery(productId, direction, event) {
      if (event) {
        event.preventDefault();
        event.stopPropagation();
      }
      
      const state = galleryState[productId];
      if (!state) return;

      state.currentIndex += direction;
      if (state.currentIndex < 0) state.currentIndex = 0;
      if (state.currentIndex >= state.images.length) state.currentIndex = state.images.length - 1;

      updateGallery(productId);
    }

    function openImageModal(src, event) {
      if (event) {
        event.preventDefault();
        event.stopPropagation();
      }
      const modal = document.getElementById('imageModal');
      const modalImg = document.getElementById('modalImage');
      modal.classList.add('show');
      modalImg.src = src;
    }

    function initProducts() {
      const container = document.getElementById('productsContainer');
      container.innerHTML = '';

      products.forEach((product) => {
        galleryState[product.id] = {
          images: product.images,
          currentIndex: 0
        };

        const productDiv = document.createElement('div');
        productDiv.className = 'product-item';
        
        let galleryHTML = '<div class="product-gallery"><div class="product-gallery-main">';
        
        if (product.images.length > 0) {
          galleryHTML += `
            <button type="button" class="product-gallery-nav prev" id="gallery-prev-${product.id}">‹</button>
            <img src="${product.images[0]}" alt="${product.name}" class="product-gallery-image" id="gallery-img-${product.id}" onerror="this.src=''; this.alt='圖片載入失敗';">
            <button type="button" class="product-gallery-nav next" id="gallery-next-${product.id}">›</button>
          `;
          
          if (product.images.length > 1) {
            galleryHTML += '<div class="product-gallery-indicators">';
            product.images.forEach((_, idx) => {
              galleryHTML += `<div class="gallery-indicator gallery-indicator-${product.id}${idx === 0 ? ' active' : ''}"></div>`;
            });
            galleryHTML += '</div>';
          }
        } else {
          galleryHTML += '<div class="product-gallery-placeholder">尚無產品照片</div>';
        }
        
        galleryHTML += '</div></div>';

        productDiv.innerHTML = `
          <div class="product-checkbox-container">
            <div class="product-checkbox-header" id="header-${product.id}">
              <input type="checkbox" class="product-checkbox" id="checkbox-${product.id}">
              <label class="product-checkbox-label" for="checkbox-${product.id}">選擇此產品</label>
            </div>
            ${galleryHTML}
            <div class="product-name" style="cursor: pointer;" data-product-id="${product.id}">${product.name}</div>
            <div class="product-subtitle" style="cursor: pointer;" data-product-id="${product.id}">${product.subtitle}</div>
            <div class="product-price" style="cursor: pointer;" data-product-id="${product.id}">NT$ ${product.price.toLocaleString()}/${product.unit}</div>
          </div>
          <div class="product-details" id="details-${product.id}">
            <div class="product-category-title">${product.categoryTitle}</div>
            <div class="product-options" id="options-${product.id}"></div>
          </div>
        `;
        container.appendChild(productDiv);

        const optionsDiv = document.getElementById(`options-${product.id}`);
        product.options.forEach((option, optionIndex) => {
          const optionDiv = document.createElement('div');
          optionDiv.className = 'option-item';
          
          optionDiv.innerHTML = `
            <span class="option-label">${option.label}</span>
            <div class="quantity-wrapper">
              <span class="quantity-label">數量</span>
              <input type="number" 
                     class="quantity-input" 
                     id="${product.id}-${optionIndex}" 
                     min="0" 
                     value="0" 
                     data-product-id="${product.id}"
                     data-price="${product.price}">
            </div>
          `;
          optionsDiv.appendChild(optionDiv);
        });

        const checkbox = document.getElementById(`checkbox-${product.id}`);
        checkbox.addEventListener('change', function() {
          toggleProductDetails(product.id);
        });

        const header = document.getElementById(`header-${product.id}`);
        header.addEventListener('click', function(e) {
          if (e.target !== checkbox) {
            e.preventDefault();
            checkbox.checked = !checkbox.checked;
            toggleProductDetails(product.id);
          }
        });

        const clickableElements = productDiv.querySelectorAll('[data-product-id]');
        clickableElements.forEach(element => {
          element.addEventListener('click', function(e) {
            e.preventDefault();
            const checkbox = document.getElementById(`checkbox-${product.id}`);
            if (!checkbox.checked) {
              checkbox.checked = true;
              toggleProductDetails(product.id);
            }
          });
        });

        const prevBtn = document.getElementById(`gallery-prev-${product.id}`);
        const nextBtn = document.getElementById(`gallery-next-${product.id}`);
        
        if (prevBtn) {
          prevBtn.addEventListener('click', function(e) {
            navigateGallery(product.id, -1, e);
          });
        }
        
        if (nextBtn) {
          nextBtn.addEventListener('click', function(e) {
            navigateGallery(product.id, 1, e);
          });
        }

        const img = document.getElementById(`gallery-img-${product.id}`);
        if (img) {
          img.addEventListener('click', function(e) {
            openImageModal(this.src, e);
          });
        }

        if (product.images.length > 0) {
          updateGallery(product.id);
        }
      });

      document.querySelectorAll('.quantity-input').forEach(input => {
        input.addEventListener('input', calculateTotal);
      });
    }

    function toggleProductDetails(productId) {
      const checkbox = document.getElementById(`checkbox-${productId}`);
      const details = document.getElementById(`details-${productId}`);
      
      if (checkbox.checked) {
        details.classList.add('show');
      } else {
        details.classList.remove('show');
        document.querySelectorAll(`input[data-product-id="${productId}"]`).forEach(input => {
          input.value = 0;
        });
        calculateTotal();
      }
    }

    function initRegionSelectors() {
      const citySelect = document.getElementById('city');
      const districtSelect = document.getElementById('district');

      Object.keys(taiwanRegions).forEach(city => {
        const option = document.createElement('option');
        option.value = city;
        option.textContent = city;
        citySelect.appendChild(option);
      });

      citySelect.addEventListener('change', function() {
        districtSelect.innerHTML = '<option value="">請選擇區域</option>';
        districtSelect.disabled = false;

        if (this.value && taiwanRegions[this.value]) {
          taiwanRegions[this.value].forEach(district => {
            const option = document.createElement('option');
            option.value = district;
            option.textContent = district;
            districtSelect.appendChild(option);
          });
        } else {
          districtSelect.disabled = true;
        }
      });
    }

    function calculateTotal() {
      let boxProducts = 0;
      let bagProducts = 0;
      let totalSubtotal = 0;
      const selectedItems = [];

      const bagProductIds = ['product3', 'product5', 'product7'];

      document.querySelectorAll('.quantity-input').forEach(input => {
        const quantity = parseInt(input.value) || 0;
        if (quantity > 0) {
          const price = parseInt(input.dataset.price);
          const productId = input.dataset.productId;
          const product = products.find(p => p.id === productId);
          const optionIndex = input.id.split('-')[1];
          const option = product.options[optionIndex];
          
          if (bagProductIds.includes(productId)) {
            bagProducts += quantity;
          } else {
            boxProducts += quantity;
          }
          
          totalSubtotal += quantity * price;
          
          selectedItems.push({
            productName: product.name,
            optionLabel: option.label,
            quantity: quantity,
            price: price,
            subtotal: quantity * price
          });
        }
      });

      const bagValidationWarning = document.getElementById('bagValidationWarning');
      const isBagValid = bagProducts === 0 || bagProducts % 2 === 0;
      
      if (!isBagValid) {
        bagValidationWarning.style.display = 'block';
      } else {
        bagValidationWarning.style.display = 'none';
      }

      const orderDetails = document.getElementById('orderDetails');
      const orderDetailsList = document.getElementById('orderDetailsList');
      
      if (selectedItems.length > 0) {
        orderDetails.style.display = 'block';
        orderDetailsList.innerHTML = selectedItems.map(item => `
          <div style="background: white; padding: 12px; border-radius: 8px; border: 1px solid #e0e0e0;">
            <div style="color: #005ea4; font-weight: 600; margin-bottom: 4px;">${item.productName}</div>
            <div style="color: #666; font-size: 14px; margin-bottom: 4px;">${item.optionLabel}</div>
            <div style="display: flex; justify-content: space-between; color: #005ea4; font-size: 14px;">
              <span>數量：${item.quantity}</span>
              <span>NT$ ${item.subtotal.toLocaleString()}</span>
            </div>
          </div>
        `).join('');
      } else {
        orderDetails.style.display = 'none';
      }

      const bagEquivalentBoxes = Math.floor(bagProducts / 2);
      const totalEquivalentBoxes = boxProducts + bagEquivalentBoxes;

      let discountRate = 0;
      let discountLabel = '';
      if (totalEquivalentBoxes >= 5) {
        discountRate = 0.6;
        discountLabel = '合併折扣（6折）：';
      } else if (totalEquivalentBoxes >= 3) {
        discountRate = 0.7;
        discountLabel = '合併折扣（7折）：';
      } else if (totalEquivalentBoxes >= 1) {
        discountRate = 0.9;
        discountLabel = '合併折扣（9折）：';
      } else {
        discountLabel = '折扣：';
      }

      const discountedSubtotal = totalSubtotal * discountRate;
      const discountAmount = totalSubtotal - discountedSubtotal;

      let shipping = 0;
      if (discountedSubtotal > 0 && discountedSubtotal < 3000) {
        shipping = 120;
      }

      const finalTotal = discountedSubtotal + shipping;

      let totalBoxesDisplay = '';
      if (bagProducts > 0 && boxProducts > 0) {
        totalBoxesDisplay = `${bagProducts}包袋裝 + ${boxProducts}盒卡裝/牙刷 = ${totalEquivalentBoxes}盒`;
      } else if (bagProducts > 0) {
        totalBoxesDisplay = `${bagProducts}包袋裝 = ${bagEquivalentBoxes}盒`;
      } else {
        totalBoxesDisplay = `${boxProducts}盒`;
      }

      document.getElementById('totalBoxes').textContent = totalBoxesDisplay;
      document.getElementById('subtotal').textContent = `NT$ ${totalSubtotal.toLocaleString()}`;
      document.getElementById('discountLabel').textContent = discountLabel;
      document.getElementById('discount').textContent = discountAmount > 0 ? `-NT$ ${Math.round(discountAmount).toLocaleString()}` : 'NT$ 0';
      document.getElementById('shipping').textContent = `NT$ ${shipping}`;
      
      const finalTotalRow = document.querySelector('.summary-row.total');
      if (isBagValid) {
        finalTotalRow.style.display = 'flex';
        document.getElementById('finalTotal').textContent = `NT$ ${Math.round(finalTotal).toLocaleString()}`;
      } else {
        finalTotalRow.style.display = 'none';
      }

      const gift3Box = document.getElementById('gift3Box');
      const gift5Box = document.getElementById('gift5Box');
      
      if (totalEquivalentBoxes >= 3) {
        gift3Box.classList.add('show');
        document.querySelectorAll('input[name="gift3Box"]').forEach(input => {
          input.required = true;
        });
      } else {
        gift3Box.classList.remove('show');
        document.querySelectorAll('input[name="gift3Box"]').forEach(input => {
          input.required = false;
          input.checked = false;
        });
      }

      if (totalEquivalentBoxes >= 5) {
        gift5Box.classList.add('show');
        document.querySelectorAll('input[name="gift5Box"]').forEach(input => {
          input.required = true;
        });
      } else {
        gift5Box.classList.remove('show');
        document.querySelectorAll('input[name="gift5Box"]').forEach(input => {
          input.required = false;
          input.checked = false;
        });
      }
    }

    document.querySelectorAll('input[name="paymentMethod"]').forEach(radio => {
      radio.addEventListener('change', function() {
        const bankInfoBox = document.getElementById('bankInfoBox');
        if (this.value === '先匯款後發貨') {
          bankInfoBox.classList.add('show');
        } else {
          bankInfoBox.classList.remove('show');
        }
      });
    });

    document.querySelectorAll('input[name="invoiceType"]').forEach(radio => {
      radio.addEventListener('change', function() {
        const invoiceDetailsSection = document.getElementById('invoiceDetailsSection');
        const invoiceTitle = document.getElementById('invoiceTitle');
        const invoiceTaxId = document.getElementById('invoiceTaxId');
        
        if (this.value === '發票三聯（需打統編）') {
          invoiceDetailsSection.style.display = 'block';
          invoiceTitle.required = true;
          invoiceTaxId.required = true;
        } else {
          invoiceDetailsSection.style.display = 'none';
          invoiceTitle.required = false;
          invoiceTaxId.required = false;
        }
      });
    });

    document.getElementById('modalClose').addEventListener('click', function() {
      document.getElementById('imageModal').classList.remove('show');
    });

    document.getElementById('imageModal').addEventListener('click', function(e) {
      if (e.target === this) {
        this.classList.remove('show');
      }
    });

    let orderData = [];

    const dataHandler = {
      onDataChanged(data) {
        orderData = data;
      }
    };

    async function sendOrderEmail(formData, selectedProducts) {
      let productDetailsText = '';
      selectedProducts.forEach(item => {
        productDetailsText += `${item.name} - ${item.option}\n數量：${item.quantity} × NT$ ${item.price} = NT$ ${item.subtotal}\n\n`;
      });

      let boxInfoText = '';
      if (formData.bagProductsCount > 0) {
        boxInfoText += `袋裝總數：${formData.bagProductsCount} 包\n`;
      }
      if (formData.boxProductsCount > 0) {
        boxInfoText += `卡裝/牙刷總數：${formData.boxProductsCount} 盒\n`;
      }
      boxInfoText += `合併計算總盒數：${formData.totalEquivalentBoxes} 盒（2包袋裝=1盒）`;

      let invoiceDetailsText = '';
      if (formData.invoiceTitle) {
        invoiceDetailsText = `發票抬頭：${formData.invoiceTitle}\n統一編號：${formData.invoiceTaxId}`;
      }

      let giftInfoText = '';
      if (formData.totalEquivalentBoxes >= 3) {
        giftInfoText += `治療椅專用展示架：${formData.displayRack3Box}\n`;
      }
      if (formData.totalEquivalentBoxes >= 5) {
        giftInfoText += `磁吸階梯式展示架：${formData.displayRack5Box}`;
      }
      if (!giftInfoText) {
        giftInfoText = '無贈品';
      }

      let notesText = formData.notes ? `\n\n=== 備註 ===\n${formData.notes}` : '';

      const templateParams = {
        orderNumber: formData.orderNumber,
        submittedAt: new Date(formData.submittedAt).toLocaleString('zh-TW'),
        doctorName: formData.doctorName,
        phone: formData.phone,
        email: formData.email,
        clinicName: formData.clinicName,
        paymentMethod: formData.paymentMethod,
        fullAddress: `${formData.city}${formData.district}${formData.address}`,
        invoiceType: formData.invoiceType,
        invoiceDetails: invoiceDetailsText,
        productDetails: productDetailsText,
        boxInfo: boxInfoText,
        subtotal: formData.subtotal.toLocaleString(),
        discount: Math.round(formData.discount).toLocaleString(),
        shipping: formData.shipping,
        finalTotal: Math.round(formData.finalTotal).toLocaleString(),
        giftInfo: giftInfoText,
        notes: notesText
      };

      try {
        await emailjs.send(
          'service_TePeLINEDentist',
          'TePeLINEDentist',
          {
            ...templateParams,
            to_email: formData.email,
            to_name: formData.doctorName
          }
        );

        return { success: true };
      } catch (error) {
        console.error('郵件發送失敗:', error);
        return { success: false, error: error };
      }
    }

    function showThankYouPage(paymentMethod) {
      const config = window.elementSdk?.config || defaultConfig;
      const thankyouPage = document.getElementById('thankyouPage');
      const thankyouText = document.getElementById('thankyouText');
      
      document.getElementById('orderForm').style.display = 'none';
      thankyouPage.classList.add('show');
      
      if (paymentMethod === '先匯款後發貨') {
        thankyouText.innerHTML = `
          <h2>感謝您的購買與支持！</h2>
          <p>再麻煩您幫忙匯款到以下帳戶，待確認匯款完後即會立刻出貨：</p>
          <div class="thankyou-bank-info">
            <p><strong>匯款帳戶資訊：</strong></p>
            <p>戶名：香港商豐達牙材有限公司台灣分公司</p>
            <p>銀行名稱：匯豐銀行台北分行 081</p>
            <p>帳號：001-591031-031（共12碼）</p>
          </div>
          <p style="margin-top: 20px;">✅ 訂單確認郵件已發送至您的信箱</p>
        `;
      } else {
        thankyouText.innerHTML = `
          <h2>感謝您的購買！</h2>
          <p>我們將於確認收款後立即出貨，感謝您對TePe的支持！</p>
          <p style="margin-top: 20px;">✅ 訂單確認郵件已發送至您的信箱</p>
        `;
      }
    }

    document.getElementById('orderForm').addEventListener('submit', async function(e) {
      e.preventDefault();

      let hasProducts = false;
      const selectedProducts = [];
      let boxProducts = 0;
      let bagProducts = 0;
      const bagProductIds = ['product3', 'product5', 'product7'];
      
      document.querySelectorAll('.quantity-input').forEach(input => {
        const quantity = parseInt(input.value) || 0;
        if (quantity > 0) {
          hasProducts = true;
          const productId = input.dataset.productId;
          const product = products.find(p => p.id === productId);
          const optionIndex = input.id.split('-')[1];
          
          if (bagProductIds.includes(productId)) {
            bagProducts += quantity;
          } else {
            boxProducts += quantity;
          }
          
          selectedProducts.push({
            name: product.name,
            option: product.options[optionIndex].label,
            quantity: quantity,
            price: product.price,
            subtotal: quantity * product.price
          });
        }
      });

      if (!hasProducts) {
        const errorDiv = document.createElement('div');
        errorDiv.style.cssText = 'background: #f8d7da; border: 2px solid #f5c6cb; color: #721c24; padding: 16px; border-radius: 8px; margin-top: 16px; text-align: center;';
        errorDiv.textContent = '請至少選擇一項產品並輸入數量';
        const submitBtn = document.getElementById('submitButton');
        if (!document.querySelector('.error-message')) {
          submitBtn.parentNode.insertBefore(errorDiv, submitBtn);
          errorDiv.className = 'error-message';
          setTimeout(() => errorDiv.remove(), 3000);
        }
        return;
      }

      if (bagProducts > 0 && bagProducts % 2 !== 0) {
        const errorDiv = document.createElement('div');
        errorDiv.style.cssText = 'background: #fff3cd; border: 2px solid #ffc107; color: #856404; padding: 16px; border-radius: 8px; margin-top: 16px; text-align: center; font-weight: 600;';
        errorDiv.textContent = '⚠️ 【袋裝】產品的總數量必須為2的倍數才能提交訂單！目前袋裝總數：' + bagProducts;
        const submitBtn = document.getElementById('submitButton');
        const existingError = document.querySelector('.bag-error-message');
        if (existingError) {
          existingError.remove();
        }
        submitBtn.parentNode.insertBefore(errorDiv, submitBtn);
        errorDiv.className = 'bag-error-message';
        setTimeout(() => errorDiv.remove(), 5000);
        return;
      }

      const bagEquivalentBoxes = Math.floor(bagProducts / 2);
      const totalEquivalentBoxes = boxProducts + bagEquivalentBoxes;
      
      const subtotalText = document.getElementById('subtotal').textContent.replace('NT$ ', '').replace(',', '');
      const discountText = document.getElementById('discount').textContent.replace('-NT$ ', '').replace('NT$ ', '').replace(',', '');
      const shippingText = document.getElementById('shipping').textContent.replace('NT$ ', '');
      const finalTotalText = document.getElementById('finalTotal').textContent.replace('NT$ ', '').replace(',', '');

      const formData = {
        orderNumber: 'TP' + Date.now(),
        paymentMethod: document.querySelector('input[name="paymentMethod"]:checked').value,
        doctorName: document.getElementById('doctorName').value,
        phone: document.getElementById('phone').value,
        email: document.getElementById('email').value,
        clinicName: document.getElementById('clinicName').value,
        city: document.getElementById('city').value,
        district: document.getElementById('district').value,
        address: document.getElementById('address').value,
        invoiceType: document.querySelector('input[name="invoiceType"]:checked').value,
        invoiceTitle: document.getElementById('invoiceTitle').value || '',
        invoiceTaxId: document.getElementById('invoiceTaxId').value || '',
        products: JSON.stringify(selectedProducts),
        bagProductsCount: bagProducts,
        boxProductsCount: boxProducts,
        totalEquivalentBoxes: totalEquivalentBoxes,
        subtotal: parseFloat(subtotalText),
        discount: parseFloat(discountText || 0),
        shipping: parseFloat(shippingText),
        finalTotal: parseFloat(finalTotalText),
        displayRack3Box: totalEquivalentBoxes >= 3 ? (document.querySelector('input[name="gift3Box"]:checked')?.value || '否') : '不適用',
        displayRack5Box: totalEquivalentBoxes >= 5 ? (document.querySelector('input[name="gift5Box"]:checked')?.value || '否') : '不適用',
        notes: document.getElementById('notes').value || '',
        submittedAt: new Date().toISOString()
      };

      document.getElementById('submitButton').disabled = true;
      document.getElementById('loadingSpinner').classList.add('show');

      try {
        if (orderData.length >= 999) {
          const limitDiv = document.createElement('div');
          limitDiv.style.cssText = 'background: #fff3cd; border: 2px solid #ffc107; color: #856404; padding: 16px; border-radius: 8px; margin-top: 16px; text-align: center;';
          limitDiv.textContent = '訂單數量已達上限（999筆），請聯繫管理員。';
          document.getElementById('submitButton').parentNode.insertBefore(limitDiv, document.getElementById('submitButton'));
          document.getElementById('submitButton').disabled = false;
          document.getElementById('loadingSpinner').classList.remove('show');
          return;
        }

        const result = await window.dataSdk.create(formData);

        if (result.isOk) {
          const emailResult = await sendOrderEmail(formData, selectedProducts);
          
          if (emailResult.success) {
            showThankYouPage(formData.paymentMethod);
          } else {
            showThankYouPage(formData.paymentMethod);
          }
        } else {
          console.error('Data SDK 儲存失敗:', result.error);
          const errorDiv = document.createElement('div');
          errorDiv.style.cssText = 'background: #f8d7da; border: 2px solid #f5c6cb; color: #721c24; padding: 16px; border-radius: 8px; margin-top: 16px; text-align: center;';
          errorDiv.textContent = '訂單提交失敗，請稍後再試：' + (result.error?.message || '未知錯誤');
          document.getElementById('submitButton').parentNode.insertBefore(errorDiv, document.getElementById('submitButton'));
        }
      } catch (error) {
        console.error('訂單提交發生錯誤:', error);
        const errorDiv = document.createElement('div');
        errorDiv.style.cssText = 'background: #f8d7da; border: 2px solid #f5c6cb; color: #721c24; padding: 16px; border-radius: 8px; margin-top: 16px; text-align: center;';
        errorDiv.textContent = '訂單提交發生錯誤：' + error.message;
        document.getElementById('submitButton').parentNode.insertBefore(errorDiv, document.getElementById('submitButton'));
      } finally {
        document.getElementById('submitButton').disabled = false;
        document.getElementById('loadingSpinner').classList.remove('show');
      }
    });

    async function onConfigChange(config) {
      const formTitle = document.getElementById('formTitle');
      const formSubtitle = document.getElementById('formSubtitle');

      formTitle.textContent = config.form_title || defaultConfig.form_title;
      formSubtitle.textContent = config.form_subtitle || defaultConfig.form_subtitle;
    }

    async function init() {
      initRegionSelectors();
      initProducts();

      if (window.dataSdk) {
        const initResult = await window.dataSdk.init(dataHandler);
        if (!initResult.isOk) {
          console.error('Data SDK 初始化失敗:', initResult.error);
        }
      }

      if (window.elementSdk) {
        await window.elementSdk.init({
          defaultConfig,
          onConfigChange,
          mapToCapabilities: (config) => ({
            recolorables: [],
            borderables: [],
            fontEditable: undefined,
            fontSizeable: undefined
          }),
          mapToEditPanelValues: (config) => new Map([
            ['form_title', config.form_title || defaultConfig.form_title],
            ['form_subtitle', config.form_subtitle || defaultConfig.form_subtitle]
          ])
        });

        await onConfigChange(window.elementSdk.config);
      } else {
        await onConfigChange(defaultConfig);
      }
    }

    init();
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9d2bf9ad07b2a9a9',t:'MTc3MTkwNDc4MC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>

