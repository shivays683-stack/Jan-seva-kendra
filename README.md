# Jan-seva-kendra
There i need to make a website for grown up our bussiness just for help peoples to know how it doing 
<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1"  -
  Krishna Cyber Cafe & Jan Seva Kendra
<script src="https://cdn.tailwindcss.com"></script>
<script>
  tailwind.config = { theme: { extend: { fontFamily: { sans:['Inter','sans-serif'] } } } };
</script>
<style>
/* loader */
.loader { border:4px solid #f3f3f3; border-top:4px solid #3b82f6; border-radius:50%; width:24px; height:24px; animation:spin 1s linear infinite; }
@keyframes spin { 0%{transform:rotate(0deg);}100%{transform:rotate(360deg);} }

/* modal */
.modal-backdrop { background: rgba(0,0,0,0.5); position: fixed; inset:0; display:flex; align-items:center; justify-content:center; z-index:60; }
.modal { width:95%; max-width:1000px; max-height:85vh; overflow:auto; background:white; border-radius:0.5rem; padding:1rem; box-shadow:0 10px 30px rgba(0,0,0,0.2); }
.service-item { cursor:pointer; }
.subitem { cursor:pointer; }
.small-muted { color:#6b7280; font-size:0.92rem; }
.hidden { display:none; }

/* small responsive tweaks */
@media (min-width: 768px) {
  .modal { padding:1.5rem; }
}
</style>
</head>
<body class="bg-gray-100 font-sans text-gray-800">

<!-- Header -->
<header class="bg-white shadow sticky top-0 z-50">
  <nav class="container mx-auto px-4 py-4 flex justify-between items-center">
    <div>
      <a href="#" class="text-2xl font-bold text-blue-600">Kendra-Krishna Cyber Cafe & Jan Seva Kendra</a>
      <div class="small-muted">Patel Nager, Gonda — +91 90444 46667</div>
    </div>
    <div class="flex gap-4 items-center">
      <a href="#services" class="text-sm text-gray-600 hover:text-blue-600">Services</a>
      <a href="#contact" class="text-sm text-gray-600 hover:text-blue-600">Contact</a>
      <a href="#ai-helper" class="text-sm text-gray-600 hover:text-blue-600">AI Helper</a>
    </div>
  </nav>
</header>

<!-- Hero -->
<section class="bg-blue-700 text-white text-center py-12">
  <div class="container mx-auto px-4">
    <h1 class="text-3xl sm:text-4xl font-extrabold">Welcome to Kendra-Krishna Cyber Cafe & Jan Seva Kendra</h1>
    <p class="mt-3 text-lg">A to Z computer & Jan Seva | Classes | Forms | Tickets | Printing | Lab</p>
    <a href="tel:+919044446667" class="inline-block mt-4 bg-white text-blue-700 px-5 py-2 rounded-lg font-bold">Call Now</a>
  </div>
</section>

<!-- Services + Search -->
<section id="services" class="container mx-auto px-4 py-12">
  <div class="flex flex-col md:flex-row md:items-center md:justify-between gap-4 mb-6">
    <h2 class="text-2xl font-bold">Hamari Sevaayein</h2>
    <div class="w-full md:w-1/2">
      <input id="global-search" type="search" placeholder="Search service or form (e.g., JEE, IRCTC, Scholarship...)" class="w-full p-3 rounded border" />
    </div>
  </div>

  <div id="services-grid" class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-4">
    <!-- JS will populate service cards -->
  </div>

  <p class="text-center text-gray-600 mt-6">Click any service to see detailed sub-items & required documents.</p>
</section>

<!-- AI helper (kept minimal) -->
<section id="ai-helper" class="bg-white py-12">
  <div class="container mx-auto px-4 max-w-3xl">
    <h3 class="text-xl font-bold mb-2">Quick Documents Check (Search)</h3>
    <div class="flex gap-2">
      <input id="ai-prompt" type="text" placeholder="Type task (e.g., 'PAN card', 'JEE application')" class="flex-1 p-2 border rounded" />
      <button id="ai-btn" class="bg-blue-600 text-white px-4 py-2 rounded">Check</button>
    </div>
    <div id="ai-output" class="mt-3 p-3 bg-gray-50 border rounded hidden"></div>
  </div>
</section>

<!-- Contact -->
<section id="contact" class="container mx-auto px-4 py-12">
  <div class="grid md:grid-cols-2 gap-6">
    <div class="bg-white p-6 rounded shadow">
      <h3 class="text-lg font-bold">Contact & Info</h3>
      <p class="mt-2"><strong>CSC Holder:</strong> Anoop Kumar Gupta</p>
      <p><strong>Address:</strong> Patel Nager, Gonda, Uttar Pradesh</p>
      <p><strong>Landmark:</strong> Near Gonda Nursing Home and Hospital, old Mohan Lal School</p>
      <p><strong>Phone:</strong> <a href="tel:+919044446667" class="text-blue-600">+91 90444 46667</a></p>
      <p><strong>Hours:</strong> 9am - 9pm (7 days)</p>
    </div>

    <div class="bg-white p-6 rounded shadow">
      <h3 class="text-lg font-bold">Location</h3>
      <div class="mt-3 h-64 overflow-hidden rounded">
        <iframe src="https://maps.app.goo.gl/mjaSMjzMQkqYoBCp7" width="100%" height="100%" style="border:0;"></iframe>
      </div>
    </div>
  </div>
</section>

<!-- Footer -->
<footer class="bg-gray-800 text-gray-200 py-6 mt-8">
  <div class="container mx-auto px-4 text-center">
    &copy; 2025 Kendra-Krishna Cyber Cafe & Jan Seva Kendra
  </div>
</footer>

<!-- Modal (details panel) -->
<div id="modal-root" class="hidden"></div>

<script>
/* ---------------- DATA: servicesData ----------------
   Each service -> subitems -> documents, help, optional link
   Edit/extend as needed.
*/
const servicesData = {
  "tickets": {
    title: "Train & Air Ticket Booking",
    description: "IRCTC, domestic flights, OTA bookings & printing",
    subitems: {
      "irctc": {
        title: "IRCTC (Train ticket)",
        help: "PNR booking, e-ticket print, tatkal support",
        documents: ["Valid Photo ID (Aadhaar/Passport/Voter ID/Driving Licence)", "Mobile number linked to ID for OTP", "Payment method (card/UPI)"],
        link: "https://www.irctc.co.in"
      },
      "air": {
        title: "Air Ticket (Domestic)",
        help: "Flight booking & print boarding pass",
        documents: ["Valid Photo ID (Aadhaar/Passport)", "E-mail & Mobile for PNR", "Payment method"],
        link: ""
      },
      "ota": {
        title: "Online Travel Agents",
        help: "MakeMyTrip, Goibibo booking help",
        documents: ["Photo ID for check-in", "Payment method"],
        link: ""
      }
    }
  },

  "forms": {
    title: "Exam & Application Forms",
    description: "JEE, NEET, Board, UPSC, SSC, Bank, GATE and more",
    subitems: {
      "jee-main": {
        title: "JEE Main",
        help: "NTA engineering entrance",
        documents: ["DOB proof (Class 10 certificate)", "Class 12 mark sheet / passing certificate", "Photograph & signature (as per specs)", "ID proof (Aadhaar/Passport)"],
        link: "https://jeemain.nta.nic.in"
      },
      "jee-adv": {
        title: "JEE Advanced",
        help: "IIT entrance (after JEE Main rank)",
        documents: ["JEE Main score/admit card", "Photograph & signature", "Class 12 certificate"],
        link: "https://jeeadv.ac.in"
      },
      "neet": {
        title: "NEET (UG)",
        help: "Medical entrance (NTA)",
        documents: ["Class 10 (DOB proof)", "Class 12 marksheet/passing certificate", "Photo & signature", "ID proof"],
        link: "https://neet.nta.nic.in"
      },
      "up-board": {
        title: "State Board (UP Board) Exams",
        help: "10th/12th board related forms & corrections",
        documents: ["School details, DOB proof, previous marksheet", "Passport-size photo"],
        link: ""
      },
      "upsc": {
        title: "UPSC (CSE)",
        help: "Civil Services preliminary & mains applications",
        documents: ["Photo & signature", "Educational certificates for certain posts", "Category certificate if applicable"],
        link: "https://upsconline.nic.in"
      },
      "ssc": {
        title: "SSC (CGL/CHSL etc.)",
        help: "Central government recruitment",
        documents: ["Matriculation (DOB proof)", "Education certificates", "Photo & signature"],
        link: "https://ssc.nic.in"
      },
      "bank": {
        title: "Bank Exams (IBPS/SBI)",
        help: "PO/Clerk application assistance",
        documents: ["Photo & signature", "Education certificates", "ID proof"],
        link: ""
      },
      "railways": {
        title: "Railway Recruitment (RRB)",
        help: "RRB application & document help",
        documents: ["Photo & signature", "DOB proof", "Education certificate"],
        link: ""
      },
      "gate": {
        title: "GATE",
        help: "Postgraduate engineering exam registration",
        documents: ["Photo & signature", "Degree/provisional certificate", "ID proof"],
        link: "https://gate.iitd.ac.in"
      },
      "others": {
        title: "Other Exams & Admissions",
        help: "State PSCs, Polytechnic, Diploma, College admissions",
        documents: ["Depends on exam — usually DOB proof, education certificates, photo & signature"],
        link: ""
      }
    }
  },

  "scholarships": {
    title: "Scholarship Forms",
    description: "NSP, state scholarships, post-matric & renewal",
    subitems: {
      "nsp": {
        title: "National Scholarship Portal (NSP)",
        help: "Central & state scholarship registration/renewal",
        documents: ["Aadhaar", "Bank passbook copy", "Admission certificate / fee receipt", "Income certificate if required"],
        link: "https://scholarships.gov.in"
      },
      "state": {
        title: "State Scholarship Forms",
        help: "State-specific post-matric & minority scholarships",
        documents: ["Income certificate", "Caste certificate (if applicable)", "Marksheets", "Bank details"],
        link: ""
      }
    }
  },

  "printing": {
    title: "Print / Scan / Stationery",
    description: "Printing, photocopy, lamination, stationery items",
    subitems: {
      "print": { title: "Printing & Photocopy", help: "A4/Legal, color/black-white prints, booklets", documents: ["Bring digital file (USB/WhatsApp/Email)"], link:"" },
      "laminate": { title: "Lamination", help: "ID cards, certificates", documents: ["Physical document"], link:"" },
      "stationery": { title: "Stationery Items", help: "Pens, registers, files, ink cartridges", documents: ["—"], link:"" }
    }
  },

  "classes": {
    title: "Classes & Training",
    description: "Typing, Graphic design, Photoshop, Video editing, Internships",
    subitems: {
      "typing": { title: "Typing Classes (Hindi/English)", help: "Beginner to advanced typing, certificate", documents: ["ID proof (Aadhaar) for enrollment"], link:"" },
      "graphic": { title: "Graphic Designing Class", help: "Corel/Illustrator/Canva basics to advanced", documents: ["ID proof, portfolio if any"], link:"" },
      "photoshop": { title: "Photoshop Expert Class", help: "Retouching, compositing, thumbnails", documents: ["ID proof"], link:"" },
      "video": { title: "Video Editing Class", help: "Filmora/Premiere/DaVinci editing", documents: ["ID proof, pen & notebook"], link:"" },
      "intern": { title: "Internships (Design / IT / Editing)", help: "Short-term internships & projects", documents: ["Resume (if any), ID proof"], link:"" },
      "computerlab": { title: "Computer Lab & Project Help", help: "Hourly PC use, project assistance, printing", documents: ["Bring digital work / files"], link:"" }
    }
  },

  "government": {
    title: "All Govt. Work",
    description: "Aadhaar, PAN, certificates, RTI help",
    subitems: {
      "aadhaar": { title: "Aadhaar Services", help: "Enrollment / Update / Print Aadhar", documents: ["Original ID proof (Aadhaar-related)","Passport-size photo if needed"], link:"" },
      "pan": { title: "PAN Card", help: "Apply new PAN / Correction / e-KYC", documents: ["Aadhaar/ID proof, Address proof, Photo"], link:"" },
      "cert": { title: "Caste / Income / Domicile Certificates", help: "Apply & print state certificates", documents: ["ID, Address, Income proofs (as required)"], link:"" }
    }
  },

  "money": {
    title: "Money Transfer & Payments",
    description: "UPI, IMPS, NEFT, Bill payments, Recharges",
    subitems: {
      "upi": { title: "UPI / Bank Transfers", help: "Send money, receive, link UPI", documents: ["Sender's ID proof if bank requires"], link:"" },
      "bills": { title: "Bill Payment / Recharge", help: "Electricity, Water, Mobile & DTH", documents: ["Consumer number / bill copy"], link:"" }
    }
  }
};

/* ---------------- UI logic ---------------- */
const servicesGrid = document.getElementById('services-grid');
const modalRoot = document.getElementById('modal-root');

function renderServiceCards(filter='') {
  servicesGrid.innerHTML = '';
  Object.keys(servicesData).forEach(key => {
    const s = servicesData[key];
    const title = s.title || key;
    const desc = s.description || '';
    // filter
    if (filter) {
      const hay = (title + ' ' + desc + ' ' + JSON.stringify(s.subitems || {})).toLowerCase();
      if (!hay.includes(filter.toLowerCase())) return;
    }
    const card = document.createElement('div');
    card.className = 'bg-white p-4 rounded shadow service-item hover:shadow-lg';
    card.innerHTML = `<h3 class="font-semibold">${title}</h3><p class="small-muted mt-1 text-sm">${desc}</p>`;
    card.addEventListener('click', () => openServiceModal(key));
    servicesGrid.appendChild(card);
  });
}
renderServiceCards();

document.getElementById('global-search').addEventListener('input', (e) => renderServiceCards(e.target.value));

// modal builder
function openServiceModal(serviceKey) {
  const service = servicesData[serviceKey];
  if (!service) return;
  modalRoot.innerHTML = `
  <div class="modal-backdrop" id="modal-backdrop">
    <div class="modal">
      <div class="flex justify-between items-start">
        <div>
          <h2 class="text-xl font-bold">${service.title}</h2>
          <p class="small-muted mt-1">${service.description || ''}</p>
        </div>
        <div><button id="close-modal" class="text-gray-600">Close ✖</button></div>
      </div>

      <div class="mt-4 grid md:grid-cols-2 gap-3" id="subitems-root"></div>

      <div id="doc-panel" class="mt-4 bg-gray-50 border p-3 rounded hidden">
        <h3 class="font-semibold" id="doc-title">Title</h3>
        <p class="small-muted" id="doc-help"></p>
        <ul class="list-disc list-inside mt-2" id="doc-list"></ul>
        <div id="doc-link" class="mt-3"></div>
      </div>
    </div>
  </div>
  `;
  modalRoot.classList.remove('hidden');

  // populate subitems
  const subRoot = document.getElementById('subitems-root');
  const subitems = service.subitems || {};
  Object.keys(subitems).forEach(subKey => {
    const sub = subitems[subKey];
    const el = document.createElement('div');
    el.className = 'p-3 border rounded subitem hover:bg-gray-50';
    el.innerHTML = `<h4 class="font-medium">${sub.title}</h4><p class="small-muted mt-1">${sub.help || ''}</p>`;
    el.addEventListener('click', () => showDocuments(sub));
    subRoot.appendChild(el);
  });

  // close events
  document.getElementById('close-modal').addEventListener('click', closeModal);
  document.getElementById('modal-backdrop').addEventListener('click', (ev) => {
    if (ev.target.id === 'modal-backdrop') closeModal();
  });
}

function closeModal() {
  modalRoot.innerHTML = '';
  modalRoot.classList.add('hidden');
}

function showDocuments(subitem) {
  const panel = document.getElementById('doc-panel');
  document.getElementById('doc-title').textContent = subitem.title || 'Details';
  document.getElementById('doc-help').textContent = subitem.help || '';
  const ul = document.getElementById('doc-list'); ul.innerHTML = '';
  (subitem.documents || []).forEach(d => {
    const li = document.createElement('li'); li.textContent = d; ul.appendChild(li);
  });
  const docLink = document.getElementById('doc-link'); docLink.innerHTML = '';
  if (subitem.link) {
    const a = document.createElement('a'); a.href = subitem.link; a.target='_blank'; a.className='text-blue-600 hover:underline';
    a.textContent = 'Official Link / Apply Here';
    docLink.appendChild(a);
  }
  panel.classList.remove('hidden');
  panel.scrollIntoView({behavior:'smooth'});
}

/* ---------------- AI Helper (local search) ---------------- */
const aiBtn = document.getElementById('ai-btn');
aiBtn.addEventListener('click', () => {
  const q = document.getElementById('ai-prompt').value.trim().toLowerCase();
  const out = document.getElementById('ai-output');
  out.innerHTML = ''; out.classList.add('hidden');
  if (!q) { out.textContent = 'Please enter a task.'; out.classList.remove('hidden'); return; }
  // search over servicesData
  let found = false;
  for (const sk of Object.keys(servicesData)) {
    const s = servicesData[sk];
    if ((s.title || '').toLowerCase().includes(q) || (s.description || '').toLowerCase().includes(q) || JSON.stringify(s).toLowerCase().includes(q)) {
      out.innerHTML = `<strong>${s.title}</strong><div class="small-muted mt-1">${s.description || ''}</div>`;
      const subs = Object.values(s.subitems || {});
      subs.slice(0, 15).forEach(si => {
        out.innerHTML += `<div class="mt-2"><em>${si.title}</em> — ${si.help || ''} <button data-service="${sk}" data-sub="${si.title}" style="margin-left:8px;padding:4px 8px;background:#2563eb;color:#fff;border-radius:6px;border:none;cursor:pointer;">View Docs</button></div>`;
      });
      found = true; break;
    }
  }
  if (!found) out.textContent = 'Koi matching service nahi mila. Try keywords like "JEE", "IRCTC", "Scholarship".';
  out.classList.remove('hidden');

  // attach listeners for generated buttons
  out.querySelectorAll('button[data-service]').forEach(btn => {
    btn.addEventListener('click', (e) => {
      const serviceKey = e.target.getAttribute('data-service');
      const subTitle = e.target.getAttribute('data-sub');
      const s = servicesData[serviceKey];
      const sub = Object.values(s.subitems || {}).find(x => x.title === subTitle);
      if (sub) {
        openServiceModal(serviceKey);
        setTimeout(()=> {
          const nodes = document.querySelectorAll('#subitems-root .subitem');
          for (const n of nodes) {
            if (n.textContent.trim().startsWith(sub.title)) { n.click(); break; }
          }
        }, 200);
      }
    });
  });
});

/* ---------------- City restriction: client-side (Gonda) ---------------- */
function restrictToGonda() {
  if (!navigator.geolocation) return; // allow if not supported
  navigator.geolocation.getCurrentPosition(pos => {
    const lat = pos.coords.latitude, lon = pos.coords.longitude;
    const gondaLat = 27.13, gondaLon = 81.93;
    function deg2rad(deg){ return deg * (Math.PI/180); }
    function distanceKm(lat1, lon1, lat2, lon2){
      const R = 6371;
      const dLat = deg2rad(lat2 - lat1);
      const dLon = deg2rad(lon2 - lon1);
      const a = Math.sin(dLat/2)*Math.sin(dLat/2) + Math.cos(deg2rad(lat1))*Math.cos(deg2rad(lat2))*Math.sin(dLon/2)*Math.sin(dLon/2);
      const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
      return R * c;
    }
    const dist = distanceKm(lat, lon, gondaLat, gondaLon);
    const allowedRadiusKm = 60; // ~60 km radius
    if (dist > allowedRadiusKm) {
      document.body.innerHTML = `<div class="min-h-screen flex items-center justify-center"><div class="bg-white p-6 rounded shadow text-center"><h2 class="text-xl font-bold">Access Restricted</h2><p class="mt-2">Ye website sirf Gonda (Uttar Pradesh) ke users ke liye available hai. Aapka detected location is region ke bahar hai.</p></div></div>`;
    }
  }, err => {
    // if blocked, show banner allowing user to permit
    console.warn('Location access denied or failed.', err);
    const banner = document.createElement('div');
    banner.className = 'bg-yellow-100 border-l-4 border-yellow-400 text-yellow-700 p-4 fixed top-16 left-4 right-4 z-50';
    banner.innerHTML = `<p><strong>Location required:</strong> Kripya location allow karein taaki hum confirm kar saken ki aap Gonda se ho. (You can still use site but some features may be limited.) <button id="allow-loc" class="ml-4 px-3 py-1 bg-blue-600 text-white rounded">Allow</button></p>`;
    document.body.appendChild(banner);
    document.getElementById('allow-loc').addEventListener('click', () => { banner.remove(); restrictToGonda(); });
  }, { timeout: 8000 });
}
restrictToGonda();

</script>
</body>
</html>
<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Kendra-Krishna Cyber Cafe & Jan Seva Kendra</title>
<script src="https://cdn.tailwindcss.com"></script>
<script>
  tailwind.config = { theme: { extend: { fontFamily: { sans:['Inter','sans-serif'] } } } };
</script>
<style>
/* loader */
.loader { border:4px solid #f3f3f3; border-top:4px solid #3b82f6; border-radius:50%; width:24px; height:24px; animation:spin 1s linear infinite; }
@keyframes spin { 0%{transform:rotate(0deg);}100%{transform:rotate(360deg);} }

/* modal */
.modal-backdrop { background: rgba(0,0,0,0.5); position: fixed; inset:0; display:flex; align-items:center; justify-content:center; z-index:60; }
.modal { width:95%; max-width:1000px; max-height:85vh; overflow:auto; background:white; border-radius:0.5rem; padding:1rem; box-shadow:0 10px 30px rgba(0,0,0,0.2); }
.service-item { cursor:pointer; }
.subitem { cursor:pointer; }
.small-muted { color:#6b7280; font-size:0.92rem; }
.hidden { display:none; }

/* small responsive tweaks */
@media (min-width: 768px) {
  .modal { padding:1.5rem; }
}
</style>
</head>
<body class="bg-gray-100 font-sans text-gray-800">

<!-- Header -->
<header class="bg-white shadow sticky top-0 z-50">
  <nav class="container mx-auto px-4 py-4 flex justify-between items-center">
    <div>
      <a href="#" class="text-2xl font-bold text-blue-600">Kendra-Krishna Cyber Cafe & Jan Seva Kendra</a>
      <div class="small-muted">Patel Nager, Gonda — +91 90444 46667</div>
    </div>
    <div class="flex gap-4 items-center">
      <a href="#services" class="text-sm text-gray-600 hover:text-blue-600">Services</a>
      <a href="#contact" class="text-sm text-gray-600 hover:text-blue-600">Contact</a>
      <a href="#ai-helper" class="text-sm text-gray-600 hover:text-blue-600">AI Helper</a>
    </div>
  </nav>
</header>

<!-- Hero -->
<section class="bg-blue-700 text-white text-center py-12">
  <div class="container mx-auto px-4">
    <h1 class="text-3xl sm:text-4xl font-extrabold">Welcome to Kendra-Krishna Cyber Cafe & Jan Seva Kendra</h1>
    <p class="mt-3 text-lg">A to Z computer & Jan Seva | Classes | Forms | Tickets | Printing | Lab</p>
    <a href="tel:+919044446667" class="inline-block mt-4 bg-white text-blue-700 px-5 py-2 rounded-lg font-bold">Call Now</a>
  </div>
</section>

<!-- Services + Search -->
<section id="services" class="container mx-auto px-4 py-12">
  <div class="flex flex-col md:flex-row md:items-center md:justify-between gap-4 mb-6">
    <h2 class="text-2xl font-bold">Hamari Sevaayein</h2>
    <div class="w-full md:w-1/2">
      <input id="global-search" type="search" placeholder="Search service or form (e.g., JEE, IRCTC, Scholarship...)" class="w-full p-3 rounded border" />
    </div>
  </div>

  <div id="services-grid" class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-4">
    <!-- JS will populate service cards -->
  </div>

  <p class="text-center text-gray-600 mt-6">Click any service to see detailed sub-items & required documents.</p>
</section>

<!-- AI helper (kept minimal) -->
<section id="ai-helper" class="bg-white py-12">
  <div class="container mx-auto px-4 max-w-3xl">
    <h3 class="text-xl font-bold mb-2">Quick Documents Check (Search)</h3>
    <div class="flex gap-2">
      <input id="ai-prompt" type="text" placeholder="Type task (e.g., 'PAN card', 'JEE application')" class="flex-1 p-2 border rounded" />
      <button id="ai-btn" class="bg-blue-600 text-white px-4 py-2 rounded">Check</button>
    </div>
    <div id="ai-output" class="mt-3 p-3 bg-gray-50 border rounded hidden"></div>
  </div>
</section>

<!-- Contact -->
<section id="contact" class="container mx-auto px-4 py-12">
  <div class="grid md:grid-cols-2 gap-6">
    <div class="bg-white p-6 rounded shadow">
      <h3 class="text-lg font-bold">Contact & Info</h3>
      <p class="mt-2"><strong>CSC Holder:</strong> Anoop Kumar Gupta</p>
      <p><strong>Address:</strong> Patel Nager, Gonda, Uttar Pradesh</p>
      <p><strong>Landmark:</strong> Near Gonda Nursing Home and Hospital, old Mohan Lal School</p>
      <p><strong>Phone:</strong> <a href="tel:+919044446667" class="text-blue-600">+91 90444 46667</a></p>
      <p><strong>Hours:</strong> 9am - 9pm (7 days)</p>
    </div>

    <div class="bg-white p-6 rounded shadow">
      <h3 class="text-lg font-bold">Location</h3>
      <div class="mt-3 h-64 overflow-hidden rounded">
        <iframe src="https://maps.app.goo.gl/mjaSMjzMQkqYoBCp7" width="100%" height="100%" style="border:0;"></iframe>
      </div>
    </div>
  </div>
</section>

<!-- Footer -->
<footer class="bg-gray-800 text-gray-200 py-6 mt-8">
  <div class="container mx-auto px-4 text-center">
    &copy; 2025 Kendra-Krishna Cyber Cafe & Jan Seva Kendra
  </div>
</footer>

<!-- Modal (details panel) -->
<div id="modal-root" class="hidden"></div>

<script>
/* ---------------- DATA: servicesData ----------------
   Each service -> subitems -> documents, help, optional link
   Edit/extend as needed.
*/
const servicesData = {
  "tickets": {
    title: "Train & Air Ticket Booking",
    description: "IRCTC, domestic flights, OTA bookings & printing",
    subitems: {
      "irctc": {
        title: "IRCTC (Train ticket)",
        help: "PNR booking, e-ticket print, tatkal support",
        documents: ["Valid Photo ID (Aadhaar/Passport/Voter ID/Driving Licence)", "Mobile number linked to ID for OTP", "Payment method (card/UPI)"],
        link: "https://www.irctc.co.in"
      },
      "air": {
        title: "Air Ticket (Domestic)",
        help: "Flight booking & print boarding pass",
        documents: ["Valid Photo ID (Aadhaar/Passport)", "E-mail & Mobile for PNR", "Payment method"],
        link: ""
      },
      "ota": {
        title: "Online Travel Agents",
        help: "MakeMyTrip, Goibibo booking help",
        documents: ["Photo ID for check-in", "Payment method"],
        link: ""
      }
    }
  },

  "forms": {
    title: "Exam & Application Forms",
    description: "JEE, NEET, Board, UPSC, SSC, Bank, GATE and more",
    subitems: {
      "jee-main": {
        title: "JEE Main",
        help: "NTA engineering entrance",
        documents: ["DOB proof (Class 10 certificate)", "Class 12 mark sheet / passing certificate", "Photograph & signature (as per specs)", "ID proof (Aadhaar/Passport)"],
        link: "https://jeemain.nta.nic.in"
      },
      "jee-adv": {
        title: "JEE Advanced",
        help: "IIT entrance (after JEE Main rank)",
        documents: ["JEE Main score/admit card", "Photograph & signature", "Class 12 certificate"],
        link: "https://jeeadv.ac.in"
      },
      "neet": {
        title: "NEET (UG)",
        help: "Medical entrance (NTA)",
        documents: ["Class 10 (DOB proof)", "Class 12 marksheet/passing certificate", "Photo & signature", "ID proof"],
        link: "https://neet.nta.nic.in"
      },
      "up-board": {
        title: "State Board (UP Board) Exams",
        help: "10th/12th board related forms & corrections",
        documents: ["School details, DOB proof, previous marksheet", "Passport-size photo"],
        link: ""
      },
      "upsc": {
        title: "UPSC (CSE)",
        help: "Civil Services preliminary & mains applications",
        documents: ["Photo & signature", "Educational certificates for certain posts", "Category certificate if applicable"],
        link: "https://upsconline.nic.in"
      },
      "ssc": {
        title: "SSC (CGL/CHSL etc.)",
        help: "Central government recruitment",
        documents: ["Matriculation (DOB proof)", "Education certificates", "Photo & signature"],
        link: "https://ssc.nic.in"
      },
      "bank": {
        title: "Bank Exams (IBPS/SBI)",
        help: "PO/Clerk application assistance",
        documents: ["Photo & signature", "Education certificates", "ID proof"],
        link: ""
      },
      "railways": {
        title: "Railway Recruitment (RRB)",
        help: "RRB application & document help",
        documents: ["Photo & signature", "DOB proof", "Education certificate"],
        link: ""
      },
      "gate": {
        title: "GATE",
        help: "Postgraduate engineering exam registration",
        documents: ["Photo & signature", "Degree/provisional certificate", "ID proof"],
        link: "https://gate.iitd.ac.in"
      },
      "others": {
        title: "Other Exams & Admissions",
        help: "State PSCs, Polytechnic, Diploma, College admissions",
        documents: ["Depends on exam — usually DOB proof, education certificates, photo & signature"],
        link: ""
      }
    }
  },

  "scholarships": {
    title: "Scholarship Forms",
    description: "NSP, state scholarships, post-matric & renewal",
    subitems: {
      "nsp": {
        title: "National Scholarship Portal (NSP)",
        help: "Central & state scholarship registration/renewal",
        documents: ["Aadhaar", "Bank passbook copy", "Admission certificate / fee receipt", "Income certificate if required"],
        link: "https://scholarships.gov.in"
      },
      "state": {
        title: "State Scholarship Forms",
        help: "State-specific post-matric & minority scholarships",
        documents: ["Income certificate", "Caste certificate (if applicable)", "Marksheets", "Bank details"],
        link: ""
      }
    }
  },

  "printing": {
    title: "Print / Scan / Stationery",
    description: "Printing, photocopy, lamination, stationery items",
    subitems: {
      "print": { title: "Printing & Photocopy", help: "A4/Legal, color/black-white prints, booklets", documents: ["Bring digital file (USB/WhatsApp/Email)"], link:"" },
      "laminate": { title: "Lamination", help: "ID cards, certificates", documents: ["Physical document"], link:"" },
      "stationery": { title: "Stationery Items", help: "Pens, registers, files, ink cartridges", documents: ["—"], link:"" }
    }
  },

  "classes": {
    title: "Classes & Training",
    description: "Typing, Graphic design, Photoshop, Video editing, Internships",
    subitems: {
      "typing": { title: "Typing Classes (Hindi/English)", help: "Beginner to advanced typing, certificate", documents: ["ID proof (Aadhaar) for enrollment"], link:"" },
      "graphic": { title: "Graphic Designing Class", help: "Corel/Illustrator/Canva basics to advanced", documents: ["ID proof, portfolio if any"], link:"" },
      "photoshop": { title: "Photoshop Expert Class", help: "Retouching, compositing, thumbnails", documents: ["ID proof"], link:"" },
      "video": { title: "Video Editing Class", help: "Filmora/Premiere/DaVinci editing", documents: ["ID proof, pen & notebook"], link:"" },
      "intern": { title: "Internships (Design / IT / Editing)", help: "Short-term internships & projects", documents: ["Resume (if any), ID proof"], link:"" },
      "computerlab": { title: "Computer Lab & Project Help", help: "Hourly PC use, project assistance, printing", documents: ["Bring digital work / files"], link:"" }
    }
  },

  "government": {
    title: "All Govt. Work",
    description: "Aadhaar, PAN, certificates, RTI help",
    subitems: {
      "aadhaar": { title: "Aadhaar Services", help: "Enrollment / Update / Print Aadhar", documents: ["Original ID proof (Aadhaar-related)","Passport-size photo if needed"], link:"" },
      "pan": { title: "PAN Card", help: "Apply new PAN / Correction / e-KYC", documents: ["Aadhaar/ID proof, Address proof, Photo"], link:"" },
      "cert": { title: "Caste / Income / Domicile Certificates", help: "Apply & print state certificates", documents: ["ID, Address, Income proofs (as required)"], link:"" }
    }
  },

  "money": {
    title: "Money Transfer & Payments",
    description: "UPI, IMPS, NEFT, Bill payments, Recharges",
    subitems: {
      "upi": { title: "UPI / Bank Transfers", help: "Send money, receive, link UPI", documents: ["Sender's ID proof if bank requires"], link:"" },
      "bills": { title: "Bill Payment / Recharge", help: "Electricity, Water, Mobile & DTH", documents: ["Consumer number / bill copy"], link:"" }
    }
  }
};

/* ---------------- UI logic ---------------- */
const servicesGrid = document.getElementById('services-grid');
const modalRoot = document.getElementById('modal-root');

function renderServiceCards(filter='') {
  servicesGrid.innerHTML = '';
  Object.keys(servicesData).forEach(key => {
    const s = servicesData[key];
    const title = s.title || key;
    const desc = s.description || '';
    // filter
    if (filter) {
      const hay = (title + ' ' + desc + ' ' + JSON.stringify(s.subitems || {})).toLowerCase();
      if (!hay.includes(filter.toLowerCase())) return;
    }
    const card = document.createElement('div');
    card.className = 'bg-white p-4 rounded shadow service-item hover:shadow-lg';
    card.innerHTML = `<h3 class="font-semibold">${title}</h3><p class="small-muted mt-1 text-sm">${desc}</p>`;
    card.addEventListener('click', () => openServiceModal(key));
    servicesGrid.appendChild(card);
  });
}
renderServiceCards();

document.getElementById('global-search').addEventListener('input', (e) => renderServiceCards(e.target.value));

// modal builder
function openServiceModal(serviceKey) {
  const service = servicesData[serviceKey];
  if (!service) return;
  modalRoot.innerHTML = `
  <div class="modal-backdrop" id="modal-backdrop">
    <div class="modal">
      <div class="flex justify-between items-start">
        <div>
          <h2 class="text-xl font-bold">${service.title}</h2>
          <p class="small-muted mt-1">${service.description || ''}</p>
        </div>
        <div><button id="close-modal" class="text-gray-600">Close ✖</button></div>
      </div>

      <div class="mt-4 grid md:grid-cols-2 gap-3" id="subitems-root"></div>

      <div id="doc-panel" class="mt-4 bg-gray-50 border p-3 rounded hidden">
        <h3 class="font-semibold" id="doc-title">Title</h3>
        <p class="small-muted" id="doc-help"></p>
        <ul class="list-disc list-inside mt-2" id="doc-list"></ul>
        <div id="doc-link" class="mt-3"></div>
      </div>
    </div>
  </div>
  `;
  modalRoot.classList.remove('hidden');

  // populate subitems
  const subRoot = document.getElementById('subitems-root');
  const subitems = service.subitems || {};
  Object.keys(subitems).forEach(subKey => {
    const sub = subitems[subKey];
    const el = document.createElement('div');
    el.className = 'p-3 border rounded subitem hover:bg-gray-50';
    el.innerHTML = `<h4 class="font-medium">${sub.title}</h4><p class="small-muted mt-1">${sub.help || ''}</p>`;
    el.addEventListener('click', () => showDocuments(sub));
    subRoot.appendChild(el);
  });

  // close events
  document.getElementById('close-modal').addEventListener('click', closeModal);
  document.getElementById('modal-backdrop').addEventListener('click', (ev) => {
    if (ev.target.id === 'modal-backdrop') closeModal();
  });
}

function closeModal() {
  modalRoot.innerHTML = '';
  modalRoot.classList.add('hidden');
}

function showDocuments(subitem) {
  const panel = document.getElementById('doc-panel');
  document.getElementById('doc-title').textContent = subitem.title || 'Details';
  document.getElementById('doc-help').textContent = subitem.help || '';
  const ul = document.getElementById('doc-list'); ul.innerHTML = '';
  (subitem.documents || []).forEach(d => {
    const li = document.createElement('li'); li.textContent = d; ul.appendChild(li);
  });
  const docLink = document.getElementById('doc-link'); docLink.innerHTML = '';
  if (subitem.link) {
    const a = document.createElement('a'); a.href = subitem.link; a.target='_blank'; a.className='text-blue-600 hover:underline';
    a.textContent = 'Official Link / Apply Here';
    docLink.appendChild(a);
  }
  panel.classList.remove('hidden');
  panel.scrollIntoView({behavior:'smooth'});
}

/* ---------------- AI Helper (local search) ---------------- */
const aiBtn = document.getElementById('ai-btn');
aiBtn.addEventListener('click', () => {
  const q = document.getElementById('ai-prompt').value.trim().toLowerCase();
  const out = document.getElementById('ai-output');
  out.innerHTML = ''; out.classList.add('hidden');
  if (!q) { out.textContent = 'Please enter a task.'; out.classList.remove('hidden'); return; }
  // search over servicesData
  let found = false;
  for (const sk of Object.keys(servicesData)) {
    const s = servicesData[sk];
    if ((s.title || '').toLowerCase().includes(q) || (s.description || '').toLowerCase().includes(q) || JSON.stringify(s).toLowerCase().includes(q)) {
      out.innerHTML = `<strong>${s.title}</strong><div class="small-muted mt-1">${s.description || ''}</div>`;
      const subs = Object.values(s.subitems || {});
      subs.slice(0, 15).forEach(si => {
        out.innerHTML += `<div class="mt-2"><em>${si.title}</em> — ${si.help || ''} <button data-service="${sk}" data-sub="${si.title}" style="margin-left:8px;padding:4px 8px;background:#2563eb;color:#fff;border-radius:6px;border:none;cursor:pointer;">View Docs</button></div>`;
      });
      found = true; break;
    }
  }
  if (!found) out.textContent = 'Koi matching service nahi mila. Try keywords like "JEE", "IRCTC", "Scholarship".';
  out.classList.remove('hidden');

  // attach listeners for generated buttons
  out.querySelectorAll('button[data-service]').forEach(btn => {
    btn.addEventListener('click', (e) => {
      const serviceKey = e.target.getAttribute('data-service');
      const subTitle = e.target.getAttribute('data-sub');
      const s = servicesData[serviceKey];
      const sub = Object.values(s.subitems || {}).find(x => x.title === subTitle);
      if (sub) {
        openServiceModal(serviceKey);
        setTimeout(()=> {
          const nodes = document.querySelectorAll('#subitems-root .subitem');
          for (const n of nodes) {
            if (n.textContent.trim().startsWith(sub.title)) { n.click(); break; }
          }
        }, 200);
      }
    });
  });
});

/* ---------------- City restriction: client-side (Gonda) ---------------- */
function restrictToGonda() {
  if (!navigator.geolocation) return; // allow if not supported
  navigator.geolocation.getCurrentPosition(pos => {
    const lat = pos.coords.latitude, lon = pos.coords.longitude;
    const gondaLat = 27.13, gondaLon = 81.93;
    function deg2rad(deg){ return deg * (Math.PI/180); }
    function distanceKm(lat1, lon1, lat2, lon2){
      const R = 6371;
      const dLat = deg2rad(lat2 - lat1);
      const dLon = deg2rad(lon2 - lon1);
      const a = Math.sin(dLat/2)*Math.sin(dLat/2) + Math.cos(deg2rad(lat1))*Math.cos(deg2rad(lat2))*Math.sin(dLon/2)*Math.sin(dLon/2);
      const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
      return R * c;
    }
    const dist = distanceKm(lat, lon, gondaLat, gondaLon);
    const allowedRadiusKm = 60; // ~60 km radius
    if (dist > allowedRadiusKm) {
      document.body.innerHTML = `<div class="min-h-screen flex items-center justify-center"><div class="bg-white p-6 rounded shadow text-center"><h2 class="text-xl font-bold">Access Restricted</h2><p class="mt-2">Ye website sirf Gonda (Uttar Pradesh) ke users ke liye available hai. Aapka detected location is region ke bahar hai.</p></div></div>`;
    }
  }, err => {
    // if blocked, show banner allowing user to permit
    console.warn('Location access denied or failed.', err);
    const banner = document.createElement('div');
    banner.className = 'bg-yellow-100 border-l-4 border-yellow-400 text-yellow-700 p-4 fixed top-16 left-4 right-4 z-50';
    banner.innerHTML = `<p><strong>Location required:</strong> Kripya location allow karein taaki hum confirm kar saken ki aap Gonda se ho. (You can still use site but some features may be limited.) <button id="allow-loc" class="ml-4 px-3 py-1 bg-blue-600 text-white rounded">Allow</button></p>`;
    document.body.appendChild(banner);
    document.getElementById('allow-loc').addEventListener('click', () => { banner.remove(); restrictToGonda(); });
  }, { timeout: 8000 });
}
restrictToGonda();

</script>
</body>
</html>
