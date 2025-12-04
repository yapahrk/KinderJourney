# KinderJourney
<html lang="th">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kinder A Journey</title>
  <script src="/_sdk/data_sdk.js"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body {
      box-sizing: border-box;
    }
    
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: 'Comic Sans MS', 'Chalkboard SE', 'Marker Felt', cursive, sans-serif;
      background: linear-gradient(135deg, #A7D7F9 0%, #FFD4E5 100%);
      width: 100%;
      height: 100%;
      overflow-x: hidden;
    }

    .app-container {
      width: 100%;
      min-height: 100%;
      background: linear-gradient(135deg, #A7D7F9 0%, #FFD4E5 100%);
      padding: 2rem 1rem;
    }

    .main-content {
      max-width: 1200px;
      margin: 0 auto;
    }

    .app-header {
      text-align: center;
      margin-bottom: 2rem;
      color: white;
    }

    .app-header h1 {
      font-size: 2.5rem;
      margin-bottom: 0.5rem;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
    }

    .app-header p {
      font-size: 1.1rem;
      opacity: 0.95;
    }

    .tab-navigation {
      display: flex;
      gap: 0.5rem;
      margin-bottom: 2rem;
      background: rgba(255, 255, 255, 0.1);
      padding: 0.5rem;
      border-radius: 12px;
      backdrop-filter: blur(10px);
      flex-wrap: wrap;
    }

    .tab-btn {
      flex: 1;
      min-width: 120px;
      padding: 0.875rem 1rem;
      border: none;
      background: rgba(255, 255, 255, 0.2);
      color: white;
      border-radius: 8px;
      cursor: pointer;
      font-size: 0.95rem;
      font-weight: 500;
      transition: all 0.3s ease;
    }

    .tab-btn:hover {
      background: rgba(255, 255, 255, 0.3);
      transform: translateY(-2px);
    }

    .tab-btn.active {
      background: white;
      color: #667eea;
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
    }

    .tab-content {
      display: none;
      background: white;
      border-radius: 16px;
      padding: 2rem;
      box-shadow: 0 8px 32px rgba(0,0,0,0.1);
    }

    .tab-content.active {
      display: block;
      animation: fadeIn 0.3s ease;
    }

    @keyframes fadeIn {
      from {
        opacity: 0;
        transform: translateY(10px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    .section-title {
      font-size: 1.75rem;
      color: #FF9ECE;
      margin-bottom: 1.5rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }

    .milestone-age-selector {
      background: #FFF9E6;
      padding: 1.5rem;
      border-radius: 12px;
      margin-bottom: 2rem;
      border: 2px solid #FFD4E5;
    }

    .age-selector-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
      gap: 1rem;
    }

    .age-selector-btn {
      padding: 1rem;
      border: 2px solid #FFD4E5;
      background: white;
      color: #FF9ECE;
      border-radius: 8px;
      cursor: pointer;
      font-size: 1rem;
      font-weight: 600;
      transition: all 0.3s ease;
      font-family: inherit;
    }

    .age-selector-btn:hover {
      background: #FFD4E5;
      color: white;
      transform: translateY(-2px);
      box-shadow: 0 4px 12px rgba(255, 212, 229, 0.3);
    }

    .checklist-section {
      background: linear-gradient(135deg, #A7D7F9 20%, #FFD4E5 100%);
      padding: 2rem;
      border-radius: 12px;
      margin-bottom: 2rem;
      box-shadow: 0 8px 32px rgba(0,0,0,0.15);
    }

    .checklist-section-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 1.5rem;
      color: white;
    }

    .checklist-section-header h3 {
      font-size: 1.5rem;
      color: white !important;
    }

    .milestone-checklist-group {
      background: white;
      padding: 1.5rem;
      border-radius: 12px;
      margin-bottom: 1rem;
    }

    .milestone-checklist-group h4 {
      color: #FF9ECE;
      font-size: 1.2rem;
      margin-bottom: 1rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }

    .milestone-checklist-item {
      background: #FFF9E6;
      padding: 1rem;
      border-radius: 8px;
      margin-bottom: 0.75rem;
      border-left: 4px solid #FFD4E5;
      transition: all 0.3s ease;
    }

    .milestone-checklist-item:hover {
      border-left-color: #FF9ECE;
      box-shadow: 0 2px 8px rgba(255, 158, 206, 0.2);
    }

    .milestone-checklist-item p {
      color: #333;
      line-height: 1.6;
    }

    .vaccine-checklist-item {
      background: #FFF9E6;
      padding: 1.25rem;
      border-radius: 8px;
      margin-bottom: 0.75rem;
      border-left: 4px solid #A7D7F9;
      transition: all 0.3s ease;
    }

    .vaccine-checklist-item:hover {
      border-left-color: #667eea;
      box-shadow: 0 2px 8px rgba(103, 126, 234, 0.2);
    }

    .vaccine-checklist-item-title {
      font-size: 1.1rem;
      font-weight: 600;
      color: #667eea;
      margin-bottom: 0.5rem;
    }

    .vaccine-checklist-item-desc {
      color: #666;
      line-height: 1.6;
      font-size: 0.95rem;
    }

    .activity-card {
      background: #FFF9E6;
      padding: 1.25rem;
      border-radius: 12px;
      margin-bottom: 1rem;
      border-left: 4px solid #FF9ECE;
      transition: all 0.3s ease;
    }

    .activity-card:hover {
      border-left-color: #667eea;
      box-shadow: 0 4px 12px rgba(255, 158, 206, 0.2);
      transform: translateY(-2px);
    }

    .activity-card-title {
      font-size: 1.15rem;
      font-weight: 600;
      color: #FF9ECE;
      margin-bottom: 0.75rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }

    .activity-card-desc {
      color: #666;
      line-height: 1.6;
      font-size: 0.95rem;
      margin-bottom: 0.75rem;
    }

    .activity-card-benefits {
      background: rgba(167, 215, 249, 0.2);
      padding: 0.75rem;
      border-radius: 6px;
      font-size: 0.9rem;
      color: #555;
      border-left: 3px solid #A7D7F9;
    }

    .add-form {
      background: #FFF9E6;
      padding: 1.5rem;
      border-radius: 12px;
      margin-bottom: 2rem;
      border: 2px dashed #FFD4E5;
    }

    .form-row {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 1rem;
      margin-bottom: 1rem;
    }

    .form-group {
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }

    .form-group label {
      font-weight: 600;
      color: #333;
      font-size: 0.9rem;
    }

    .form-group input,
    .form-group select,
    .form-group textarea {
      padding: 0.75rem;
      border: 2px solid #FFD4E5;
      border-radius: 8px;
      font-size: 1rem;
      transition: border-color 0.3s ease;
      font-family: inherit;
    }

    .form-group input:focus,
    .form-group select:focus,
    .form-group textarea:focus {
      outline: none;
      border-color: #FF9ECE;
    }

    .form-group textarea {
      resize: vertical;
      min-height: 80px;
    }

    .btn-primary {
      background: linear-gradient(135deg, #FFD4E5 0%, #FFC7E0 100%);
      color: #FF9ECE;
      border: none;
      padding: 0.875rem 2rem;
      border-radius: 8px;
      font-size: 1rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: 0 4px 12px rgba(255, 212, 229, 0.3);
    }

    .btn-primary:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 20px rgba(255, 212, 229, 0.4);
    }

    .btn-primary:disabled {
      opacity: 0.6;
      cursor: not-allowed;
      transform: none;
    }

    .checklist-item {
      background: #FFF9E6;
      border: 2px solid #FFD4E5;
      border-radius: 12px;
      padding: 1.25rem;
      margin-bottom: 1rem;
      transition: all 0.3s ease;
    }

    .checklist-item:hover {
      border-color: #FF9ECE;
      box-shadow: 0 4px 12px rgba(255, 158, 206, 0.1);
    }

    .checklist-item.completed {
      background: #E8F8F5;
      border-color: #A7E7D8;
    }

    .checklist-header {
      display: flex;
      align-items: start;
      gap: 1rem;
      margin-bottom: 0.75rem;
    }

    .checkbox-wrapper {
      display: flex;
      align-items: center;
      margin-top: 0.25rem;
    }

    .checkbox-wrapper input[type="checkbox"] {
      width: 24px;
      height: 24px;
      cursor: pointer;
      accent-color: #FF9ECE;
    }

    .checklist-content {
      flex: 1;
    }

    .checklist-title {
      font-size: 1.1rem;
      font-weight: 600;
      color: #333;
      margin-bottom: 0.5rem;
    }

    .checklist-meta {
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
      font-size: 0.9rem;
      color: #666;
      margin-bottom: 0.75rem;
    }

    .checklist-meta span {
      display: flex;
      align-items: center;
      gap: 0.25rem;
    }

    .checklist-notes {
      background: #FFF9E6;
      padding: 0.875rem;
      border-radius: 8px;
      font-size: 0.95rem;
      color: #666;
      border-left: 4px solid #FFD4E5;
      margin-top: 0.75rem;
    }

    .checklist-actions {
      display: flex;
      gap: 0.5rem;
      margin-top: 0.75rem;
    }

    .btn-small {
      padding: 0.5rem 1rem;
      border: none;
      border-radius: 6px;
      font-size: 0.875rem;
      cursor: pointer;
      transition: all 0.2s ease;
      font-weight: 500;
    }

    .btn-delete {
      background: #fee;
      color: #dc2626;
    }

    .btn-delete:hover {
      background: #fcc;
    }

    .chart-container {
      background: #FFF9E6;
      padding: 2rem;
      border-radius: 12px;
      margin-bottom: 2rem;
    }

    .chart-wrapper {
      position: relative;
      height: 300px;
    }

    .stats-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 1.5rem;
      margin-bottom: 2rem;
    }

    .stat-card {
      background: linear-gradient(135deg, #A7D7F9 0%, #FFD4E5 100%);
      color: white;
      padding: 1.5rem;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(167, 215, 249, 0.3);
    }

    .stat-value {
      font-size: 2.5rem;
      font-weight: 700;
      margin-bottom: 0.25rem;
    }

    .stat-label {
      font-size: 1rem;
      opacity: 0.9;
    }

    .empty-state {
      text-align: center;
      padding: 3rem 1rem;
      color: #666;
    }

    .empty-state-icon {
      font-size: 4rem;
      margin-bottom: 1rem;
    }

    .empty-state p {
      font-size: 1.1rem;
    }

    .loading-spinner {
      display: inline-block;
      width: 20px;
      height: 20px;
      border: 3px solid rgba(255,255,255,.3);
      border-radius: 50%;
      border-top-color: white;
      animation: spin 1s ease-in-out infinite;
    }

    @keyframes spin {
      to { transform: rotate(360deg); }
    }

    .milestone-categories {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1rem;
      margin-bottom: 2rem;
    }

    .category-card {
      background: linear-gradient(135deg, #FFD4E5 0%, #FFC7E0 100%);
      color: white;
      padding: 1.25rem;
      border-radius: 12px;
      cursor: pointer;
      transition: all 0.3s ease;
      text-align: center;
    }

    .category-card:hover {
      transform: translateY(-4px);
      box-shadow: 0 8px 20px rgba(255, 212, 229, 0.4);
    }

    .category-card.selected {
      background: linear-gradient(135deg, #A7E7D8 0%, #7FD9C7 100%);
      box-shadow: 0 8px 20px rgba(167, 231, 216, 0.4);
    }

    .category-icon {
      font-size: 2.5rem;
      margin-bottom: 0.5rem;
    }

    .category-name {
      font-size: 1.1rem;
      font-weight: 600;
    }

    @media (max-width: 768px) {
      .app-header h1 {
        font-size: 2rem;
      }
      
      .form-row {
        grid-template-columns: 1fr;
      }
      
      .tab-navigation {
        overflow-x: auto;
        flex-wrap: nowrap;
      }
      
      .tab-btn {
        white-space: nowrap;
      }

      .age-selector-grid {
        grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
      }
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
  <script src="https://cdn.tailwindcss.com" type="text/javascript"></script>
 </head>
 <body>
  <div class="app-container">
   <div class="main-content">
    <header class="app-header">
     <h1 id="app-title">🌟 Kinder A Journey</h1>
     <p id="welcome-message">ติดตามพัฒนาการลูกน้อยของคุณ</p>
    </header>
    <nav class="tab-navigation"><button class="tab-btn active" data-tab="dashboard">📊 ภาพรวม</button> <button class="tab-btn" data-tab="development">🧠 พัฒนาการ</button> <button class="tab-btn" data-tab="vaccine">💉 วัคซีน</button> <button class="tab-btn" data-tab="nutrition">🍎 โภชนาการ</button> <button class="tab-btn" data-tab="activities">🎨 กิจกรรม</button>
    </nav><!-- Dashboard Tab -->
    <div id="dashboard" class="tab-content active">
     <h2 class="section-title">📊 ภาพรวมพัฒนาการ</h2>
     <div class="stats-grid">
      <div class="stat-card">
       <div class="stat-value" id="total-milestones">
        0
       </div>
       <div class="stat-label">
        พัฒนาการทั้งหมด
       </div>
      </div>
      <div class="stat-card">
       <div class="stat-value" id="completed-milestones">
        0
       </div>
       <div class="stat-label">
        ผ่านแล้ว
       </div>
      </div>
      <div class="stat-card">
       <div class="stat-value" id="total-vaccines">
        0
       </div>
       <div class="stat-label">
        วัคซีนที่ได้รับ
       </div>
      </div>
      <div class="stat-card">
       <div class="stat-value" id="total-activities">
        0
       </div>
       <div class="stat-label">
        กิจกรรมทั้งหมด
       </div>
      </div>
     </div>
     <div class="chart-container">
      <h3 style="margin-bottom: 1.5rem; color: #667eea;">กราฟความคืบหน้าตามเดือน</h3>
      <div class="chart-wrapper">
       <canvas id="progressChart"></canvas>
      </div>
     </div>
    </div><!-- Development Tab -->
    <div id="development" class="tab-content">
     <h2 class="section-title">🧠 ติดตามพัฒนาการ</h2>
     <div class="milestone-age-selector">
      <h3 style="margin-bottom: 1rem; color: #FF9ECE;">📅 เลือกช่วงอายุเพื่อดู Checklist พัฒนาการ</h3>
      <div class="age-selector-grid"><button class="age-selector-btn" data-age="0-3">0-3 เดือน</button> <button class="age-selector-btn" data-age="4-6">4-6 เดือน</button> <button class="age-selector-btn" data-age="7-9">7-9 เดือน</button> <button class="age-selector-btn" data-age="10-12">10-12 เดือน</button> <button class="age-selector-btn" data-age="13-18">13-18 เดือน</button> <button class="age-selector-btn" data-age="19-24">19-24 เดือน</button> <button class="age-selector-btn" data-age="25-36">25-36 เดือน</button>
      </div>
     </div>
     <div id="milestone-checklist-container" style="display: none;">
      <div class="checklist-section">
       <div class="checklist-section-header">
        <h3 id="checklist-age-title">Checklist พัฒนาการ</h3><button id="close-checklist" class="btn-small" style="background: white; color: #FF9ECE;">ปิด</button>
       </div>
       <div id="milestone-checklist-content"></div>
      </div>
     </div>
     <div class="milestone-categories" id="milestone-categories">
      <div class="category-card selected" data-category="all">
       <div class="category-icon">
        📋
       </div>
       <div class="category-name">
        ทั้งหมด
       </div>
      </div>
      <div class="category-card" data-category="physical">
       <div class="category-icon">
        🏃
       </div>
       <div class="category-name">
        ร่างกาย
       </div>
      </div>
      <div class="category-card" data-category="cognitive">
       <div class="category-icon">
        🧩
       </div>
       <div class="category-name">
        สติปัญญา
       </div>
      </div>
      <div class="category-card" data-category="social">
       <div class="category-icon">
        👥
       </div>
       <div class="category-name">
        สังคม
       </div>
      </div>
      <div class="category-card" data-category="language">
       <div class="category-icon">
        💬
       </div>
       <div class="category-name">
        ภาษา
       </div>
      </div>
     </div>
     <div class="add-form">
      <h3 style="margin-bottom: 1rem; color: #FF9ECE;">เพิ่มข้อมูลพัฒนาการ</h3>
      <form id="development-form">
       <div class="form-row">
        <div class="form-group"><label for="dev-child-name">ชื่อเด็ก</label> <input type="text" id="dev-child-name" required>
        </div>
        <div class="form-group"><label for="dev-title">พัฒนาการ</label> <input type="text" id="dev-title" placeholder="เช่น เริ่มนั่งได้เอง" required>
        </div>
        <div class="form-group"><label for="dev-category">หมวดหมู่</label> <select id="dev-category" required> <option value="physical">ร่างกาย</option> <option value="cognitive">สติปัญญา</option> <option value="social">สังคม</option> <option value="language">ภาษา</option> </select>
        </div>
        <div class="form-group"><label for="dev-age">อายุ (เดือน)</label> <input type="number" id="dev-age" min="0" max="36" required>
        </div>
        <div class="form-group"><label for="dev-date">วันที่</label> <input type="date" id="dev-date" required>
        </div>
       </div>
       <div class="form-group"><label for="dev-notes">หมายเหตุ</label> <textarea id="dev-notes" placeholder="บันทึกรายละเอียดเพิ่มเติม..."></textarea>
       </div><button type="submit" class="btn-primary"> <span class="btn-text">บันทึกพัฒนาการ</span> </button>
      </form>
     </div>
     <div id="development-list"></div>
    </div><!-- Vaccine Tab -->
    <div id="vaccine" class="tab-content">
     <h2 class="section-title">💉 ตารางวัคซีน</h2>
     <div class="milestone-age-selector">
      <h3 style="margin-bottom: 1rem; color: #FF9ECE;">📅 ตารางวัคซีนตามช่วงอายุ</h3>
      <div class="age-selector-grid"><button class="age-selector-btn" data-vaccine-age="birth">แรกเกิด</button> <button class="age-selector-btn" data-vaccine-age="2-months">2 เดือน</button> <button class="age-selector-btn" data-vaccine-age="4-months">4 เดือน</button> <button class="age-selector-btn" data-vaccine-age="6-months">6 เดือน</button> <button class="age-selector-btn" data-vaccine-age="9-months">9 เดือน</button> <button class="age-selector-btn" data-vaccine-age="12-months">12 เดือน</button> <button class="age-selector-btn" data-vaccine-age="18-months">18 เดือน</button> <button class="age-selector-btn" data-vaccine-age="24-months">2 ปี</button> <button class="age-selector-btn" data-vaccine-age="30-months">2.5 ปี</button> <button class="age-selector-btn" data-vaccine-age="4-years">4 ปี</button>
      </div>
     </div>
     <div id="vaccine-checklist-container" style="display: none;">
      <div class="checklist-section">
       <div class="checklist-section-header">
        <h3 id="vaccine-checklist-age-title">ตารางวัคซีน</h3><button id="close-vaccine-checklist" class="btn-small" style="background: white; color: #FF9ECE;">ปิด</button>
       </div>
       <div id="vaccine-checklist-content"></div>
      </div>
     </div>
     <div class="add-form">
      <h3 style="margin-bottom: 1rem; color: #FF9ECE;">บันทึกการรับวัคซีน</h3>
      <form id="vaccine-form">
       <div class="form-row">
        <div class="form-group"><label for="vac-child-name">ชื่อเด็ก</label> <input type="text" id="vac-child-name" required>
        </div>
        <div class="form-group"><label for="vac-title">ชื่อวัคซีน</label> <input type="text" id="vac-title" placeholder="เช่น วัคซีน BCG" required>
        </div>
        <div class="form-group"><label for="vac-age">อายุที่รับ (เดือน)</label> <input type="number" id="vac-age" min="0" max="36" required>
        </div>
        <div class="form-group"><label for="vac-date">วันที่รับวัคซีน</label> <input type="date" id="vac-date" required>
        </div>
       </div>
       <div class="form-group"><label for="vac-notes">หมายเหตุ</label> <textarea id="vac-notes" placeholder="บันทึกอาการหลังฉีด หรือข้อมูลเพิ่มเติม..."></textarea>
       </div><button type="submit" class="btn-primary"> <span class="btn-text">บันทึกวัคซีน</span> </button>
      </form>
     </div>
     <div id="vaccine-list"></div>
    </div><!-- Nutrition Tab -->
    <div id="nutrition" class="tab-content">
     <h2 class="section-title">🍎 บันทึกโภชนาการ</h2>
     <div class="milestone-age-selector">
      <h3 style="margin-bottom: 1rem; color: #FF9ECE;">🍽️ คำแนะนำอาหารตามช่วงอายุ</h3>
      <div class="age-selector-grid"><button class="age-selector-btn" data-nutrition-age="0-6">0-6 เดือน</button> <button class="age-selector-btn" data-nutrition-age="6-12">6-12 เดือน</button> <button class="age-selector-btn" data-nutrition-age="12-24">1-2 ปี</button> <button class="age-selector-btn" data-nutrition-age="24-36">2-3 ปี</button> <button class="age-selector-btn" data-nutrition-age="36-60">3-5 ปี</button>
      </div>
     </div>
     <div id="nutrition-guide-container" style="display: none;">
      <div class="checklist-section">
       <div class="checklist-section-header">
        <h3 id="nutrition-guide-age-title">คำแนะนำอาหาร</h3><button id="close-nutrition-guide" class="btn-small" style="background: white; color: #FF9ECE;">ปิด</button>
       </div>
       <div id="nutrition-guide-content"></div>
      </div>
     </div>
     <div class="add-form">
      <h3 style="margin-bottom: 1rem; color: #FF9ECE;">เพิ่มข้อมูลโภชนาการ</h3>
      <form id="nutrition-form">
       <div class="form-row">
        <div class="form-group"><label for="nutr-child-name">ชื่อเด็ก</label> <input type="text" id="nutr-child-name" required>
        </div>
        <div class="form-group"><label for="nutr-title">ชนิดอาหาร/สารอาหาร</label> <input type="text" id="nutr-title" placeholder="เช่น นมแม่, ธาตุเหล็ก" required>
        </div>
        <div class="form-group"><label for="nutr-category">ประเภท</label> <select id="nutr-category" required> <option value="milk">นม</option> <option value="food">อาหาร</option> <option value="supplement">วิตามิน/แร่ธาตุ</option> </select>
        </div>
        <div class="form-group"><label for="nutr-date">วันที่</label> <input type="date" id="nutr-date" required>
        </div>
       </div>
       <div class="form-group"><label for="nutr-notes">หมายเหตุ</label> <textarea id="nutr-notes" placeholder="บันทึกปริมาณ ความถี่ หรือข้อมูลเพิ่มเติม..."></textarea>
       </div><button type="submit" class="btn-primary"> <span class="btn-text">บันทึกโภชนาการ</span> </button>
      </form>
     </div>
     <div id="nutrition-list"></div>
    </div><!-- Activities Tab -->
    <div id="activities" class="tab-content">
     <h2 class="section-title">🎨 กิจกรรมและการเตรียมความพร้อม</h2>
     <div class="milestone-age-selector">
      <h3 style="margin-bottom: 1rem; color: #FF9ECE;">🎯 กิจกรรมแนะนำตามช่วงอายุ</h3>
      <div class="age-selector-grid"><button class="age-selector-btn" data-activity-age="0-6">0-6 เดือน</button> <button class="age-selector-btn" data-activity-age="6-12">6-12 เดือน</button> <button class="age-selector-btn" data-activity-age="12-24">1-2 ปี</button> <button class="age-selector-btn" data-activity-age="24-36">2-3 ปี</button> <button class="age-selector-btn" data-activity-age="36-60">3-5 ปี</button>
      </div>
     </div>
     <div id="activity-guide-container" style="display: none;">
      <div class="checklist-section">
       <div class="checklist-section-header">
        <h3 id="activity-guide-age-title">กิจกรรมแนะนำ</h3><button id="close-activity-guide" class="btn-small" style="background: white; color: #FF9ECE;">ปิด</button>
       </div>
       <div id="activity-guide-content"></div>
      </div>
     </div>
     <div class="add-form">
      <h3 style="margin-bottom: 1rem; color: #FF9ECE;">เพิ่มกิจกรรม</h3>
      <form id="activity-form">
       <div class="form-row">
        <div class="form-group"><label for="act-child-name">ชื่อเด็ก</label> <input type="text" id="act-child-name" required>
        </div>
        <div class="form-group"><label for="act-title">ชื่อกิจกรรม</label> <input type="text" id="act-title" placeholder="เช่น อ่านนิทาน, ร้องเพลง" required>
        </div>
        <div class="form-group"><label for="act-category">ประเภท</label> <select id="act-category" required> <option value="learning">การเรียนรู้</option> <option value="play">การเล่น</option> <option value="social">ทักษะสังคม</option> <option value="preparation">เตรียมความพร้อม</option> </select>
        </div>
        <div class="form-group"><label for="act-date">วันที่</label> <input type="date" id="act-date" required>
        </div>
       </div>
       <div class="form-group"><label for="act-notes">หมายเหตุ</label> <textarea id="act-notes" placeholder="บันทึกรายละเอียดกิจกรรม ความคืบหน้า..."></textarea>
       </div><button type="submit" class="btn-primary"> <span class="btn-text">บันทึกกิจกรรม</span> </button>
      </form>
     </div>
     <div id="activity-list"></div>
    </div>
   </div>
  </div>
  <script>
    let allData = [];
    let progressChart = null;
    let selectedCategory = 'all';

    const defaultConfig = {
      app_title: "🌟 Kinder A Journey",
      welcome_message: "ติดตามพัฒนาการลูกน้อยของคุณ",
      background_color: "#A7D7F9",
      surface_color: "#FFF9E6",
      text_color: "#FF9ECE",
      primary_action_color: "#FFD4E5",
      secondary_action_color: "#FFC7E0",
      font_family: "Comic Sans MS",
      font_size: 16
    };

    const milestoneData = {
      "0-3": {
        title: "พัฒนาการ 0-3 เดือน",
        categories: {
          physical: [
            "ยกศีรษะขึ้นได้เมื่อนอนคว่ำ",
            "เคลื่อนไหวแขนขาอย่างสม่ำเสมอ",
            "เริ่มเหยียดแขนขาได้",
            "กำมือแน่น แต่เริ่มคลายมือได้"
          ],
          cognitive: [
            "จ้องมองใบหน้าคนใกล้ชิด",
            "ติดตามวัตถุที่เคลื่อนไหว",
            "สนใจเสียงดังและแสงสว่าง",
            "เริ่มรู้จักเสียงของคนในครอบครัว"
          ],
          social: [
            "ยิ้มให้คนใกล้ชิด",
            "สบตาและมองหน้าผู้ดูแล",
            "สงบลงเมื่อได้ยินเสียงที่คุ้นเคย",
            "แสดงอารมณ์ด้วยการร้องไห้"
          ],
          language: [
            "ส่งเสียงครวญครางเบาๆ",
            "ส่งเสียงตอบสนองเมื่อมีคนพูดด้วย",
            "ร้องไห้แตกต่างกันตามความต้องการ",
            "เริ่มส่งเสียง 'อู' 'อา'"
          ]
        }
      },
      "4-6": {
        title: "พัฒนาการ 4-6 เดือน",
        categories: {
          physical: [
            "พลิกตัวจากหงายเป็นคว่ำได้",
            "ยกหัวและอกขึ้นได้ชัดเจน",
            "นั่งโดยมีที่พิง",
            "เอื้อมมือหยิบของเล่น",
            "ถ่ายทอดของจากมือข้างหนึ่งไปอีกข้าง"
          ],
          cognitive: [
            "สำรวจของด้วยการเอาเข้าปาก",
            "หาแหล่งที่มาของเสียง",
            "เริ่มแสดงความสนใจในภาพในหนังสือ",
            "รู้จักวัตถุที่คุ้นเคย"
          ],
          social: [
            "รู้จักใบหน้าคนคุ้นเคย",
            "ชอบเล่นกับคนอื่น โดยเฉพาะพ่อแม่",
            "ตอบสนองต่ออารมณ์ของคนอื่น",
            "มักมองตัวเองในกระจก"
          ],
          language: [
            "ส่งเสียงตอบเมื่อมีคนพูดด้วย",
            "ส่งเสียงแสดงความชื่นชมและไม่พอใจ",
            "เริ่มพูดพยางค์ 'บา-บา' 'มา-มา'",
            "ใช้เสียงเพื่อดึงความสนใจ"
          ]
        }
      },
      "7-9": {
        title: "พัฒนาการ 7-9 เดือน",
        categories: {
          physical: [
            "นั่งได้เองโดยไม่ต้องพิง",
            "คลานหรือขยับเคลื่อนที่ได้",
            "ยืนโดยยึดเกาะ",
            "หยิบของเล็กด้วยนิ้วหัวแม่มือและนิ้วชี้",
            "เคาะของเข้าหากันได้"
          ],
          cognitive: [
            "มองหาของที่ตกหล่น",
            "เริ่มเข้าใจคำง่ายๆ เช่น 'ไม่ได้'",
            "ชี้สิ่งต่างๆ ด้วยนิ้ว",
            "เริ่มเล่นสำรวจความสัมพันธ์เชิงเหตุผล"
          ],
          social: [
            "แยกแยะคนแปลกหน้า อาจกลัวหรือเขิน",
            "ชอบเกมซ่อนหา (peek-a-boo)",
            "แสดงความรักต่อผู้ดูแลหลัก",
            "มีของเล่นที่ชอบเป็นพิเศษ"
          ],
          language: [
            "เข้าใจคำว่า 'ไม่'",
            "พูดพยางค์ซ้ำๆ หลายแบบ",
            "ใช้น้ำเสียงต่างๆ เมื่อพูด",
            "ลอกเลียนเสียงและท่าทาง"
          ]
        }
      },
      "10-12": {
        title: "พัฒนาการ 10-12 เดือน",
        categories: {
          physical: [
            "ยืนได้เองโดยไม่ต้องพิง",
            "เดินโดยจูงมือ หรือเริ่มเดินได้เอง",
            "ดีดนิ้วมือ",
            "ดื่มจากแก้วได้",
            "หยิบของเล็กได้แม่นยำขึ้น"
          ],
          cognitive: [
            "สำรวจของด้วยวิธีต่างๆ (เขย่า, เคาะ, โยน)",
            "หาของที่ถูกซ่อนได้ง่ายขึ้น",
            "เลียนแบบการกระทำง่ายๆ",
            "ใช้ของอย่างถูกต้อง (แปรงผม, โทรศัพท์)"
          ],
          social: [
            "ขี้อาย หรือกลัวคนแปลกหน้า",
            "ร้องไห้เมื่อพ่อแม่จากไป",
            "มีคนหรือของโปรดชัดเจน",
            "แสดงความกลัวในบางสถานการณ์"
          ],
          language: [
            "เปลี่ยนน้ำเสียงเมื่อพูด",
            "พูดคำง่ายๆ เช่น 'พ่อ' 'แม่' 'ไป'",
            "ส่ายหัว 'ไม่'",
            "โบกมือ 'บ๊ายบาย'"
          ]
        }
      },
      "13-18": {
        title: "พัฒนาการ 13-18 เดือน",
        categories: {
          physical: [
            "เดินได้อย่างมั่นคง",
            "วิ่งเร็วขึ้น",
            "ลากหรือดึงของเล่นขณะเดิน",
            "ปีนขึ้นเฟอร์นิเจอร์",
            "เดินขึ้นบันไดโดยจับราวบันได"
          ],
          cognitive: [
            "ชี้เพื่อแสดงสิ่งที่สนใจให้คนอื่นเห็น",
            "รู้จักใช้ของใช้ในบ้านได้",
            "เล่นเกมง่ายๆ เช่น ซ่อนหา",
            "ชี้ส่วนต่างๆ ของร่างกายเมื่อถูกถาม"
          ],
          social: [
            "แสดงความรักต่อคนที่คุ้นเคย",
            "สนใจเด็กคนอื่น",
            "ยื่นของเล่นให้คนอื่นเล่นด้วย",
            "อาจมีอาการหงุดหงิดหรือจู้จี้"
          ],
          language: [
            "พูดคำง่ายๆ หลายคำ (15-20 คำ)",
            "ส่ายหัวและพยักหน้าเพื่อตอบ",
            "ชี้สิ่งที่ต้องการ",
            "ทำตามคำสั่งง่ายๆ"
          ]
        }
      },
      "19-24": {
        title: "พัฒนาการ 19-24 เดือน",
        categories: {
          physical: [
            "วิ่งได้คล่องขึ้น",
            "เตะบอลได้",
            "เริ่มกระโดดด้วยเท้าเดียว",
            "ขึ้นลงบันไดโดยจับราว",
            "ปัดลูกบอลได้"
          ],
          cognitive: [
            "จำรูปร่างและสีได้",
            "เริ่มเล่นเกมจินตนาการ",
            "สร้างอะไรด้วยบล็อกง่ายๆ",
            "รู้จักแยกสี รูปร่าง ตำแหน่ง"
          ],
          social: [
            "ลอกเลียนพฤติกรรมผู้ใหญ่และเด็กคนอื่น",
            "ตื่นเต้นเมื่ออยู่กับเด็กคนอื่น",
            "แสดงความเป็นอิสระมากขึ้น",
            "เริ่มมีพฤติกรรมต่อต้าน"
          ],
          language: [
            "ชี้สิ่งต่างๆ ในหนังสือเมื่อถูกถาม",
            "รู้จักชื่อคนที่คุ้นเคย และส่วนต่างๆ ของร่างกาย",
            "พูดประโยค 2-4 คำ",
            "ทำตามคำสั่ง 2 ขั้นตอน"
          ]
        }
      },
      "25-36": {
        title: "พัฒนาการ 25-36 เดือน",
        categories: {
          physical: [
            "ปีนป่ายได้ดี",
            "วิ่งได้อย่างคล่องแคล่ว",
            "เดินขึ้นลงบันไดได้เองแต่ละขั้น",
            "เตะและโยนลูกบอลได้",
            "วาดเส้นและวงกลมได้"
          ],
          cognitive: [
            "จับคู่สีและรูปร่างได้",
            "ปะภาพตัดต่อ 3-4 ชิ้นได้",
            "เข้าใจแนวคิด 'สอง'",
            "เล่นเกมแสร้งทำที่ซับซ้อนขึ้น"
          ],
          social: [
            "เลียนแบบพ่อแม่และเพื่อน",
            "แสดงความรักต่อเพื่อนโดยไม่ต้องบอก",
            "เริ่มรู้จักผลัดกันเล่น",
            "เข้าใจแนวคิด 'ของฉัน' และ 'ของเขา'"
          ],
          language: [
            "พูดประโยค 5-6 คำ",
            "สนทนาได้โดยใช้ 2-3 ประโยค",
            "ใช้คำบุพบท (ใน, บน, ใต้)",
            "พูดชื่อและนามสกุลได้"
          ]
        }
      }
    };

    const nutritionGuideData = {
      "0-6": {
        title: "อาหารแนะนำ 0-6 เดือน",
        description: "ช่วงนี้ลูกน้อยควรได้รับนมเป็นอาหารหลักเท่านั้น",
        categories: {
          main: {
            title: "🍼 อาหารหลัก",
            items: [
              { name: "นมแม่", detail: "ดีที่สุด! ให้นมแม่เพียงอย่างเดียวตลอด 6 เดือนแรก ฟรี มีภูมิคุ้มกัน เหมาะกับลูกที่สุด" },
              { name: "นมผสม", detail: "หากไม่สามารถให้นมแม่ได้ ใช้นมผสมสูตร 1 ตามคำแนะนำของแพทย์ ราคาประมาณ 300-800 บาท/กระป๋อง" }
            ]
          },
          important: {
            title: "⚠️ ข้อควรระวัง",
            items: [
              { name: "ไม่ควรให้อาหารแข็ง", detail: "ระบบย่อยอาหารยังไม่พร้อม" },
              { name: "ไม่ต้องให้น้ำเปล่า", detail: "นมแม่มีน้ำเพียงพอแล้ว" },
              { name: "หลีกเลี่ยงน้ำผลไม้", detail: "รอจนครบ 6 เดือนก่อน" }
            ]
          }
        }
      },
      "6-12": {
        title: "อาหารแนะนำ 6-12 เดือน",
        description: "เริ่มให้อาหารเสริมควบคู่นมแม่/นมผสม เน้นสารอาหารครบ 5 หมู่",
        categories: {
          protein: {
            title: "🥚 โปรตีน (ราคาประหยัด)",
            items: [
              { name: "ไข่", detail: "15-20 บาท/10 ฟอง - โปรตีนคุณภาพดี มีธาตุเหล็ก เริ่มจากไข่แดงก่อน" },
              { name: "เต้าหู้", detail: "10-15 บาท/แผ่น - โปรตีนจากพืช ราคาถูก ทำได้หลายเมนู" },
              { name: "ปลาทู", detail: "30-40 บาท/ตัว - มีโอเมก้า 3 ดีต่อสมอง ระวังก้าง" },
              { name: "ตับไก่", detail: "40-50 บาท/กก. - เหล็กสูง ป้องกันโลหิตจาง" }
            ]
          },
          carbs: {
            title: "🍚 แป้ง-คาร์โบไฮเดรต",
            items: [
              { name: "ข้าวหุงบด", detail: "ประมาณ 20 บาท/กก. - เริ่มจากข้าวต้มบดละเอียด" },
              { name: "ข้าวโอ๊ต", detail: "50-80 บาท/กก. - ทานง่าย มีไฟเบอร์" },
              { name: "มันเทศ", detail: "15-25 บาท/กก. - หวานธรรมชาติ มีวิตามินเอ" },
              { name: "ฟักทอง", detail: "20-30 บาท/กก. - หวาน นุ่ม ย่อยง่าย" }
            ]
          },
          vegetables: {
            title: "🥬 ผัก",
            items: [
              { name: "แครอท", detail: "20-30 บาท/กก. - วิตามินเอสูง ดีต่อสายตา" },
              { name: "บร็อกโคลี", detail: "30-40 บาท/กก. - วิตามินซี แคลเซียม" },
              { name: "ผักโขม", detail: "10-20 บาท/มัด - เหล็กสูง ป้องกันโลหิตจาง" },
              { name: "ผักกาดหอม", detail: "5-10 บาท/มัด - ราคาถูก มีวิตามินหลากหลาย" }
            ]
          },
          fruits: {
            title: "🍌 ผลไม้",
            items: [
              { name: "กล้วยน้ำว้า", detail: "10-20 บาท/หวี - นุ่ม หวาน พลังงานดี" },
              { name: "มะละกอ", detail: "15-25 บาท/กก. - ย่อยง่าย ช่วยระบบขับถ่าย" },
              { name: "แอปเปิ้ล", detail: "40-60 บาท/กก. - นึ่งหรือขูดบด" },
              { name: "ฝรั่ง", detail: "20-30 บาท/กก. - วิตามินซีสูง" }
            ]
          },
          tips: {
            title: "💡 เคล็ดลับ",
            items: [
              { name: "เริ่มทีละอย่าง", detail: "สังเกตอาการแพ้ 3-5 วัน ก่อนให้อย่างใหม่" },
              { name: "ความเข้มข้น", detail: "เริ่มจากเหลว → ข้น → บด → ก้อนเล็ก" },
              { name: "ยังต้องกินนม", detail: "นมยังเป็นอาหารหลัก อาหารเสริมเป็นของเสริม" }
            ]
          }
        }
      },
      "12-24": {
        title: "อาหารแนะนำ 1-2 ปี",
        description: "เริ่มกินอาหารครอบครัวได้ แต่ปรับเนื้อสัมผัสให้เหมาะสม",
        categories: {
          meals: {
            title: "🍽️ มื้ออาหารหลัก",
            items: [
              { name: "ข้าวผัดไข่", detail: "20-30 บาท/จาน - ง่าย ทำเอง ประหยัด" },
              { name: "ข้าวต้มปลา", detail: "25-35 บาท/ชาม - อ่อนนุ่ม ย่อยง่าย" },
              { name: "ข้าวหน้าไก่ตับ", detail: "30-40 บาท/จาน - เหล็กสูง" },
              { name: "ก๋วยเตี๋ยวต้มยำ", detail: "25-35 บาท/ชาม - เลือกเส้นเล็กบด" }
            ]
          },
          protein: {
            title: "🍗 โปรตีนราคาประหยัด",
            items: [
              { name: "ไก่สับ", detail: "80-100 บาท/กก. - ทำได้หลายเมนู" },
              { name: "ปลากระพง", detail: "120-150 บาท/กก. - ก้างน้อย เนื้อนุ่ม" },
              { name: "ไข่เจียว", detail: "10-15 บาท/จาน - เมนูที่เด็กชอบ" },
              { name: "ถั่วลันเตา", detail: "30-40 บาท/กก. - โปรตีนพืชถูก" }
            ]
          },
          snacks: {
            title: "🍪 ของว่าง",
            items: [
              { name: "กล้วยตาก", detail: "20-30 บาท/ห่อ - พลังงานดี ไม่มีน้ำตาลเติม" },
              { name: "ขนมปังโฮลวีท", detail: "25-35 บาท/ถุง - มีไฟเบอร์" },
              { name: "น้ำเต้าหู้", detail: "10-15 บาท/ขวด - โปรตีน แคลเซียม" },
              { name: "ข้าวเกรียบ", detail: "10-20 บาท/ห่อ - กรุบกรอบ ไม่เค็มมาก" }
            ]
          },
          avoid: {
            title: "❌ ควรหลีกเลี่ยง",
            items: [
              { name: "น้ำตาล เกลือ", detail: "ไม่ควรใส่มาก ให้ลูกได้รสชาติธรรมชาติ" },
              { name: "น้ำอัดลม", detail: "ไม่มีประโยชน์ ทำลายฟัน" },
              { name: "ขนมหวานจัด", detail: "เค้ก ช็อกโกแลต ลูกอม" },
              { name: "อาหารแข็งมาก", detail: "ถั่วเต็มเมล็ด องุ่นทั้งผล (อาจสำลัก)" }
            ]
          }
        }
      },
      "24-36": {
        title: "อาหารแนะนำ 2-3 ปี",
        description: "กินอาหารครอบครัวได้แล้ว เน้นหลากหลาย ครบ 5 หมู่",
        categories: {
          breakfast: {
            title: "🌅 อาหารเช้า (30-50 บาท)",
            items: [
              { name: "ขนมปัง + ไข่ + นม", detail: "30 บาท - พลังงานดี เริ่มวันใหม่" },
              { name: "ข้าวต้ม + เนื้อหมูสับ", detail: "35 บาท - อ่อนนุ่ม อิ่มนาน" },
              { name: "โจ๊กปลา + ผักโขม", detail: "30 บาท - ย่อยง่าย มีเหล็ก" },
              { name: "ข้าวเหนียว + ไก่ย่าง", detail: "40 บาท - เด็กไทยชอบ" }
            ]
          },
          lunch: {
            title: "☀️ อาหารกลางวัน (40-70 บาท)",
            items: [
              { name: "ข้าวราดแกงผักผสม", detail: "40 บาท - ครบ 5 หมู่" },
              { name: "ผัดผัก + เนื้อสัตว์ + ข้าว", detail: "50 บาท - ทำที่บ้าน" },
              { name: "ข้าวมันไก่", detail: "40-50 บาท - เด็กชอบ มีผักกาดดอง" },
              { name: "ข้าวผัดอเมริกัน", detail: "50-60 บาท - มีผักเยอะ" }
            ]
          },
          dinner: {
            title: "🌙 อาหารเย็น (40-70 บาท)",
            items: [
              { name: "ส้มตำไทย (ไม่เผ็ด) + ไก่ย่าง", detail: "50 บาท - วิตามินเยอะ" },
              { name: "ผัดไทยไม่เผ็ด", detail: "40 บาท - โปรตีนจากไข่ ถั่ว" },
              { name: "แกงจืดเต้าหู้ + ข้าว", detail: "35 บาท - ง่าย ถูก มีประโยชน์" },
              { name: "ไข่พะโล้", detail: "30 บาท - ทำง่าย เด็กชอบ" }
            ]
          },
          snacks: {
            title: "🍎 ของว่าง 2 มื้อ",
            items: [
              { name: "ผลไม้ตามฤดูกาล", detail: "10-20 บาท - กล้วย มะละกอ ฝรั่ง" },
              { name: "ข้าวเหนียวมะม่วง", detail: "25-30 บาท - พลังงานดี (1-2 ครั้ง/สัปดาห์)" },
              { name: "ไข่ต้ม", detail: "5-10 บาท - โปรตีนดี" },
              { name: "นมเปรี้ยว", detail: "15-20 บาท - ดีต่อลำไส้" }
            ]
          },
          tips: {
            title: "📌 คำแนะนำ",
            items: [
              { name: "ให้กินเอง", detail: "ฝึกทักษะการใช้ช้อนส้อม" },
              { name: "จุกจิก", detail: "เป็นเรื่องปกติ อย่าบังคับ" },
              { name: "น้ำเปล่า", detail: "ดีที่สุด ลดน้ำผลไม้หวาน" }
            ]
          }
        }
      },
      "36-60": {
        title: "อาหารแนะนำ 3-5 ปี",
        description: "วัยเตรียมเข้าโรงเรียน เน้นอาหารที่ให้พลังงานและบำรุงสมอง",
        categories: {
          daily_meals: {
            title: "🍱 มื้ออาหารหลัก 3 มื้อ",
            items: [
              { name: "ข้าวกล่อง (เด็ก)", detail: "40-60 บาท - ข้าว + กับข้าว 2 อย่าง + ผลไม้" },
              { name: "ก๋วยเตี๋ยวต้มยำ", detail: "40-50 บาท - มีผัก เนื้อสัตว์ครบ" },
              { name: "ข้าวหมูแดง", detail: "50-60 บาท - เด็กชอบ มีผัก" },
              { name: "ข้าวผัดหมู", detail: "40-50 บาท - ครบ 5 หมู่ในจานเดียว" }
            ]
          },
          brain_food: {
            title: "🧠 อาหารบำรุงสมอง",
            items: [
              { name: "ปลาทู/ปลาซาบะ", detail: "30-50 บาท - โอเมก้า 3 ดีต่อสมอง" },
              { name: "ไข่ (ต้ม/คน/เจียว)", detail: "15-20 บาท/10 ฟอง - โคลีน ช่วยจดจำ" },
              { name: "ถั่วเหลือง/เต้าหู้", detail: "15-25 บาท - เลซิติน บำรุงสมอง" },
              { name: "ถั่วเมล็ดแห้ง", detail: "30-50 บาท - โปรตีน วิตามินบี" }
            ]
          },
          lunch_box: {
            title: "🎒 กล่องข้าวเด็กโรงเรียน",
            items: [
              { name: "ข้าวกล่องบ้าน", detail: "30-40 บาท - ปลอดภัย ประหยัด ควบคุมคุณค่า" },
              { name: "ขนมปังแซนด์วิช", detail: "25-35 บาท - ไข่ + ผัก + แฮม" },
              { name: "ข้าวห่อไข่", detail: "25-30 บาท - กินง่าย พกสะดวก" },
              { name: "ผลไม้ + นม", detail: "20-30 บาท - ของว่างดีมีประโยชน์" }
            ]
          },
          energy_snacks: {
            title: "⚡ ของว่างเพิ่มพลังงาน",
            items: [
              { name: "ข้าวเกรียบปลา", detail: "15-20 บาท - กรุบกรอบ มีโปรตีน" },
              { name: "ข้าวโพดต้ม", detail: "10-15 บาท - ใยอาหาร พลังงาน" },
              { name: "ปอเปี๊ยะสด", detail: "10-15 บาท/ชิ้น - ผัก กุ้ง ย่อยง่าย" },
              { name: "วุ้นเย็น", detail: "10 บาท - หวานน้อย เย็นชื่นใจ" }
            ]
          },
          budget_tips: {
            title: "💰 เคล็ดลับประหยัด",
            items: [
              { name: "ซื้อตามฤดูกาล", detail: "ผัก ผลไม้ จะถูก สด คุณภาพดี" },
              { name: "ทำเองที่บ้าน", detail: "ถูกกว่า ปลอดภัยกว่า ครบ 5 หมู่" },
              { name: "ซื้อจากตลาดสด", detail: "ถูกกว่าห้าง สดใหม่" },
              { name: "หมุนเวียนเมนู", detail: "วางแผนรายสัปดาห์ ไม่ซื้อซ้ำซ้อน" }
            ]
          }
        }
      }
    };

    const activityGuideData = {
      "0-6": {
        title: "กิจกรรมแนะนำ 0-6 เดือน",
        description: "เน้นกระตุ้นประสาทสัมผัสและการพัฒนากล้ามเนื้อ",
        activities: [
          {
            icon: "👶",
            title: "Tummy Time (นอนคว่ำ)",
            description: "ให้ลูกนอนคว่ำบนพื้นเรียบ 3-5 นาทีต่อครั้ง วันละ 2-3 ครั้ง วางของเล่นสีสันสดใสไว้ข้างหน้าให้ลูกยกหัวมอง",
            benefits: "💪 เสริมสร้างกล้ามเนื้อคอและหลัง | 🧠 กระตุ้นการยกหัวและพลิกตัว"
          },
          {
            icon: "🎵",
            title: "ร้องเพลง + พูดคุยกับลูก",
            description: "ร้องเพลงกล่อม พูดคุยเรื่องราวในชีวิตประจำวัน ใช้น้ำเสียงต่างๆ เพื่อดึงความสนใจ มองตาลูกขณะพูด",
            benefits: "👂 พัฒนาการได้ยินและจดจำเสียง | 💬 กระตุ้นพัฒนาการด้านภาษา"
          },
          {
            icon: "🖐️",
            title: "นวดและจับมือลูก",
            description: "นวดแขน ขา มือ เท้าของลูกเบาๆ ให้ลูกจับนิ้วของคุณ ช่วยกระตุ้นการเคลื่อนไหว",
            benefits: "🤗 สร้างความผูกพัน | ✋ กระตุ้นการรับรู้ทางผิวหนัง"
          },
          {
            icon: "📱",
            title: "มือถือเด็ก (Mobile)",
            description: "แขวนมือถือเด็กที่มีสีสันสดใสเหนือเตียง ระยะห่าง 20-30 ซม. ให้ลูกมองและเอื้อมมือจับ",
            benefits: "👀 กระตุ้นสายตา | 🎯 ฝึกการติดตามวัตถุ"
          },
          {
            icon: "🔄",
            title: "เล่นกระจก",
            description: "ให้ลูกมองตัวเองในกระจก ยิ้มให้ ทำหน้าต่างๆ ให้ลูกสังเกต",
            benefits: "😊 พัฒนาความรู้จักตัวเอง | 📸 กระตุ้นการรับรู้ใบหน้า"
          },
          {
            icon: "🎨",
            title: "บัตรภาพขาวดำ",
            description: "ใช้บัตรลายขาวดำหรือสีคมชัดให้ลูกดู เนื่องจากเด็กทารกมองเห็นความตัดกันของสีได้ชัดเจน",
            benefits: "👁️ กระตุ้นการมองเห็น | 🧠 พัฒนาสมอง"
          }
        ]
      },
      "6-12": {
        title: "กิจกรรมแนะนำ 6-12 เดือน",
        description: "เน้นพัฒนาทักษะการเคลื่อนไหว การสำรวจ และปฏิสัมพันธ์",
        activities: [
          {
            icon: "🧸",
            title: "เล่นซ่อนแอบ (Peek-a-boo)",
            description: "ใช้ผ้าหรือมือปิดหน้า แล้วค่อยเปิดออกพร้อมพูดว่า 'จ๊ะเอ๋!' ซ้ำๆ ให้ลูกเรียนรู้ว่าสิ่งที่หายไปยังอยู่",
            benefits: "🤔 สอนแนวคิด Object Permanence | 😄 สร้างความสนุกสนาน"
          },
          {
            icon: "📦",
            title: "เล่นกล่องใส่ของ",
            description: "ใช้กล่องและของเล่นขนาดใหญ่ ให้ลูกฝึกหยิบใส่ กล่องและเทออก พัฒนาการประสานงานมือตา",
            benefits: "🖐️ ฝึกทักษะมือ | 🧩 เรียนรู้เชิงสาเหตุและผล"
          },
          {
            icon: "📚",
            title: "อ่านหนังสือภาพ",
            description: "เลือกหนังสือผ้าหรือกระดาษแข็งที่มีภาพสีสันสดใส อ่านให้ลูกฟัง ชี้ภาพพร้อมบอกชื่อ",
            benefits: "📖 กระตุ้นความสนใจในหนังสือ | 🗣️ พัฒนาคำศัพท์"
          },
          {
            icon: "🎶",
            title: "เล่นดนตรีและเต้นจังหวะ",
            description: "เปิดเพลงให้ลูกฟัง ตบมือตามจังหวะ หรือถือมือลูกเต้นไปด้วย ใช้กลองของเล่นหรือกระป๋องเคาะเสียง",
            benefits: "🎵 พัฒนาจังหวะและประสาทสัมผัส | 💃 ฝึกการเคลื่อนไหว"
          },
          {
            icon: "🚼",
            title: "ฝึกคลาน + เดิน",
            description: "วางของเล่นให้ห่างออกไปเพื่อกระตุ้นให้ลูกคลานไปหยิบ จูงมือให้ลูกยืนและเดิน",
            benefits: "🦵 พัฒนากล้ามเนื้อขา | ⚖️ ฝึกทรงตัว"
          },
          {
            icon: "🧩",
            title: "เล่นของเล่นเรียงซ้อน",
            description: "ใช้บล็อกหรือแก้วสีสันต่างๆ ให้ลูกฝึกเรียงซ้อน เริ่มจาก 2-3 ชิ้น",
            benefits: "👁️‍🗨️ ฝึกสมาธิ | 🏗️ เรียนรู้เรื่องขนาดและน้ำหนัก"
          }
        ]
      },
      "12-24": {
        title: "กิจกรรมแนะนำ 1-2 ปี",
        description: "เน้นสร้างความมั่นใจในการเคลื่อนไหวและการสื่อสาร",
        activities: [
          {
            icon: "🏃",
            title: "เล่นไล่จับ + วิ่ง",
            description: "เล่นไล่จับในบ้านหรือสวน วิ่งช้าๆ ให้ลูกไล่ตาม หรือให้ลูกหนีแล้วไล่ตาม ช่วยพัฒนาการวิ่งและทรงตัว",
            benefits: "🏃‍♀️ พัฒนาทักษะการวิ่ง | 😆 สร้างความสนุก ลดพลังงานส่วนเกิน"
          },
          {
            icon: "⚽",
            title: "เล่นลูกบอล",
            description: "กลิ้ง เตะ และโยนลูกบอลไปมาระหว่างกัน เริ่มจากลูกบอลขนาดใหญ่ก่อน",
            benefits: "🎯 พัฒนาทักษะการโยนและจับ | 👀 ฝึกสายตาและการประสานงาน"
          },
          {
            icon: "🎨",
            title: "วาดภาพ + ระบายสี",
            description: "ให้ลูกใช้สีเทียน ดินสอสี หรือสีน้ำวาดเขี่ยๆ บนกระดาษขนาดใหญ่ ไม่ต้องห่วงความสวยงาม",
            benefits: "✏️ ฝึกกล้ามเนื้อมือ | 🌈 กระตุ้นความคิดสร้างสรรค์"
          },
          {
            icon: "🧱",
            title: "เล่นบล็อกต่อ",
            description: "ใช้บล็อกขนาดใหญ่ให้ลูกต่อเป็นตึกหรือรูปทรงต่างๆ สนับสนุนจินตนาการของลูก",
            benefits: "🏗️ พัฒนาทักษะเชิงพื้นที่ | 🤲 ฝึกการใช้มือทั้งสองข้าง"
          },
          {
            icon: "🧑‍🍳",
            title: "เล่นบทบาทสมมติ",
            description: "เล่นทำอาหาร เล่นหมอ เล่นซื้อของ ใช้ของเล่นหรือของจริง (ปลอดภัย) ให้ลูกจินตนาการตามบทบาท",
            benefits: "🎭 พัฒนาจินตนาการ | 👥 เรียนรู้บทบาทสังคม"
          },
          {
            icon: "🎤",
            title: "ร้องเพลงประกอบท่าทาง",
            description: "ร้องเพลงเด็กที่มีท่าทางประกอบ เช่น 'หัวไหล่หัวเข่าฝ่าเท้า' 'จับปูดำ' ให้ลูกทำตาม",
            benefits: "🎵 จดจำคำศัพท์ | 💃 พัฒนาการเคลื่อนไหว"
          }
        ]
      },
      "24-36": {
        title: "กิจกรรมแนะนำ 2-3 ปี",
        description: "เน้นการเรียนรู้ผ่านการเล่นและพัฒนาทักษะทางสังคม",
        activities: [
          {
            icon: "🧩",
            title: "ต่อจิ๊กซอว์",
            description: "เริ่มจากจิ๊กซอว์ 4-6 ชิ้น แล้วค่อยเพิ่มความซับซ้อน เลือกภาพที่ลูกชอบหรือคุ้นเคย",
            benefits: "🧠 ฝึกแก้ปัญหา | 🎯 พัฒนาสมาธิและความอดทน"
          },
          {
            icon: "✂️",
            title: "ตัด-ปะ-ติด",
            description: "ให้ลูกใช้กรรไกรปลายมนตัดกระดาษ แล้วนำมาติดเป็นรูปทรง ใช้กาวแท่งปลอดภัย",
            benefits: "✋ พัฒนากล้ามเนื้อมือละเอียด | 🎨 ส่งเสริมความคิดสร้างสรรค์"
          },
          {
            icon: "🔢",
            title: "นับเลข + รู้จักสี",
            description: "นับของเล่น ลูกบอล หรือผลไม้ จัดกลุ่มตามสี เรียนรู้แนวคิดมาก-น้อย",
            benefits: "🔢 พัฒนาทักษะคณิตศาสตร์เบื้องต้น | 🌈 จำแนกสีและรูปร่าง"
          },
          {
            icon: "👫",
            title: "เล่นกับเด็กคนอื่น",
            description: "พาลูกไปสนามเด็กเล่น หรือนัดเพื่อนมาเล่นที่บ้าน ให้ลูกฝึกแบ่งปันและรอคอย",
            benefits: "🤝 พัฒนาทักษะทางสังคม | 😊 เรียนรู้การแบ่งปันและรอคิว"
          },
          {
            icon: "🚲",
            title: "ปั่นจักรยาน 3 ล้อ",
            description: "ให้ลูกฝึกปั่นจักรยาน 3 ล้อในพื้นที่ปลอดภัย ส่งเสริมความมั่นใจและการทรงตัว",
            benefits: "🚴 พัฒนาทักษะการทรงตัว | 💪 เสริมสร้างกล้ามเนื้อขา"
          },
          {
            icon: "🌱",
            title: "ปลูกต้นไม้ + เล่นน้ำ",
            description: "ให้ลูกช่วยรดน้ำต้นไม้ ปลูกผักง่ายๆ เช่น ผักชี ต้นหอม หรือเล่นน้ำในอ่างเล็กๆ",
            benefits: "🌿 เรียนรู้ความรับผิดชอบ | 💧 กระตุ้นประสาทสัมผัส"
          }
        ]
      },
      "36-60": {
        title: "กิจกรรมแนะนำ 3-5 ปี",
        description: "เตรียมความพร้อมเข้าโรงเรียน พัฒนาทักษะการเรียนรู้และความเป็นอิสระ",
        activities: [
          {
            icon: "✍️",
            title: "ฝึกเขียนตัวอักษร",
            description: "ให้ลูกหัดขีดเส้น วงกลม และตัวอักษร ก-ฮ, A-Z เริ่มจากลากเส้นตามจุด แล้วค่อยเขียนเอง",
            benefits: "✏️ เตรียมพร้อมการเขียน | 🧠 ฝึกสมาธิและความละเอียด"
          },
          {
            icon: "📖",
            title: "อ่านหนังสือนิทานทุกวัน",
            description: "อ่านนิทานให้ลูกฟังก่อนนอน หรือตอนว่าง ให้ลูกช่วยเล่าเรื่อง ถามคำถามเกี่ยวกับเนื้อเรื่อง",
            benefits: "📚 สร้างนิสัยรักการอ่าน | 💬 พัฒนาทักษะภาษาและจินตนาการ"
          },
          {
            icon: "🎭",
            title: "แสดงละครบทบาท",
            description: "ให้ลูกแสดงเป็นตัวละครในนิทาน สวมบทบาทครู หมอ ตำรวจ หรือสร้างเรื่องราวขึ้นเอง",
            benefits: "🎬 ส่งเสริมจินตนาการ | 🗣️ พัฒนาทักษะการพูด"
          },
          {
            icon: "🔬",
            title: "ทดลองวิทยาศาสตร์ง่ายๆ",
            description: "ทำไอศกรีม ปลูกผัก ทำภูเขาไฟจำลอง หรือทดลองของลอยน้ำ-จม ให้ลูกสังเกตและสรุป",
            benefits: "🧪 กระตุ้นความอยากรู้ | 🤔 ฝึกทักษะการสังเกตและแก้ปัญหา"
          },
          {
            icon: "🎮",
            title: "เกมการศึกษา",
            description: "เล่นเกมจับคู่ภาพ เกมหาความแตกต่าง เกมจำลำดับ หรือเกมบอร์ดง่ายๆ",
            benefits: "🧠 พัฒนาความจำและสมาธิ | 🎯 เรียนรู้กฎกติกา"
          },
          {
            icon: "🏀",
            title: "กีฬาและการเคลื่อนไหว",
            description: "ให้ลูกเล่นกีฬาเบื้องต้น เช่น วิ่ง กระโดดเชือก ว่ายน้ำ หรือฝึกยิมนาสติกง่ายๆ",
            benefits: "💪 พัฒนาร่างกายแข็งแรง | ⚽ ฝึกการทำงานเป็นทีม"
          },
          {
            icon: "🎒",
            title: "ฝึกความเป็นอิสระ",
            description: "ให้ลูกแต่งตัวเอง จัดกระเป๋าเอง เก็บของเล่น ช่วยทำงานบ้านง่ายๆ เช่น เช็ดโต๊ะ",
            benefits: "🙋 สร้างความมั่นใจ | 🏠 เรียนรู้ความรับผิดชอบ"
          }
        ]
      }
    };

    const vaccineData = {
      "birth": {
        title: "วัคซีนแรกเกิด",
        vaccines: [
          {
            name: "วัคซีนวัณโรค (BCG)",
            description: "ป้องกันวัณโรคที่รุนแรง เช่น วัณโรคสมอง ฉีดบริเวณแขนซ้ายด้านนอก จะเกิดแผลเป็นตุ่มเล็กๆ เป็นปกติ"
          },
          {
            name: "วัคซีนตับอักเสบบี ครั้งที่ 1 (HB1)",
            description: "ป้องกันโรคตับอักเสบบีที่อาจนำไปสู่มะเร็งตับ ควรฉีดภายใน 24 ชั่วโมงหลังคลอด"
          }
        ]
      },
      "2-months": {
        title: "วัคซีน 2 เดือน",
        vaccines: [
          {
            name: "วัคซีนตับอักเสบบี ครั้งที่ 2 (HB2)",
            description: "เสริมภูมิคุ้มกันต่อโรคตับอักเสบบี"
          },
          {
            name: "วัคซีนรวม 5 โรค ครั้งที่ 1 (DTP-HB-Hib1)",
            description: "ป้องกัน คอตีบ บาดทะยัก ไอกรน ตับอักเสบบี และโรคติดเชื้อ HIB"
          },
          {
            name: "วัคซีนโปลิโอ ครั้งที่ 1 (OPV1/IPV1)",
            description: "ป้องกันโรคโปลิโอที่ทำให้เกิดอัมพาต"
          },
          {
            name: "วัคซีนป้องกันโรคปอดอักเสบ ครั้งที่ 1 (PCV1)",
            description: "ป้องกันโรคติดเชื้อนิวโมคอคคัส เช่น ปอดบวม เยื่อหุ้มสมองอักเสบ"
          },
          {
            name: "วัคซีนโรต้าไวรัส ครั้งที่ 1 (RV1)",
            description: "ป้องกันโรคท้องเสียจากเชื้อโรต้า ฉีดก่อนอายุ 14 สัปดาห์ 6 วัน"
          }
        ]
      },
      "4-months": {
        title: "วัคซีน 4 เดือน",
        vaccines: [
          {
            name: "วัคซีนรวม 5 โรค ครั้งที่ 2 (DTP-HB-Hib2)",
            description: "เสริมภูมิคุ้มกันต่อ คอตีบ บาดทะยัก ไอกรน ตับอักเสบบี และโรค HIB"
          },
          {
            name: "วัคซีนโปลิโอ ครั้งที่ 2 (OPV2/IPV2)",
            description: "เสริมภูมิคุ้มกันต่อโรคโปลิโอ"
          },
          {
            name: "วัคซีนป้องกันโรคปอดอักเสบ ครั้งที่ 2 (PCV2)",
            description: "เสริมภูมิคุ้มกันต่อโรคติดเชื้อนิวโมคอคคัส"
          },
          {
            name: "วัคซีนโรต้าไวรัส ครั้งที่ 2 (RV2)",
            description: "เสริมภูมิคุ้มกันต่อโรคท้องเสียจากเชื้อโรต้า"
          }
        ]
      },
      "6-months": {
        title: "วัคซีน 6 เดือน",
        vaccines: [
          {
            name: "วัคซีนรวม 5 โรค ครั้งที่ 3 (DTP-HB-Hib3)",
            description: "ครบวงจรป้องกัน คอตีบ บาดทะยัก ไอกรน ตับอักเสบบี และโรค HIB"
          },
          {
            name: "วัคซีนโปลิโอ ครั้งที่ 3 (OPV3/IPV3)",
            description: "ครบวงจรป้องกันโรคโปลิโอ"
          },
          {
            name: "วัคซีนป้องกันโรคปอดอักเสบ ครั้งที่ 3 (PCV3)",
            description: "ครบวงจรป้องกันโรคติดเชื้อนิวโมคอคคัส"
          }
        ]
      },
      "9-months": {
        title: "วัคซีน 9 เดือน",
        vaccines: [
          {
            name: "วัคซีนหัด หัดเยอรมัน คางทูม ครั้งที่ 1 (MMR1)",
            description: "ป้องกันโรคหัด หัดเยอรมัน และคางทูม ซึ่งอาจทำให้เกิดภาวะแทรกซ้อนรุนแรงได้"
          },
          {
            name: "วัคซีนไข้สมองอักเสบเจอี (JE)",
            description: "ป้องกันโรคไข้สมองอักเสบเจแปนนีสที่เกิดจากยุงลาย (เฉพาะพื้นที่เสี่ยง)"
          }
        ]
      },
      "12-months": {
        title: "วัคซีน 12 เดือน (1 ปี)",
        vaccines: [
          {
            name: "วัคซีนไข้สมองอักเสบเจอี ครั้งที่ 2 (JE2)",
            description: "เสริมภูมิคุ้มกันต่อโรคไข้สมองอักเสบเจแปนนีส (หากได้รับเข็มแรกที่ 9 เดือน)"
          }
        ]
      },
      "18-months": {
        title: "วัคซีน 18 เดือน (1.5 ปี)",
        vaccines: [
          {
            name: "วัคซีนรวม 3 โรค (DTP4)",
            description: "เสริมภูมิคุ้มกันต่อ คอตีบ บาดทะยัก และไอกรน"
          },
          {
            name: "วัคซีนโปลิโอ ครั้งที่ 4 (OPV4)",
            description: "เสริมภูมิคุ้มกันต่อโรคโปลิโอ"
          },
          {
            name: "วัคซีนหัด หัดเยอรมัน คางทูม ครั้งที่ 2 (MMR2)",
            description: "เสริมภูมิคุ้มกันต่อโรคหัด หัดเยอรมัน และคางทูม"
          }
        ]
      },
      "24-months": {
        title: "วัคซีน 2 ปี",
        vaccines: [
          {
            name: "วัคซีนไข้สมองอักเสบเจอี ครั้งที่ 3 (JE3)",
            description: "เสริมภูมิคุ้มกันต่อโรคไข้สมองอักเสบเจแปนนีส (เฉพาะพื้นที่เสี่ยง)"
          },
          {
            name: "วัคซีนตับอักเสบเอ ครั้งที่ 1 (HepA1)",
            description: "ป้องกันโรคตับอักเสบเอ ซึ่งติดต่อจากอาหารและน้ำที่ปนเปื้อน"
          }
        ]
      },
      "30-months": {
        title: "วัคซีน 2.5 ปี",
        vaccines: [
          {
            name: "วัคซีนตับอักเสบเอ ครั้งที่ 2 (HepA2)",
            description: "เสริมภูมิคุ้มกันต่อโรคตับอักเสบเอ ฉีดห่างจากเข็มแรก 6 เดือน"
          }
        ]
      },
      "4-years": {
        title: "วัคซีน 4 ปี",
        vaccines: [
          {
            name: "วัคซีนรวม 3 โรค (DTP5)",
            description: "เสริมภูมิคุ้มกันต่อ คอตีบ บาดทะยัก และไอกรน ก่อนเข้าโรงเรียน"
          },
          {
            name: "วัคซีนโปลิโอ ครั้งที่ 5 (OPV5)",
            description: "เสริมภูมิคุ้มกันต่อโรคโปลิโอ ก่อนเข้าโรงเรียน"
          }
        ]
      }
    };

    const dataHandler = {
      onDataChanged(data) {
        allData = data;
        updateDashboard();
        renderDevelopmentList();
        renderVaccineList();
        renderNutritionList();
        renderActivityList();
        updateChart();
      }
    };

    async function onConfigChange(config) {
      const appTitle = config.app_title || defaultConfig.app_title;
      const welcomeMessage = config.welcome_message || defaultConfig.welcome_message;
      const backgroundColor = config.background_color || defaultConfig.background_color;
      const surfaceColor = config.surface_color || defaultConfig.surface_color;
      const textColor = config.text_color || defaultConfig.text_color;
      const primaryActionColor = config.primary_action_color || defaultConfig.primary_action_color;
      const customFont = config.font_family || defaultConfig.font_family;
      const baseSize = config.font_size || defaultConfig.font_size;
      const baseFontStack = 'Comic Sans MS, Chalkboard SE, Marker Felt, cursive, sans-serif';

      document.getElementById('app-title').textContent = appTitle;
      document.getElementById('welcome-message').textContent = welcomeMessage;
      
      document.querySelector('.app-container').style.background = `linear-gradient(135deg, ${backgroundColor} 0%, ${primaryActionColor} 100%)`;
      document.body.style.background = `linear-gradient(135deg, ${backgroundColor} 0%, ${primaryActionColor} 100%)`;
      
      document.querySelectorAll('.tab-content, .checklist-item').forEach(el => {
        el.style.backgroundColor = surfaceColor;
      });
      
      document.querySelectorAll('.section-title, .checklist-title, label, .stat-label').forEach(el => {
        el.style.color = textColor;
      });
      
      document.querySelectorAll('.btn-primary, .stat-card, .category-card, .checklist-section').forEach(el => {
        el.style.background = `linear-gradient(135deg, ${backgroundColor} 0%, ${primaryActionColor} 100%)`;
      });

      document.getElementById('app-title').style.fontFamily = `${customFont}, ${baseFontStack}`;
      document.getElementById('welcome-message').style.fontFamily = `${customFont}, ${baseFontStack}`;
      document.querySelectorAll('.section-title').forEach(el => {
        el.style.fontFamily = `${customFont}, ${baseFontStack}`;
      });
      
      document.getElementById('app-title').style.fontSize = `${baseSize * 2.5}px`;
      document.getElementById('welcome-message').style.fontSize = `${baseSize * 1.1}px`;
      document.querySelectorAll('.section-title').forEach(el => {
        el.style.fontSize = `${baseSize * 1.75}px`;
      });
      document.querySelectorAll('.checklist-title, .category-name, .stat-label').forEach(el => {
        el.style.fontSize = `${baseSize * 1.1}px`;
      });
      document.querySelectorAll('label, .checklist-meta, input, select, textarea, button').forEach(el => {
        el.style.fontSize = `${baseSize}px`;
      });
    }

    async function initializeApp() {
      const initResult = await window.dataSdk.init(dataHandler);
      if (!initResult.isOk) {
        console.error("Failed to initialize data SDK");
        return;
      }

      if (window.elementSdk) {
        window.elementSdk.init({
          defaultConfig,
          onConfigChange,
          mapToCapabilities: (config) => ({
            recolorables: [
              {
                get: () => config.background_color || defaultConfig.background_color,
                set: (value) => {
                  config.background_color = value;
                  window.elementSdk.setConfig({ background_color: value });
                }
              },
              {
                get: () => config.surface_color || defaultConfig.surface_color,
                set: (value) => {
                  config.surface_color = value;
                  window.elementSdk.setConfig({ surface_color: value });
                }
              },
              {
                get: () => config.text_color || defaultConfig.text_color,
                set: (value) => {
                  config.text_color = value;
                  window.elementSdk.setConfig({ text_color: value });
                }
              },
              {
                get: () => config.primary_action_color || defaultConfig.primary_action_color,
                set: (value) => {
                  config.primary_action_color = value;
                  window.elementSdk.setConfig({ primary_action_color: value });
                }
              },
              {
                get: () => config.secondary_action_color || defaultConfig.secondary_action_color,
                set: (value) => {
                  config.secondary_action_color = value;
                  window.elementSdk.setConfig({ secondary_action_color: value });
                }
              }
            ],
            borderables: [],
            fontEditable: {
              get: () => config.font_family || defaultConfig.font_family,
              set: (value) => {
                config.font_family = value;
                window.elementSdk.setConfig({ font_family: value });
              }
            },
            fontSizeable: {
              get: () => config.font_size || defaultConfig.font_size,
              set: (value) => {
                config.font_size = value;
                window.elementSdk.setConfig({ font_size: value });
              }
            }
          }),
          mapToEditPanelValues: (config) => new Map([
            ["app_title", config.app_title || defaultConfig.app_title],
            ["welcome_message", config.welcome_message || defaultConfig.welcome_message]
          ])
        });
      }

      setupEventListeners();
      initializeChart();
      
      const today = new Date().toISOString().split('T')[0];
      document.querySelectorAll('input[type="date"]').forEach(input => {
        input.value = today;
      });
    }

    function setupEventListeners() {
      document.querySelectorAll('.tab-btn').forEach(btn => {
        btn.addEventListener('click', (e) => {
          const tabName = e.target.dataset.tab;
          switchTab(tabName);
        });
      });

      document.getElementById('development-form').addEventListener('submit', async (e) => {
        e.preventDefault();
        await handleDevelopmentSubmit(e);
      });

      document.getElementById('vaccine-form').addEventListener('submit', async (e) => {
        e.preventDefault();
        await handleVaccineSubmit(e);
      });

      document.getElementById('nutrition-form').addEventListener('submit', async (e) => {
        e.preventDefault();
        await handleNutritionSubmit(e);
      });

      document.getElementById('activity-form').addEventListener('submit', async (e) => {
        e.preventDefault();
        await handleActivitySubmit(e);
      });

      document.querySelectorAll('.category-card').forEach(card => {
        card.addEventListener('click', (e) => {
          const category = e.currentTarget.dataset.category;
          selectCategory(category);
        });
      });

      document.querySelectorAll('[data-age]').forEach(btn => {
        btn.addEventListener('click', (e) => {
          const ageRange = e.target.dataset.age;
          showMilestoneChecklist(ageRange);
        });
      });

      document.getElementById('close-checklist').addEventListener('click', () => {
        document.getElementById('milestone-checklist-container').style.display = 'none';
      });

      document.querySelectorAll('[data-vaccine-age]').forEach(btn => {
        btn.addEventListener('click', (e) => {
          const ageRange = e.target.dataset.vaccineAge;
          showVaccineChecklist(ageRange);
        });
      });

      document.getElementById('close-vaccine-checklist').addEventListener('click', () => {
        document.getElementById('vaccine-checklist-container').style.display = 'none';
      });

      document.querySelectorAll('[data-nutrition-age]').forEach(btn => {
        btn.addEventListener('click', (e) => {
          const ageRange = e.target.dataset.nutritionAge;
          showNutritionGuide(ageRange);
        });
      });

      document.getElementById('close-nutrition-guide').addEventListener('click', () => {
        document.getElementById('nutrition-guide-container').style.display = 'none';
      });

      document.querySelectorAll('[data-activity-age]').forEach(btn => {
        btn.addEventListener('click', (e) => {
          const ageRange = e.target.dataset.activityAge;
          showActivityGuide(ageRange);
        });
      });

      document.getElementById('close-activity-guide').addEventListener('click', () => {
        document.getElementById('activity-guide-container').style.display = 'none';
      });
    }

    function showMilestoneChecklist(ageRange) {
      const container = document.getElementById('milestone-checklist-container');
      const content = document.getElementById('milestone-checklist-content');
      const title = document.getElementById('checklist-age-title');
      
      const data = milestoneData[ageRange];
      
      if (!data) return;
      
      title.textContent = data.title;
      
      let html = '';
      
      const categoryInfo = {
        physical: { icon: '🏃', name: 'พัฒนาการด้านร่างกาย' },
        cognitive: { icon: '🧩', name: 'พัฒนาการด้านสติปัญญา' },
        social: { icon: '👥', name: 'พัฒนาการด้านสังคม-อารมณ์' },
        language: { icon: '💬', name: 'พัฒนาการด้านภาษา' }
      };
      
      for (const [category, items] of Object.entries(data.categories)) {
        const info = categoryInfo[category];
        html += `
          <div class="milestone-checklist-group">
            <h4>${info.icon} ${info.name}</h4>
            ${items.map(item => `
              <div class="milestone-checklist-item">
                <p>✓ ${escapeHtml(item)}</p>
              </div>
            `).join('')}
          </div>
        `;
      }
      
      content.innerHTML = html;
      container.style.display = 'block';
      
      container.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
    }

    function showVaccineChecklist(ageRange) {
      const container = document.getElementById('vaccine-checklist-container');
      const content = document.getElementById('vaccine-checklist-content');
      const title = document.getElementById('vaccine-checklist-age-title');
      
      const data = vaccineData[ageRange];
      
      if (!data) return;
      
      title.textContent = data.title;
      
      let html = '<div class="milestone-checklist-group">';
      html += `<h4>💉 ${data.title}</h4>`;
      
      data.vaccines.forEach(vaccine => {
        html += `
          <div class="vaccine-checklist-item">
            <div class="vaccine-checklist-item-title">${escapeHtml(vaccine.name)}</div>
            <div class="vaccine-checklist-item-desc">${escapeHtml(vaccine.description)}</div>
          </div>
        `;
      });
      
      html += '</div>';
      
      content.innerHTML = html;
      container.style.display = 'block';
      
      container.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
    }

    function showNutritionGuide(ageRange) {
      const container = document.getElementById('nutrition-guide-container');
      const content = document.getElementById('nutrition-guide-content');
      const title = document.getElementById('nutrition-guide-age-title');
      
      const data = nutritionGuideData[ageRange];
      
      if (!data) return;
      
      title.textContent = data.title;
      
      let html = '<div class="milestone-checklist-group">';
      html += `<h4 style="font-size: 1.3rem; margin-bottom: 0.5rem;">${data.title}</h4>`;
      html += `<p style="color: #666; margin-bottom: 1.5rem; line-height: 1.6;">${escapeHtml(data.description)}</p>`;
      
      for (const [categoryKey, category] of Object.entries(data.categories)) {
        html += `<div style="margin-bottom: 2rem;">`;
        html += `<h5 style="color: #667eea; font-size: 1.15rem; margin-bottom: 1rem;">${category.title}</h5>`;
        
        category.items.forEach(item => {
          html += `
            <div class="vaccine-checklist-item" style="border-left-color: #10b981;">
              <div class="vaccine-checklist-item-title" style="color: #10b981;">${escapeHtml(item.name)}</div>
              <div class="vaccine-checklist-item-desc">${escapeHtml(item.detail)}</div>
            </div>
          `;
        });
        
        html += `</div>`;
      }
      
      html += '</div>';
      
      content.innerHTML = html;
      container.style.display = 'block';
      
      container.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
    }

    function showActivityGuide(ageRange) {
      const container = document.getElementById('activity-guide-container');
      const content = document.getElementById('activity-guide-content');
      const title = document.getElementById('activity-guide-age-title');
      
      const data = activityGuideData[ageRange];
      
      if (!data) return;
      
      title.textContent = data.title;
      
      let html = '<div class="milestone-checklist-group">';
      html += `<h4 style="font-size: 1.3rem; margin-bottom: 0.5rem;">${data.title}</h4>`;
      html += `<p style="color: #666; margin-bottom: 1.5rem; line-height: 1.6;">${escapeHtml(data.description)}</p>`;
      
      data.activities.forEach(activity => {
        html += `
          <div class="activity-card">
            <div class="activity-card-title">${activity.icon} ${escapeHtml(activity.title)}</div>
            <div class="activity-card-desc">${escapeHtml(activity.description)}</div>
            <div class="activity-card-benefits">${escapeHtml(activity.benefits)}</div>
          </div>
        `;
      });
      
      html += '</div>';
      
      content.innerHTML = html;
      container.style.display = 'block';
      
      container.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
    }

    function switchTab(tabName) {
      document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
      document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));
      
      document.querySelector(`[data-tab="${tabName}"]`).classList.add('active');
      document.getElementById(tabName).classList.add('active');
    }

    function selectCategory(category) {
      selectedCategory = category;
      document.querySelectorAll('.category-card').forEach(card => {
        card.classList.remove('selected');
      });
      document.querySelector(`[data-category="${category}"]`).classList.add('selected');
      renderDevelopmentList();
    }

    async function handleDevelopmentSubmit(e) {
      const submitBtn = e.target.querySelector('button[type="submit"]');
      const btnText = submitBtn.querySelector('.btn-text');
      const originalText = btnText.textContent;
      
      if (allData.filter(d => d.type === 'development').length >= 999) {
        showMessage('ถึงขีดจำกัด 999 รายการแล้ว กรุณาลบรายการเก่าก่อน', 'error');
        return;
      }

      btnText.innerHTML = '<span class="loading-spinner"></span> กำลังบันทึก...';
      submitBtn.disabled = true;

      const formData = {
        id: Date.now().toString(),
        type: 'development',
        child_name: document.getElementById('dev-child-name').value,
        title: document.getElementById('dev-title').value,
        category: document.getElementById('dev-category').value,
        age_months: parseInt(document.getElementById('dev-age').value),
        date: document.getElementById('dev-date').value,
        notes: document.getElementById('dev-notes').value,
        completed: false,
        created_at: new Date().toISOString()
      };

      const result = await window.dataSdk.create(formData);
      
      if (result.isOk) {
        e.target.reset();
        const today = new Date().toISOString().split('T')[0];
        document.getElementById('dev-date').value = today;
      } else {
        showMessage('เกิดข้อผิดพลาดในการบันทึก', 'error');
      }

      btnText.textContent = originalText;
      submitBtn.disabled = false;
    }

    async function handleVaccineSubmit(e) {
      const submitBtn = e.target.querySelector('button[type="submit"]');
      const btnText = submitBtn.querySelector('.btn-text');
      const originalText = btnText.textContent;
      
      if (allData.filter(d => d.type === 'vaccine').length >= 999) {
        showMessage('ถึงขีดจำกัด 999 รายการแล้ว กรุณาลบรายการเก่าก่อน', 'error');
        return;
      }

      btnText.innerHTML = '<span class="loading-spinner"></span> กำลังบันทึก...';
      submitBtn.disabled = true;

      const formData = {
        id: Date.now().toString(),
        type: 'vaccine',
        child_name: document.getElementById('vac-child-name').value,
        title: document.getElementById('vac-title').value,
        age_months: parseInt(document.getElementById('vac-age').value),
        date: document.getElementById('vac-date').value,
        notes: document.getElementById('vac-notes').value,
        completed: true,
        created_at: new Date().toISOString()
      };

      const result = await window.dataSdk.create(formData);
      
      if (result.isOk) {
        e.target.reset();
        const today = new Date().toISOString().split('T')[0];
        document.getElementById('vac-date').value = today;
      } else {
        showMessage('เกิดข้อผิดพลาดในการบันทึก', 'error');
      }

      btnText.textContent = originalText;
      submitBtn.disabled = false;
    }

    async function handleNutritionSubmit(e) {
      const submitBtn = e.target.querySelector('button[type="submit"]');
      const btnText = submitBtn.querySelector('.btn-text');
      const originalText = btnText.textContent;
      
      if (allData.filter(d => d.type === 'nutrition').length >= 999) {
        showMessage('ถึงขีดจำกัด 999 รายการแล้ว กรุณาลบรายการเก่าก่อน', 'error');
        return;
      }

      btnText.innerHTML = '<span class="loading-spinner"></span> กำลังบันทึก...';
      submitBtn.disabled = true;

      const formData = {
        id: Date.now().toString(),
        type: 'nutrition',
        child_name: document.getElementById('nutr-child-name').value,
        title: document.getElementById('nutr-title').value,
        category: document.getElementById('nutr-category').value,
        date: document.getElementById('nutr-date').value,
        notes: document.getElementById('nutr-notes').value,
        completed: true,
        created_at: new Date().toISOString()
      };

      const result = await window.dataSdk.create(formData);
      
      if (result.isOk) {
        e.target.reset();
        const today = new Date().toISOString().split('T')[0];
        document.getElementById('nutr-date').value = today;
      } else {
        showMessage('เกิดข้อผิดพลาดในการบันทึก', 'error');
      }

      btnText.textContent = originalText;
      submitBtn.disabled = false;
    }

    async function handleActivitySubmit(e) {
      const submitBtn = e.target.querySelector('button[type="submit"]');
      const btnText = submitBtn.querySelector('.btn-text');
      const originalText = btnText.textContent;
      
      if (allData.filter(d => d.type === 'activity').length >= 999) {
        showMessage('ถึงขีดจำกัด 999 รายการแล้ว กรุณาลบรายการเก่าก่อน', 'error');
        return;
      }

      btnText.innerHTML = '<span class="loading-spinner"></span> กำลังบันทึก...';
      submitBtn.disabled = true;

      const formData = {
        id: Date.now().toString(),
        type: 'activity',
        child_name: document.getElementById('act-child-name').value,
        title: document.getElementById('act-title').value,
        category: document.getElementById('act-category').value,
        date: document.getElementById('act-date').value,
        notes: document.getElementById('act-notes').value,
        completed: false,
        created_at: new Date().toISOString()
      };

      const result = await window.dataSdk.create(formData);
      
      if (result.isOk) {
        e.target.reset();
        const today = new Date().toISOString().split('T')[0];
        document.getElementById('act-date').value = today;
      } else {
        showMessage('เกิดข้อผิดพลาดในการบันทึก', 'error');
      }

      btnText.textContent = originalText;
      submitBtn.disabled = false;
    }

    function updateDashboard() {
      const developments = allData.filter(d => d.type === 'development');
      const vaccines = allData.filter(d => d.type === 'vaccine');
      const activities = allData.filter(d => d.type === 'activity');
      
      document.getElementById('total-milestones').textContent = developments.length;
      document.getElementById('completed-milestones').textContent = developments.filter(d => d.completed).length;
      document.getElementById('total-vaccines').textContent = vaccines.length;
      document.getElementById('total-activities').textContent = activities.length;
    }

    function renderDevelopmentList() {
      const container = document.getElementById('development-list');
      let items = allData.filter(d => d.type === 'development');
      
      if (selectedCategory !== 'all') {
        items = items.filter(d => d.category === selectedCategory);
      }
      
      items.sort((a, b) => new Date(b.date) - new Date(a.date));

      if (items.length === 0) {
        container.innerHTML = `
          <div class="empty-state">
            <div class="empty-state-icon">📝</div>
            <p>ยังไม่มีข้อมูลพัฒนาการ</p>
          </div>
        `;
        return;
      }

      container.innerHTML = items.map(item => `
        <div class="checklist-item ${item.completed ? 'completed' : ''}">
          <div class="checklist-header">
            <div class="checkbox-wrapper">
              <input type="checkbox" ${item.completed ? 'checked' : ''} data-id="${item.__backendId}">
            </div>
            <div class="checklist-content">
              <div class="checklist-title">${escapeHtml(item.title)}</div>
              <div class="checklist-meta">
                <span>👶 ${escapeHtml(item.child_name)}</span>
                <span>📅 ${formatDate(item.date)}</span>
                <span>🎂 ${item.age_months} เดือน</span>
                <span>${getCategoryEmoji(item.category)} ${getCategoryLabel(item.category)}</span>
              </div>
              ${item.notes ? `<div class="checklist-notes">📌 ${escapeHtml(item.notes)}</div>` : ''}
              <div class="checklist-actions">
                <button class="btn-small btn-delete" data-id="${item.__backendId}">ลบ</button>
              </div>
            </div>
          </div>
        </div>
      `).join('');

      container.querySelectorAll('input[type="checkbox"]').forEach(checkbox => {
        checkbox.addEventListener('change', async (e) => {
          const id = e.target.dataset.id;
          const item = allData.find(d => d.__backendId === id);
          if (item) {
            item.completed = e.target.checked;
            await window.dataSdk.update(item);
          }
        });
      });

      container.querySelectorAll('.btn-delete').forEach(btn => {
        btn.addEventListener('click', async (e) => {
          const id = e.target.dataset.id;
          await handleDelete(id);
        });
      });
    }

    function renderVaccineList() {
      const container = document.getElementById('vaccine-list');
      const items = allData.filter(d => d.type === 'vaccine').sort((a, b) => new Date(b.date) - new Date(a.date));

      if (items.length === 0) {
        container.innerHTML = `
          <div class="empty-state">
            <div class="empty-state-icon">💉</div>
            <p>ยังไม่มีข้อมูลวัคซีน</p>
          </div>
        `;
        return;
      }

      container.innerHTML = items.map(item => `
        <div class="checklist-item completed">
          <div class="checklist-header">
            <div class="checkbox-wrapper">
              <input type="checkbox" checked disabled>
            </div>
            <div class="checklist-content">
              <div class="checklist-title">${escapeHtml(item.title)}</div>
              <div class="checklist-meta">
                <span>👶 ${escapeHtml(item.child_name)}</span>
                <span>📅 ${formatDate(item.date)}</span>
                <span>🎂 ${item.age_months} เดือน</span>
              </div>
              ${item.notes ? `<div class="checklist-notes">📌 ${escapeHtml(item.notes)}</div>` : ''}
              <div class="checklist-actions">
                <button class="btn-small btn-delete" data-id="${item.__backendId}">ลบ</button>
              </div>
            </div>
          </div>
        </div>
      `).join('');

      container.querySelectorAll('.btn-delete').forEach(btn => {
        btn.addEventListener('click', async (e) => {
          const id = e.target.dataset.id;
          await handleDelete(id);
        });
      });
    }

    function renderNutritionList() {
      const container = document.getElementById('nutrition-list');
      const items = allData.filter(d => d.type === 'nutrition').sort((a, b) => new Date(b.date) - new Date(a.date));

      if (items.length === 0) {
        container.innerHTML = `
          <div class="empty-state">
            <div class="empty-state-icon">🍎</div>
            <p>ยังไม่มีข้อมูลโภชนาการ</p>
          </div>
        `;
        return;
      }

      container.innerHTML = items.map(item => `
        <div class="checklist-item completed">
          <div class="checklist-header">
            <div class="checkbox-wrapper">
              <input type="checkbox" checked disabled>
            </div>
            <div class="checklist-content">
              <div class="checklist-title">${escapeHtml(item.title)}</div>
              <div class="checklist-meta">
                <span>👶 ${escapeHtml(item.child_name)}</span>
                <span>📅 ${formatDate(item.date)}</span>
                <span>${getNutritionEmoji(item.category)} ${getNutritionLabel(item.category)}</span>
              </div>
              ${item.notes ? `<div class="checklist-notes">📌 ${escapeHtml(item.notes)}</div>` : ''}
              <div class="checklist-actions">
                <button class="btn-small btn-delete" data-id="${item.__backendId}">ลบ</button>
              </div>
            </div>
          </div>
        </div>
      `).join('');

      container.querySelectorAll('.btn-delete').forEach(btn => {
        btn.addEventListener('click', async (e) => {
          const id = e.target.dataset.id;
          await handleDelete(id);
        });
      });
    }

    function renderActivityList() {
      const container = document.getElementById('activity-list');
      const items = allData.filter(d => d.type === 'activity').sort((a, b) => new Date(b.date) - new Date(a.date));

      if (items.length === 0) {
        container.innerHTML = `
          <div class="empty-state">
            <div class="empty-state-icon">🎨</div>
            <p>ยังไม่มีข้อมูลกิจกรรม</p>
          </div>
        `;
        return;
      }

      container.innerHTML = items.map(item => `
        <div class="checklist-item ${item.completed ? 'completed' : ''}">
          <div class="checklist-header">
            <div class="checkbox-wrapper">
              <input type="checkbox" ${item.completed ? 'checked' : ''} data-id="${item.__backendId}">
            </div>
            <div class="checklist-content">
              <div class="checklist-title">${escapeHtml(item.title)}</div>
              <div class="checklist-meta">
                <span>👶 ${escapeHtml(item.child_name)}</span>
                <span>📅 ${formatDate(item.date)}</span>
                <span>${getActivityEmoji(item.category)} ${getActivityLabel(item.category)}</span>
              </div>
              ${item.notes ? `<div class="checklist-notes">📌 ${escapeHtml(item.notes)}</div>` : ''}
              <div class="checklist-actions">
                <button class="btn-small btn-delete" data-id="${item.__backendId}">ลบ</button>
              </div>
            </div>
          </div>
        </div>
      `).join('');

      container.querySelectorAll('input[type="checkbox"]').forEach(checkbox => {
        checkbox.addEventListener('change', async (e) => {
          const id = e.target.dataset.id;
          const item = allData.find(d => d.__backendId === id);
          if (item) {
            item.completed = e.target.checked;
            await window.dataSdk.update(item);
          }
        });
      });

      container.querySelectorAll('.btn-delete').forEach(btn => {
        btn.addEventListener('click', async (e) => {
          const id = e.target.dataset.id;
          await handleDelete(id);
        });
      });
    }

    async function handleDelete(id) {
      const item = allData.find(d => d.__backendId === id);
      if (item) {
        await window.dataSdk.delete(item);
      }
    }

    function initializeChart() {
      const ctx = document.getElementById('progressChart');
      progressChart = new Chart(ctx, {
        type: 'line',
        data: {
          labels: [],
          datasets: [{
            label: 'พัฒนาการที่ผ่านแล้ว',
            data: [],
            borderColor: '#667eea',
            backgroundColor: 'rgba(102, 126, 234, 0.1)',
            tension: 0.4,
            fill: true
          }]
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          plugins: {
            legend: {
              display: true,
              position: 'top'
            }
          },
          scales: {
            y: {
              beginAtZero: true,
              ticks: {
                stepSize: 1
              }
            }
          }
        }
      });
    }

    function updateChart() {
      const developments = allData.filter(d => d.type === 'development');
      const monthlyData = {};

      developments.forEach(item => {
        const month = item.age_months;
        if (!monthlyData[month]) {
          monthlyData[month] = 0;
        }
        if (item.completed) {
          monthlyData[month]++;
        }
      });

      const sortedMonths = Object.keys(monthlyData).sort((a, b) => parseInt(a) - parseInt(b));
      const labels = sortedMonths.map(m => `${m} เดือน`);
      const data = sortedMonths.map(m => monthlyData[m]);

      progressChart.data.labels = labels;
      progressChart.data.datasets[0].data = data;
      progressChart.update();
    }

    function getCategoryEmoji(category) {
      const emojis = {
        physical: '🏃',
        cognitive: '🧩',
        social: '👥',
        language: '💬'
      };
      return emojis[category] || '📋';
    }

    function getCategoryLabel(category) {
      const labels = {
        physical: 'ร่างกาย',
        cognitive: 'สติปัญญา',
        social: 'สังคม',
        language: 'ภาษา'
      };
      return labels[category] || category;
    }

    function getNutritionEmoji(category) {
      const emojis = {
        milk: '🍼',
        food: '🍽️',
        supplement: '💊'
      };
      return emojis[category] || '🍎';
    }

    function getNutritionLabel(category) {
      const labels = {
        milk: 'นม',
        food: 'อาหาร',
        supplement: 'วิตามิน/แร่ธาตุ'
      };
      return labels[category] || category;
    }

    function getActivityEmoji(category) {
      const emojis = {
        learning: '📚',
        play: '🎮',
        social: '👫',
        preparation: '🎒'
      };
      return emojis[category] || '🎨';
    }

    function getActivityLabel(category) {
      const labels = {
        learning: 'การเรียนรู้',
        play: 'การเล่น',
        social: 'ทักษะสังคม',
        preparation: 'เตรียมความพร้อม'
      };
      return labels[category] || category;
    }

    function formatDate(dateString) {
      const date = new Date(dateString);
      return date.toLocaleDateString('th-TH', { 
        year: 'numeric', 
        month: 'short', 
        day: 'numeric' 
      });
    }

    function escapeHtml(text) {
      const div = document.createElement('div');
      div.textContent = text;
      return div.innerHTML;
    }

    function showMessage(message, type) {
      const existingMessage = document.querySelector('.toast-message');
      if (existingMessage) {
        existingMessage.remove();
      }

      const toast = document.createElement('div');
      toast.className = 'toast-message';
      toast.textContent = message;
      toast.style.cssText = `
        position: fixed;
        top: 20px;
        right: 20px;
        background: ${type === 'error' ? '#dc2626' : '#10b981'};
        color: white;
        padding: 1rem 1.5rem;
        border-radius: 8px;
        box-shadow: 0 4px 12px rgba(0,0,0,0.15);
        z-index: 1000;
        animation: slideIn 0.3s ease;
      `;
      
      document.body.appendChild(toast);
      setTimeout(() => toast.remove(), 3000);
    }

    initializeApp();
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9a89a987c3a2894f',t:'MTc2NDgzNDA5NS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
