Here is the HTML document with the PDF export functions fixed to properly capture and display the data from the income ledger and purchasing tables.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes, viewport-fit=cover">
    <title>Flah Humanity | Smart Collective Qurbani System</title>
    <!-- Bootstrap 5 + Icons + Fonts -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- Font Awesome 6 -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <!-- html2pdf library with better compatibility -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js" integrity="sha512-GsLlZN/3F2ErC5ifS5QtgpiJtWd43JWSuIgh7mbzZ8zBps+dvLusV+eNQATqgA/HdeKFVgA5v3S/cIrLF7QnIg==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,600;14..32,700;14..32,800&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }
        
        body {
            background: radial-gradient(circle at 10% 30%, #0a0f1e, #05080f);
            min-height: 100vh;
            padding: 1.5rem;
            color: #eef5ff;
        }
        
        /* Glassmorphic futuristic containers */
        .glass-card {
            background: rgba(15, 25, 45, 0.65);
            backdrop-filter: blur(14px);
            border-radius: 2rem;
            border: 1px solid rgba(0, 255, 255, 0.2);
            box-shadow: 0 25px 40px -12px rgba(0,0,0,0.5), inset 0 1px 0 rgba(255,255,255,0.08);
            transition: all 0.3s ease;
        }
        
        .btn-futuristic {
            background: linear-gradient(95deg, #00c6ff, #0072ff);
            border: none;
            border-radius: 40px;
            padding: 10px 28px;
            font-weight: 600;
            letter-spacing: 0.3px;
            color: white;
            transition: 0.2s;
            box-shadow: 0 4px 12px rgba(0,114,255,0.3);
        }
        
        .btn-futuristic:hover {
            transform: translateY(-2px);
            box-shadow: 0 12px 24px rgba(0,114,255,0.4);
            background: linear-gradient(95deg, #00b4ff, #0066e6);
        }
        
        .btn-outline-cyber {
            background: transparent;
            border: 1.5px solid #0ff;
            color: #0ff;
            border-radius: 2rem;
            padding: 6px 20px;
            font-weight: 600;
            transition: 0.2s;
        }
        
        .btn-outline-cyber:hover {
            background: #0ff20f;
            color: #000;
            box-shadow: 0 0 12px #0ff;
        }
        
        .section-tab {
            cursor: pointer;
            background: rgba(20, 30, 55, 0.7);
            backdrop-filter: blur(8px);
            border-radius: 60px;
            padding: 10px 28px;
            font-weight: 600;
            transition: 0.2s;
            border: 1px solid rgba(0,255,255,0);
        }
        
        .section-tab.active {
            background: linear-gradient(135deg, #0ff, #0066ff);
            color: #0a0f1e;
            border-color: cyan;
            box-shadow: 0 0 15px cyan;
        }
        
        .form-control, .form-select {
            background: rgba(10, 20, 35, 0.8);
            border: 1px solid #2c3e66;
            color: #f0f9ff;
            border-radius: 1.2rem;
            padding: 12px 16px;
        }
        
        .form-control:focus, .form-select:focus {
            background: #0a1428;
            border-color: #0ff;
            box-shadow: 0 0 0 0.2rem rgba(0,255,255,0.25);
            color: white;
        }
        
        .table-cyber {
            background: rgba(0, 0, 0, 0.5);
            border-collapse: separate;
            border-spacing: 0;
            border-radius: 1.5rem;
            overflow: hidden;
            min-width: 600px;
        }
        
        .table-cyber th {
            background: #0a1a2f;
            color: #0ff;
            font-weight: 600;
            border-bottom: 1px solid #0ff33f;
            white-space: nowrap;
        }
        
        .table-cyber td {
            white-space: nowrap;
        }
        
        /* Mobile responsive table wrapper */
        .table-responsive-wrapper {
            width: 100%;
            overflow-x: auto;
            -webkit-overflow-scrolling: touch;
            border-radius: 1.5rem;
        }
        
        .upload-area {
            border: 2px dashed #0ff;
            background: rgba(0, 255, 255, 0.05);
            border-radius: 30px;
            padding: 10px;
            text-align: center;
            cursor: pointer;
            transition: 0.2s;
        }
        
        .upload-area:hover {
            background: rgba(0, 255, 255, 0.15);
        }
        
        .camera-btn {
            background: linear-gradient(135deg, #ff416c, #ff4b2b);
            border: none;
            border-radius: 40px;
            padding: 8px 20px;
            color: white;
            font-weight: bold;
        }
        
        footer {
            border-top: 1px solid rgba(0, 255, 255, 0.2);
            margin-top: 3rem;
            padding-top: 1.5rem;
            text-align: center;
            font-size: 0.8rem;
            opacity: 0.7;
        }
        
        .animal-thumb {
            width: 55px;
            height: 55px;
            object-fit: cover;
            border-radius: 1rem;
            border: 1px solid cyan;
        }
        
        @media (max-width: 768px) {
            body { padding: 1rem; }
            .section-tab { padding: 6px 16px; font-size: 0.9rem; }
        }
        
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #0a0f1e;
        }
        ::-webkit-scrollbar-thumb {
            background: cyan;
            border-radius: 8px;
        }
        
        .media-preview {
            max-width: 100px;
            max-height: 80px;
            border-radius: 12px;
            object-fit: cover;
        }
        
        .main-title {
            font-size: 4rem;
            font-weight: 800;
            background: linear-gradient(135deg, #fff, #0ff, #00a6ff);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 0 20px rgba(0,255,255,0.3);
            letter-spacing: 2px;
        }
        
        @media (max-width: 576px) {
            .main-title { font-size: 2.5rem; }
        }
        
        .cow-icon {
            color: #0ff;
            filter: drop-shadow(0 0 5px cyan);
        }
        
        /* PDF print styles */
        .pdf-report {
            padding: 20px;
            background: white;
            color: black;
            font-family: Arial, sans-serif;
        }
        .pdf-report h2, .pdf-report h3 {
            color: #1a5f7a;
        }
        .pdf-report table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 15px;
        }
        .pdf-report th, .pdf-report td {
            border: 1px solid #ccc;
            padding: 8px;
            text-align: left;
        }
        .pdf-report th {
            background: #e0f0f5;
        }
    </style>
</head>
<body>

<div class="container-lg px-2 px-md-4">
    <!-- Futuristic Header with only QURBANI -->
    <div class="text-center mb-4">
        <h1 class="main-title">QURBANI</h1>
        <p class="text-cyan-300 mt-2">Advanced Collective Sacrifice Management System</p>
    </div>

    <!-- NGO Link trigger -->
    <div class="text-center mt-1">
        <a href="#" id="showNgoLink" class="text-decoration-none fs-5" style="color: #0ff; font-weight: 600;"><i class="fas fa-building"></i> ادارہ فلاح انسانیت | Flah Humanity Foundation</a>
    </div>
    <div id="ngoDisplayArea" class="text-center my-2 p-2 rounded-4 fw-bold" style="background: rgba(0,255,255,0.1); letter-spacing: 1px; font-size: 1.3rem;"></div>
    <div class="text-center text-info-emphasis mb-2"><i class="fas fa-user-astronaut"></i> Lead Developer: Mohammed Adnan</div>
    
    <!-- ENTER BUTTON -->
    <div class="d-flex justify-content-center my-4">
        <button id="enterMainBtn" class="btn btn-futuristic px-5 py-3 fs-5"><i class="fas fa-fingerprint me-2"></i> ENTER DASHBOARD</button>
    </div>

    <!-- MAIN PANEL -->
    <div id="mainPanel" style="display: none;">
        <!-- TABS -->
        <div class="d-flex justify-content-center gap-3 mb-5 flex-wrap">
            <div id="qurbaniTabBtn" class="section-tab active"><i class="fas fa-user-astronaut me-2"></i> QURBANI APPLY</div>
            <div id="adminTabBtn" class="section-tab"><i class="fas fa-crown me-2"></i> ADMIN NEXUS</div>
        </div>

        <!-- ======================= QURBANI SECTION ======================= -->
        <div id="qurbaniSection" class="glass-card p-4 p-md-5">
            <div class="d-flex align-items-center gap-3 mb-4">
                <i class="fas fa-file-invoice-dollar fa-2x" style="color: #0ff;"></i>
                <h3 class="mb-0">📿 Register Your Qurbani Share</h3>
            </div>
            <form id="qurbaniForm">
                <div class="row g-4">
                    <div class="col-md-4"><label class="form-label"><i class="fas fa-user me-1"></i> Full Name</label><input type="text" class="form-control" id="userName" required placeholder="e.g., Ahmed Raza"></div>
                    <div class="col-md-4"><label class="form-label"><i class="fas fa-user-friends"></i> Father's Name</label><input type="text" class="form-control" id="fatherName" required placeholder="Abdul Qadir"></div>
                    <div class="col-md-4"><label class="form-label"><i class="fas fa-phone-alt"></i> Contact Number</label><input type="tel" class="form-control" id="contactNo" required placeholder="+92 300 1234567"></div>
                    <div class="col-md-3"><label class="form-label"><i class="fas fa-tag"></i> Share Category</label>
                        <select id="hissaType" class="form-select">
                            <option value="KATTA">KATTA (Male Buffalo)</option>
                            <option value="KATTI">KATTI (Female Buffalo)</option>
                            <option value="WACHA">WACHA (Male Cow)</option>
                            <option value="WACHI">WACHI (Female Cow)</option>
                        </select>
                    </div>
                    <div class="col-md-3"><label class="form-label"><i class="fas fa-coins"></i> Amount (PKR)</label><select id="amountSelect" class="form-select"><option>28000</option><option>32000</option><option>34000</option><option>38000</option></select></div>
                    <div class="col-md-3"><label class="form-label"><i class="fas fa-chart-simple"></i> Number of Shares (1-7)</label><input type="number" id="pistas" min="1" max="7" value="1" class="form-control"></div>
                    <div class="col-md-3"><label class="form-label"><i class="fas fa-university"></i> Account Holder</label><select id="accountTitle" class="form-select"><option>Nouman Rasheed</option><option>Kashif Nadeem</option><option>Muhammad Adnan</option><option>Asif Ibrahim</option></select></div>
                    <div class="col-12"><label class="form-label"><i class="fas fa-receipt"></i> Upload Deposit Slip / Screenshot</label>
                        <div class="upload-area" onclick="document.getElementById('receiptUpload').click();"><i class="fas fa-cloud-upload-alt me-2"></i> Click to upload receipt (image/PDF)</div>
                        <input type="file" id="receiptUpload" accept="image/*,application/pdf" style="display:none">
                        <span id="receiptStatus" class="small text-info ms-2"></span>
                    </div>
                    <div class="col-12 mt-3"><button type="submit" class="btn btn-futuristic w-100 py-2"><i class="fas fa-check-double"></i> SUBMIT QURBANI SHARE</button></div>
                </div>
            </form>
            <div id="qurbaniMessage" class="mt-4 alert d-none"></div>
        </div>

        <!-- ======================= ADMIN SECTION ======================= -->
        <div id="adminSection" style="display: none;">
            <ul class="nav nav-tabs mb-4 border-0 gap-2" id="adminTabs" role="tablist">
                <li class="nav-item" role="presentation"><button class="nav-link active btn-outline-cyber me-2" data-bs-toggle="tab" data-bs-target="#incomeTab" type="button"><i class="fas fa-chart-line"></i> Income Ledger</button></li>
                <li class="nav-item"><button class="nav-link btn-outline-cyber" data-bs-toggle="tab" data-bs-target="#purchaseTab" type="button"><i class="fas fa-truck-fast"></i> Livestock Purchasing</button></li>
                <li class="nav-item"><button class="nav-link btn-outline-cyber" data-bs-toggle="tab" data-bs-target="#listingTab" type="button"><i class="fas fa-list-ul"></i> Animals Registry</button></li>
            </ul>
            <div class="tab-content glass-card p-4">
                <!-- INCOME SECTION -->
                <div class="tab-pane fade show active" id="incomeTab">
                    <div class="d-flex justify-content-between align-items-center flex-wrap gap-3 mb-4">
                        <h4><i class="fas fa-database text-info"></i> All Collected Shares</h4>
                        <button id="downloadIncomePDF" class="btn btn-futuristic"><i class="fas fa-file-pdf"></i> Export PDF</button>
                    </div>
                    <div class="table-responsive-wrapper">
                        <table class="table table-cyber text-white" id="incomeTable">
                            <thead>
                                <tr><th>#</th><th>Shareholder Name</th><th>Shares(Qty)</th><th>Amount (PKR)</th><th>Account</th><th>Deposit Date</th><th>Type</th></tr>
                            </thead>
                            <tbody id="incomeListBody"></tbody>
                        </table>
                    </div>
                </div>

                <!-- PURCHASE SECTION -->
                <div class="tab-pane fade" id="purchaseTab">
                    <div class="row g-4">
                        <div class="col-12"><div class="bg-dark p-3 rounded-4"><h5><i class="fas fa-plus-circle"></i> Register New Animal</h5>
                        <form id="addAnimalForm" class="row g-3">
                            <div class="col-md-3"><label>Purchase Date</label><input type="date" id="purchaseDate" class="form-control" required></div>
                            <div class="col-md-2"><label>Price (PKR)</label><input type="number" id="animalPrice" placeholder="Price" class="form-control" required></div>
                            <div class="col-md-2"><label>Quantity</label><input type="number" id="animalCount" value="1" class="form-control"></div>
                            <div class="col-md-3"><label>Animal Type</label>
                                <select id="animalType" class="form-select">
                                    <option value="KATTA (Male Buffalo)">KATTA (Male Buffalo)</option>
                                    <option value="KATTI (Female Buffalo)">KATTI (Female Buffalo)</option>
                                    <option value="WACHA (Male Cow)">WACHA (Male Cow)</option>
                                    <option value="WACHI (Female Cow)">WACHI (Female Cow)</option>
                                </select>
                            </div>
                            <div class="col-md-2"><label>Expected Weight (kg)</label><input type="text" id="expectedWeight" placeholder="e.g., 350kg" class="form-control"></div>
                            <div class="col-12"><label>Short Description</label><textarea id="animalDesc" rows="2" placeholder="Breed, color, health notes..." class="form-control"></textarea></div>
                            <div class="col-12">
                                <label>📸 Upload Picture OR Short Video (3-5 sec)</label>
                                <div class="d-flex flex-wrap gap-2 align-items-center">
                                    <div class="upload-area flex-grow-1" onclick="document.getElementById('animalMedia').click();"><i class="fas fa-cloud-upload-alt me-2"></i> Choose from Gallery</div>
                                    <button type="button" id="openCameraBtn" class="camera-btn"><i class="fas fa-camera me-2"></i> Open Camera</button>
                                </div>
                                <input type="file" id="animalMedia" accept="image/*,video/mp4" style="display:none">
                                <div id="mediaPreview" class="mt-2"></div>
                            </div>
                            <div class="col-12"><button type="submit" class="btn btn-futuristic"><i class="fas fa-save"></i> Add Animal Asset</button></div>
                        </form></div></div>
                        <div class="col-12 mt-3 d-flex justify-content-between flex-wrap gap-2"><h5>📋 Purchasing Log</h5><button id="downloadPurchasePDF" class="btn btn-outline-cyber"><i class="fas fa-print"></i> PDF Report</button></div>
                        <div class="table-responsive-wrapper">
                            <table class="table table-cyber" id="purchaseTable">
                                <thead><tr><th>Date</th><th>Price (PKR)</th><th>Qty</th><th>Type</th><th>Details</th><th>Media Preview</th></tr></thead>
                                <tbody id="purchaseListBody"></tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <!-- LISTING & SHAREHOLDER ASSIGNMENT -->
                <div class="tab-pane fade" id="listingTab">
                    <h5><i class="fas fa-paw text-info"></i> Registered Animals (Click any to assign shareholders)</h5>
                    <div id="animalsListContainer" class="row g-3 my-3"></div>
                    <div id="shareholderAssignmentArea" style="display:none;" class="mt-4 p-3 rounded-4" style="background:#0a1022;">
                        <hr class="border-info"><h5>Assign Shareholders to: <span id="selectedAnimalIdSpan" class="text-warning"></span></h5>
                        <p class="small text-info">Maximum 7 shareholders per animal (1 share each person).</p>
                        <select id="availableShareholdersSelect" class="form-select mb-3"></select>
                        <button id="assignShareholderBtn" class="btn btn-info me-2"><i class="fas fa-user-plus"></i> Assign Selected</button>
                        <div id="assignedListDiv" class="mt-3 bg-dark p-3 rounded-3"></div>
                        <button id="completeAnimalAssignmentBtn" class="btn btn-success mt-3"><i class="fas fa-lock"></i> Finalize & Save Animal Shareholders</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <footer>
        <i class="fas fa-shield-alt"></i> Flah Humanity Foundation | Transparent Qurbani System | Powered by Smart Ledger
    </footer>
</div>

<script>
    // ======================= LOCAL STORAGE KEYS =======================
    let qurbaniApplications = JSON.parse(localStorage.getItem("flah_qurbani_apps") || "[]");
    let animalsPurchased = JSON.parse(localStorage.getItem("flah_animals") || "[]");
    let animalShareholdersMap = JSON.parse(localStorage.getItem("flah_animal_shareholders") || "{}");

    function saveAll(){
        localStorage.setItem("flah_qurbani_apps", JSON.stringify(qurbaniApplications));
        localStorage.setItem("flah_animals", JSON.stringify(animalsPurchased));
        localStorage.setItem("flah_animal_shareholders", JSON.stringify(animalShareholdersMap));
    }

    function renderIncome(){
        let tbody = document.getElementById("incomeListBody");
        if(!tbody) return;
        tbody.innerHTML = "";
        qurbaniApplications.forEach((app, i) => {
            tbody.innerHTML += `<tr><td class="text-white">${i+1}</td><td class="text-white">${app.userName} / ${app.fatherName}</td><td class="text-white">${app.pistas}</td><td class="text-white">${app.amount}</td><td class="text-white">${app.accountTitle}</td><td class="text-white">${app.date || new Date().toLocaleDateString()}</td><td class="text-white">${app.hissaType}</td></tr>`;
        });
    }
    
    function renderPurchaseTable(){
        let tbody = document.getElementById("purchaseListBody");
        if(!tbody) return;
        tbody.innerHTML = "";
        animalsPurchased.forEach((a) => {
            let mediaHtml = a.mediaData ? (a.mediaType==='image' ? `<img src="${a.mediaData}" class="animal-thumb">` : `<i class="fas fa-video text-info"></i> video`) : "—";
            tbody.innerHTML += `<tr><td class="text-white">${a.date}</td><td class="text-white">${a.price}</td><td class="text-white">${a.count}</td><td class="text-white">${a.type}</td><td class="text-white">${a.desc} | W:${a.weight}</td><td>${mediaHtml}</td></tr>`;
        });
    }
    
    function renderAnimalsList(){
        let container = document.getElementById("animalsListContainer");
        if(!container) return;
        container.innerHTML = "";
        animalsPurchased.forEach((animal, idx) => {
            let assignedCount = (animalShareholdersMap[idx] || []).length;
            container.innerHTML += `<div class="col-md-3 col-6"><div class="glass-card p-2 text-center animal-entry" style="cursor:pointer;"><i class="fas fa-cow fa-2x cow-icon"></i><div class="fw-bold mt-1">${animal.type}</div><small>${animal.price} PKR | ${animal.date}</small><br><span class="badge bg-info mt-1">${assignedCount}/7 Shareholders</span><br><button class="btn btn-sm btn-outline-cyber mt-2 assign-trigger" data-idx="${idx}"><i class="fas fa-users"></i> Assign Shares</button></div></div>`;
        });
        document.querySelectorAll('.assign-trigger').forEach(btn => {
            btn.addEventListener('click', (e) => { e.stopPropagation(); let idx = btn.getAttribute('data-idx'); openShareholderAssignment(parseInt(idx)); });
        });
    }
    
    let currentAnimalIdx = null;
    function openShareholderAssignment(animalIndex){
        currentAnimalIdx = animalIndex;
        let currentAssigned = animalShareholdersMap[animalIndex] || [];
        if(currentAssigned.length >= 7){
            alert("Maximum 7 shareholders already assigned to this animal.");
            return;
        }
        document.getElementById("shareholderAssignmentArea").style.display = "block";
        document.getElementById("selectedAnimalIdSpan").innerHTML = `ANIMAL #${animalIndex} (${animalsPurchased[animalIndex]?.type}) &nbsp; <span class="badge bg-warning">${currentAssigned.length}/7 assigned</span>`;
        renderAvailableShareholders(animalIndex);
        renderAssignedList(animalIndex);
    }
    
    function renderAvailableShareholders(animalIdx){
        let assignedIds = animalShareholdersMap[animalIdx] || [];
        let available = qurbaniApplications.filter((_, idx) => !assignedIds.includes(idx));
        let select = document.getElementById("availableShareholdersSelect");
        select.innerHTML = "<option value=''>-- Select Shareholder --</option>";
        available.forEach((app, origIdx) => {
            select.innerHTML += `<option value="${origIdx}">${app.userName} (${app.fatherName}) - Deposited ${app.amount} PKR | ${app.pistas} shares</option>`;
        });
        if(available.length === 0){
            select.innerHTML = "<option value=''>No available shareholders</option>";
        }
    }
    
    function renderAssignedList(animalIdx){
        let assignedIds = animalShareholdersMap[animalIdx] || [];
        let div = document.getElementById("assignedListDiv");
        if(assignedIds.length === 0){ div.innerHTML = "<i class='fas fa-info-circle'></i> No shareholders assigned yet."; return; }
        let html = "<ul class='list-group bg-transparent'>";
        assignedIds.forEach(shId => {
            let sh = qurbaniApplications[shId];
            if(sh) html += `<li class='list-group-item bg-dark text-white d-flex justify-content-between align-items-center'>📌 ${sh.userName} | ${sh.contactNo} | ${sh.amount} PKR <button class='btn btn-sm btn-danger remove-sh' data-animal="${animalIdx}" data-shidx="${shId}"><i class='fas fa-trash'></i> Remove</button></li>`;
        });
        html += "</ul>";
        div.innerHTML = html;
        document.querySelectorAll('.remove-sh').forEach(btn => {
            btn.addEventListener('click', (e) => {
                let aIdx = btn.getAttribute('data-animal');
                let sId = parseInt(btn.getAttribute('data-shidx'));
                let list = animalShareholdersMap[aIdx] || [];
                animalShareholdersMap[aIdx] = list.filter(id => id != sId);
                saveAll();
                renderAssignedList(aIdx);
                renderAvailableShareholders(aIdx);
                renderAnimalsList();
                let currentLen = (animalShareholdersMap[aIdx] || []).length;
                document.getElementById("selectedAnimalIdSpan").innerHTML = `ANIMAL #${aIdx} (${animalsPurchased[aIdx]?.type}) &nbsp; <span class="badge bg-warning">${currentLen}/7 assigned</span>`;
            });
        });
    }
    
    document.getElementById("assignShareholderBtn")?.addEventListener("click", () => {
        if(currentAnimalIdx === null) return;
        let currentAssigned = animalShareholdersMap[currentAnimalIdx] || [];
        if(currentAssigned.length >= 7){
            alert("Cannot assign more than 7 shareholders per animal.");
            return;
        }
        let select = document.getElementById("availableShareholdersSelect");
        let selected = select.value;
        if(!selected || selected === "") return alert("Select a shareholder first");
        let assigned = animalShareholdersMap[currentAnimalIdx] || [];
        if(assigned.includes(parseInt(selected))) return alert("Already assigned.");
        assigned.push(parseInt(selected));
        animalShareholdersMap[currentAnimalIdx] = assigned;
        saveAll();
        renderAvailableShareholders(currentAnimalIdx);
        renderAssignedList(currentAnimalIdx);
        renderAnimalsList();
        let updatedLen = (animalShareholdersMap[currentAnimalIdx] || []).length;
        document.getElementById("selectedAnimalIdSpan").innerHTML = `ANIMAL #${currentAnimalIdx} (${animalsPurchased[currentAnimalIdx]?.type}) &nbsp; <span class="badge bg-warning">${updatedLen}/7 assigned</span>`;
    });
    
    document.getElementById("completeAnimalAssignmentBtn")?.addEventListener("click", () => {
        alert("✅ Shareholders finalized for this animal.");
        renderIncome();
        renderAnimalsList();
    });
    
    // ======================= FIXED PDF FUNCTIONS =======================
    async function generatePDFFromData(type) {
        const ngoName = "اداره فلاح انسانیت - Flah Humanity Foundation";
        const currentDate = new Date().toLocaleString();
        
        let htmlContent = `
            <div class="pdf-report" style="padding: 20px; font-family: Arial, sans-serif;">
                <div style="text-align: center; margin-bottom: 20px;">
                    <h2 style="color: #1a5f7a; margin-bottom: 5px;">${ngoName}</h2>
                    <h3>${type === 'income' ? 'INCOME LEDGER REPORT' : 'LIVESTOCK PURCHASING REPORT'}</h3>
                    <p>Generated on: ${currentDate}</p>
                    <hr style="border: 1px solid #ccc;">
                </div>
        `;
        
        if(type === 'income') {
            htmlContent += `
                <table style="width: 100%; border-collapse: collapse;">
                    <thead>
                        <tr style="background: #e0f0f5;">
                            <th style="border: 1px solid #ccc; padding: 8px;">#</th>
                            <th style="border: 1px solid #ccc; padding: 8px;">Shareholder Name</th>
                            <th style="border: 1px solid #ccc; padding: 8px;">Shares</th>
                            <th style="border: 1px solid #ccc; padding: 8px;">Amount (PKR)</th>
                            <th style="border: 1px solid #ccc; padding: 8px;">Account</th>
                            <th style="border: 1px solid #ccc; padding: 8px;">Date</th>
                            <th style="border: 1px solid #ccc; padding: 8px;">Type</th>
                        </tr>
                    </thead>
                    <tbody>
            `;
            qurbaniApplications.forEach((app, i) => {
                htmlContent += `
                    <tr>
                        <td style="border: 1px solid #ccc; padding: 8px;">${i+1}</td>
                        <td style="border: 1px solid #ccc; padding: 8px;">${app.userName} / ${app.fatherName}</td>
                        <td style="border: 1px solid #ccc; padding: 8px;">${app.pistas}</td>
                        <td style="border: 1px solid #ccc; padding: 8px;">${app.amount}</td>
                        <td style="border: 1px solid #ccc; padding: 8px;">${app.accountTitle}</td>
                        <td style="border: 1px solid #ccc; padding: 8px;">${app.date || new Date().toLocaleDateString()}</td>
                        <td style="border: 1px solid #ccc; padding: 8px;">${app.hissaType}</td>
                    </tr>
                `;
            });
            htmlContent += `
                    </tbody>
                </table>
                <div style="margin-top: 20px; text-align: right;">
                    <p><strong>Total Collection:</strong> ${qurbaniApplications.reduce((sum, app) => sum + parseInt(app.amount), 0)} PKR</p>
                </div>
            `;
        } else if(type === 'purchase') {
            htmlContent += `
                <table style="width: 100%; border-collapse: collapse;">
                    <thead>
                        <tr style="background: #e0f0f5;">
                            <th style="border: 1px solid #ccc; padding: 8px;">Date</th>
                            <th style="border: 1px solid #ccc; padding: 8px;">Price (PKR)</th>
                            <th style="border: 1px solid #ccc; padding: 8px;">Quantity</th>
                            <th style="border: 1px solid #ccc; padding: 8px;">Animal Type</th>
                            <th style="border: 1px solid #ccc; padding: 8px;">Description</th>
                            <th style="border: 1px solid #ccc; padding: 8px;">Expected Weight</th>
                        </tr>
                    </thead>
                    <tbody>
            `;
            animalsPurchased.forEach((animal) => {
                htmlContent += `
                    <tr>
                        <td style="border: 1px solid #ccc; padding: 8px;">${animal.date}</td>
                        <td style="border: 1px solid #ccc; padding: 8px;">${animal.price}</td>
                        <td style="border: 1px solid #ccc; padding: 8px;">${animal.count}</td>
                        <td style="border: 1px solid #ccc; padding: 8px;">${animal.type}</td>
                        <td style="border: 1px solid #ccc; padding: 8px;">${animal.desc || '-'}</td>
                        <td style="border: 1px solid #ccc; padding: 8px;">${animal.weight || '-'}</td>
                    </tr>
                `;
            });
            htmlContent += `
                    </tbody>
                </table>
                <div style="margin-top: 20px; text-align: right;">
                    <p><strong>Total Animals Purchased:</strong> ${animalsPurchased.reduce((sum, a) => sum + parseInt(a.count), 0)}</p>
                    <p><strong>Total Investment:</strong> ${animalsPurchased.reduce((sum, a) => sum + (parseInt(a.price) * parseInt(a.count)), 0)} PKR</p>
                </div>
            `;
        }
        
        htmlContent += `<div style="margin-top: 30px; text-align: center; font-size: 12px; color: #666;">
                            <hr>Flah Humanity Foundation - Official Qurbani Record
                        </div></div>`;
        
        const opt = {
            margin: [0.5, 0.5, 0.5, 0.5],
            filename: type === 'income' ? 'Flah_Income_Report.pdf' : 'Flah_Purchase_Report.pdf',
            image: { type: 'jpeg', quality: 0.98 },
            html2canvas: { scale: 2, letterRendering: true, useCORS: true },
            jsPDF: { unit: 'in', format: 'a4', orientation: 'landscape' }
        };
        
        const element = document.createElement('div');
        element.innerHTML = htmlContent;
        document.body.appendChild(element);
        try {
            await html2pdf().set(opt).from(element).save();
        } catch (err) {
            console.error("PDF Error:", err);
            alert("PDF generation failed, but data is safe. Try again.");
        }
        document.body.removeChild(element);
    }
    
    document.getElementById("downloadIncomePDF")?.addEventListener("click", async () => {
        if(qurbaniApplications.length === 0) {
            alert("No income data available to export.");
            return;
        }
        await generatePDFFromData('income');
    });
    
    document.getElementById("downloadPurchasePDF")?.addEventListener("click", async () => {
        if(animalsPurchased.length === 0) {
            alert("No purchase data available to export.");
            return;
        }
        await generatePDFFromData('purchase');
    });
    
    // Qurbani form submit
    document.getElementById("qurbaniForm")?.addEventListener("submit", (e) => {
        e.preventDefault();
        let newEntry = {
            userName: document.getElementById("userName").value, 
            fatherName: document.getElementById("fatherName").value, 
            contactNo: document.getElementById("contactNo").value,
            hissaType: document.getElementById("hissaType").value, 
            amount: document.getElementById("amountSelect").value, 
            pistas: document.getElementById("pistas").value,
            accountTitle: document.getElementById("accountTitle").value, 
            date: new Date().toLocaleString()
        };
        qurbaniApplications.push(newEntry);
        saveAll();
        renderIncome();
        document.getElementById("qurbaniForm").reset();
        let msg = document.getElementById("qurbaniMessage");
        msg.classList.remove("d-none"); 
        msg.classList.add("alert-success"); 
        msg.innerHTML = "<i class='fas fa-check-circle'></i> ✨ Qurbani share recorded successfully! Jazakallah ✨";
        setTimeout(()=>msg.classList.add("d-none"), 3000);
        if(currentAnimalIdx !== null){
            renderAvailableShareholders(currentAnimalIdx);
        }
    });
    
    // Camera and file handling
    let currentMediaData = null, currentMediaType = null;
    document.getElementById("openCameraBtn")?.addEventListener("click", () => {
        let input = document.createElement('input');
        input.type = 'file';
        input.accept = 'image/*';
        input.capture = 'environment';
        input.onchange = (e) => {
            if(e.target.files.length) handleMediaFile(e.target.files[0]);
        };
        input.click();
    });
    document.getElementById("animalMedia")?.addEventListener("change", (e) => {
        if(e.target.files.length) handleMediaFile(e.target.files[0]);
    });
    function handleMediaFile(file){
        let reader = new FileReader();
        reader.onload = (ev) => {
            currentMediaData = ev.target.result;
            currentMediaType = file.type.startsWith("image") ? "image" : "video";
            let previewDiv = document.getElementById("mediaPreview");
            if(currentMediaType === "image") previewDiv.innerHTML = `<img src="${currentMediaData}" class="media-preview mt-2 border rounded">`;
            else previewDiv.innerHTML = `<video src="${currentMediaData}" controls class="media-preview mt-2"></video>`;
        };
        reader.readAsDataURL(file);
    }
    
    document.getElementById("addAnimalForm")?.addEventListener("submit", (e) => {
        e.preventDefault();
        let animal = { 
            date: document.getElementById("purchaseDate").value, 
            price: document.getElementById("animalPrice").value, 
            count: document.getElementById("animalCount").value, 
            type: document.getElementById("animalType").value, 
            weight: document.getElementById("expectedWeight").value, 
            desc: document.getElementById("animalDesc").value, 
            mediaData: currentMediaData || "", 
            mediaType: currentMediaType || "" 
        };
        animalsPurchased.push(animal);
        saveAll();
        renderPurchaseTable(); 
        renderAnimalsList();
        document.getElementById("addAnimalForm").reset();
        document.getElementById("mediaPreview").innerHTML = "";
        currentMediaData = null; 
        currentMediaType = null;
        alert("Animal added successfully!");
    });
    
    document.getElementById("receiptUpload")?.addEventListener("change", ()=>document.getElementById("receiptStatus").innerHTML = "<i class='fas fa-check-circle'></i> Receipt uploaded");
    
    function init(){
        renderIncome(); 
        renderPurchaseTable(); 
        renderAnimalsList();
        document.getElementById("qurbaniTabBtn").onclick = ()=>{ 
            document.getElementById("qurbaniSection").style.display="block"; 
            document.getElementById("adminSection").style.display="none"; 
            document.getElementById("qurbaniTabBtn").classList.add("active"); 
            document.getElementById("adminTabBtn").classList.remove("active"); 
        };
        document.getElementById("adminTabBtn").onclick = ()=>{ 
            document.getElementById("adminSection").style.display="block"; 
            document.getElementById("qurbaniSection").style.display="none"; 
            document.getElementById("adminTabBtn").classList.add("active"); 
            document.getElementById("qurbaniTabBtn").classList.remove("active"); 
        };
        document.getElementById("enterMainBtn").onclick = ()=>{ 
            document.getElementById("mainPanel").style.display = "block"; 
        };
        document.getElementById("showNgoLink").onclick = (e)=>{ 
            e.preventDefault(); 
            document.getElementById("ngoDisplayArea").innerHTML = "🌟 ادارہ فلاح انسانیت (Flah Humanity Foundation) 🌟"; 
        };
    }
    init();
</script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```
