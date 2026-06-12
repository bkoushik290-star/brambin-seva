<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PujaConnect - ব্রাহ্মণ সেবা ও বুকিং প্ল্যাটফর্ম</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Hind+Siliguri:wght@400;500;600;700&family=Poppins:wght@300;400;500;600&display=swap');
        
        body {
            font-family: 'Hind Siliguri', 'Poppins', sans-serif;
            background-color: #FFFDF9;
        }
        .bg-puja-orange {
            background-color: #E65100;
        }
        .bg-puja-dark {
            background-color: #26140A;
        }
        .text-puja-orange {
            color: #E65100;
        }
        .border-puja-orange {
            borderColor: #E65100;
        }
        .swastik-bg {
            background-image: radial-gradient(#FFEB3B 1px, transparent 1px);
            background-size: 20px 20px;
            background-opacity: 0.05;
        }
    </style>
</head>
<body class="max-w-md mx-auto min-h-screen shadow-2xl relative bg-[#FFFDF9] pb-24">

    <!-- TOP BAR (Language Selection) -->
    <header class="p-4 bg-[#FFFDF9] border-b border-orange-100 sticky top-0 z-50 shadow-sm">
        <div class="flex justify-between items-center">
            <div class="flex items-center space-x-2">
                <span class="text-3xl text-puja-orange font-bold">🕉️</span>
                <div>
                    <h1 class="text-2xl font-bold tracking-tight text-puja-dark">PujaConnect</h1>
                    <p id="app-subtitle" class="text-xs text-gray-500 font-medium">পূজো সেবা ও বুকিং প্ল্যাটফর্ম</p>
                </div>
            </div>
            
            <!-- Language Dropdown -->
            <div class="relative">
                <select id="lang-selector" onchange="changeLanguage(this.value)" class="bg-orange-50 border border-orange-200 text-puja-dark rounded-full px-3 py-1 text-xs font-semibold focus:outline-none focus:ring-1 focus:ring-orange-500">
                    <option value="bn">🎯 বাংলা</option>
                    <option value="en">🇬🇧 English</option>
                    <option value="hi">🇮🇳 हिन्दी</option>
                    <option value="sa">🔱 संस्कृतम्</option>
                </select>
            </div>
        </div>
    </header>

    <!-- TAB NAVIGATION (Inspired by Screenshot_20260612-104559_Claude.jpg) -->
    <div class="px-4 py-3">
        <div class="bg-puja-dark p-1 rounded-xl flex">
            <button id="tab-purohit" onclick="switchTab('purohit')" class="w-1/2 bg-puja-orange text-white py-2.5 px-4 rounded-lg font-bold text-sm transition-all flex items-center justify-center space-x-2">
                <span>🙏</span> <span id="text-tab-purohit">পুরোহিত প্রোফাইল</span>
            </button>
            <button id="tab-features" onclick="switchTab('features')" class="w-1/2 text-orange-200 hover:text-white py-2.5 px-4 rounded-lg font-bold text-sm transition-all flex items-center justify-center space-x-2">
                <span>🔱</span> <span id="text-tab-features">সেবা ও পঞ্জিকা</span>
            </button>
        </div>
    </div>

    <!-- MAIN CONTENT AREA -->
    <main class="px-4">
        
        <!-- SECTION 1: PUROHIT PROFILES -->
        <div id="section-purohit" class="space-y-4">
            
            <!-- Dynamic Profile Generator (Create New Profile) -->
            <div class="bg-orange-50 border border-orange-100 rounded-2xl p-4 shadow-sm">
                <button onclick="toggleProfileForm()" class="w-full flex justify-between items-center font-bold text-puja-dark text-sm">
                    <span id="text-create-title"><i class="fa-solid fa-user-plus mr-1 text-puja-orange"></i> নতুন পুরোহিত প্রোফাইল তৈরি করুন</span>
                    <i id="form-chevron" class="fa-solid fa-chevron-down text-xs"></i>
                </button>
                
                <form id="profile-form" class="mt-4 space-y-3 hidden" onsubmit="saveProfile(event)">
                    <div>
                        <label id="lbl-name" class="block text-xs font-bold text-gray-600 mb-1">পুরোহিতের নাম</label>
                        <input type="text" id="p-name" required placeholder="উদা: পণ্ডিত রামকৃষ্ণ শাস্ত্রী" class="w-full text-sm p-2 rounded-lg border border-orange-200 focus:outline-none focus:border-orange-500">
                    </div>
                    <div class="grid grid-cols-2 gap-2">
                        <div>
                            <label id="lbl-degree" class="block text-xs font-bold text-gray-600 mb-1">যোগ্যতা / ডিগ্রি</label>
                            <input type="text" id="p-degree" required placeholder="উদা: বেদান্ত বিশারদ" class="w-full text-sm p-2 rounded-lg border border-orange-200 focus:outline-none focus:border-orange-500">
                        </div>
                        <div>
                            <label id="lbl-exp" class="block text-xs font-bold text-gray-600 mb-1">অভিজ্ঞতা (বছর)</label>
                            <input type="number" id="p-exp" required placeholder="উদা: ২৫" class="w-full text-sm p-2 rounded-lg border border-orange-200 focus:outline-none focus:border-orange-500">
                        </div>
                    </div>
                    <div class="grid grid-cols-2 gap-2">
                        <div>
                            <label id="lbl-fees" class="block text-xs font-bold text-gray-600 mb-1">ন্যূনতম দক্ষিণা (₹)</label>
                            <input type="number" id="p-fees" required placeholder="উদা: ১৫০১" class="w-full text-sm p-2 rounded-lg border border-orange-200 focus:outline-none focus:border-orange-500">
                        </div>
                        <div>
                            <label id="lbl-loc" class="block text-xs font-bold text-gray-600 mb-1">অবস্থান / জেলা</label>
                            <input type="text" id="p-loc" required placeholder="উদা: কলকাতা, পশ্চিমবঙ্গ" class="w-full text-sm p-2 rounded-lg border border-orange-200 focus:outline-none focus:border-orange-500">
                        </div>
                    </div>
                    <button type="submit" id="btn-submit-profile" class="w-full bg-puja-dark text-white font-bold py-2 text-xs rounded-lg uppercase tracking-wider">প্রোফাইল লাইভ করুন</button>
                </form>
            </div>

            <!-- Profile Cards List (Replicating Screenshot_20260612-104559_Claude.jpg exactly) -->
            <div id="profiles-container" class="space-y-4">
                <!-- JavaScript will populate profiles here -->
            </div>
        </div>

        <!-- SECTION 2: SERVICES, PANJIKA & HIGHLY CUSTOMIZED DONATION -->
        <div id="section-features" class="space-y-6 hidden">
            
            <!-- BRIEF PANJIKA ALMANAC -->
            <div class="bg-gradient-to-br from-amber-50 to-orange-100 border border-orange-200 rounded-2xl p-4 shadow-sm">
                <div class="flex items-center space-x-2 border-b border-orange-200 pb-2 mb-3">
                    <span class="text-xl">📅</span>
                    <h3 id="panjika-header" class="font-bold text-puja-dark">সংক্ষেপে আজকের পঞ্জিকা</h3>
                </div>
                <div class="grid grid-cols-2 gap-3 text-xs">
                    <div class="bg-white/80 p-2 rounded-lg border border-orange-100">
                        <span id="panjika-date-lbl" class="text-gray-500 block">তারিখ ও বার:</span>
                        <strong id="panjika-date" class="text-puja-dark">১২ জুন, ২০২৬ | শুক্রবার</strong>
                    </div>
                    <div class="bg-white/80 p-2 rounded-lg border border-orange-100">
                        <span id="panjika-tithi-lbl" class="text-gray-500 block">তিথি:</span>
                        <strong id="panjika-tithi" class="text-puja-dark">কৃষ্ণাদ্বাদশীতিথি</strong>
                    </div>
                    <div class="bg-white/80 p-2 rounded-lg border border-orange-100">
                        <span id="panjika-nakshatra-lbl" class="text-gray-500 block">নক্ষত্র:</span>
                        <strong id="panjika-nakshatra" class="text-puja-dark">ভরনী নক্ষত্র</strong>
                    </div>
                    <div class="bg-white/80 p-2 rounded-lg border border-orange-100">
                        <span id="panjika-muhurta-lbl" class="text-gray-500 block">শুভ মুহূর্ত:</span>
                        <strong id="panjika-muhurta" class="text-[#2E7D32]">সকাল ০৫:২৪ - সকাল ০৭:১১</strong>
                    </div>
                </div>
            </div>

            <!-- DIGITAL DONATION WITH SPECIFIC CATEGORIES -->
            <div class="bg-white border border-orange-100 rounded-2xl p-4 shadow-sm">
                <div class="flex items-center space-x-2 border-b border-orange-100 pb-2 mb-4">
                    <span class="text-xl text-puja-orange">💳</span>
                    <h3 id="donation-header" class="font-bold text-puja-dark">ডিজিটাল দান ও কল্যাণ তহবিল</h3>
                </div>

                <!-- Donation Categories Form Card -->
                <form onsubmit="handleDonation(event)" class="space-y-4">
                    <div>
                        <label id="lbl-don-cat" class="block text-xs font-bold text-gray-700 mb-1.5">দানের খাত/ক্যাটাগরি নির্বাচন করুন:</label>
                        <div class="space-y-2">
                            <label class="flex items-start p-2.5 rounded-xl border border-orange-100 hover:bg-orange-50/50 cursor-pointer transition-all">
                                <input type="radio" name="don_category" value="cat_1" checked class="mt-1 accent-orange-600">
                                <span id="don-cat-1" class="ml-2.5 text-xs font-medium text-gray-800 leading-relaxed">১. নব উপনীত ব্রাহ্মণদের শিক্ষার ব্যবস্থা উন্নত করতে দান</span>
                            </label>
                            <label class="flex items-start p-2.5 rounded-xl border border-orange-100 hover:bg-orange-50/50 cursor-pointer transition-all">
                                <input type="radio" name="don_category" value="cat_2" class="mt-1 accent-orange-600">
                                <span id="don-cat-2" class="ml-2.5 text-xs font-medium text-gray-800 leading-relaxed">২. গণ বিবাহের জন্য যৌথ দান</span>
                            </label>
                            <label class="flex items-start p-2.5 rounded-xl border border-orange-100 hover:bg-orange-50/50 cursor-pointer transition-all">
                                <input type="radio" name="don_category" value="cat_3" class="mt-1 accent-orange-600">
                                <span id="don-cat-3" class="ml-2.5 text-xs font-medium text-gray-800 leading-relaxed">৩. গণ উপনয়নের আয়োজন ও সহায়তায় দান</span>
                            </label>
                            <label class="flex items-start p-2.5 rounded-xl border border-orange-100 hover:bg-orange-50/50 cursor-pointer transition-all">
                                <input type="radio" name="don_category" value="cat_4" class="mt-1 accent-orange-600">
                                <span id="don-cat-4" class="ml-2.5 text-xs font-medium text-gray-800 leading-relaxed">৪. মন্দির বাস্তবায়নের (নির্মাণ ও সংস্কার) জন্যে দান</span>
                            </label>
                            <label class="flex items-start p-2.5 rounded-xl border border-orange-100 hover:bg-orange-50/50 cursor-pointer transition-all">
                                <input type="radio" name="don_category" value="cat_5" class="mt-1 accent-orange-600">
                                <span id="don-cat-5" class="ml-2.5 text-xs font-medium text-gray-800 leading-relaxed">৫. বিশেষ মনস্কামনা পূরণে সংকল্পের দান</span>
                            </label>
                        </div>
                    </div>

                    <!-- Donor Details Form -->
                    <div class="grid grid-cols-2 gap-2 pt-2">
                        <div>
                            <label id="lbl-don-name" class="block text-xs font-bold text-gray-600 mb-1">দাতার নাম</label>
                            <input type="text" id="don-name" required placeholder="উদা: সৌমেন চ্যাটার্জী" class="w-full text-xs p-2 rounded-lg border border-orange-200 focus:outline-none focus:border-orange-500">
                        </div>
                        <div>
                            <label id="lbl-don-gotra" class="block text-xs font-bold text-gray-600 mb-1">গোত্র</label>
                            <input type="text" id="don-gotra" required placeholder="উদা: শাণ্ডিল্য" class="w-full text-xs p-2 rounded-lg border border-orange-200 focus:outline-none focus:border-orange-500">
                        </div>
                    </div>

                    <div>
                        <label id="lbl-don-amount" class="block text-xs font-bold text-gray-600 mb-1">দানের পরিমাণ (₹)</label>
                        <input type="number" id="don-amount" required placeholder="উদা: ৫০১" min="1" class="w-full text-xs p-2 rounded-lg border border-orange-200 focus:outline-none focus:border-orange-500">
                    </div>

                    <button type="submit" id="btn-donate" class="w-full bg-puja-orange hover:bg-orange-700 text-white font-bold py-2.5 text-sm rounded-xl transition-all shadow-sm flex items-center justify-center space-x-2">
                        <i class="fa-solid fa-hands-praying"></i>
                        <span id="txt-btn-donate">ডিজিটাল সংকল্প ও দান করুন</span>
                    </button>
                </form>
            </div>
        </div>

    </main>

    <!-- BOOKING MODAL DIALOG -->
    <div id="booking-modal" class="fixed inset-0 bg-black/50 z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl w-full max-w-sm p-5 space-y-4 shadow-xl">
            <div class="flex justify-between items-center border-b pb-2">
                <h4 id="modal-title" class="font-bold text-puja-dark">পূজা সেবা বুকিং ফর্ম</h4>
                <button onclick="closeBookingModal()" class="text-gray-400 hover:text-gray-600"><i class="fa-solid fa-xmark"></i></button>
            </div>
            <form onsubmit="confirmBooking(event)" class="space-y-3">
                <input type="hidden" id="modal-purohit-id">
                <div>
                    <label id="lbl-book-user" class="block text-xs font-bold text-gray-600 mb-1">আপনার নাম</label>
                    <input type="text" id="b-user" required class="w-full text-sm p-2 rounded-lg border border-orange-200">
                </div>
                <div>
                    <label id="lbl-book-puja" class="block text-xs font-bold text-gray-600 mb-1">পূজার ধরণ / উপলক্ষ্য</label>
                    <input type="text" id="b-puja" required placeholder="উদা: গৃহপ্রবেশ পূজা" class="w-full text-sm p-2 rounded-lg border border-orange-200">
                </div>
                <div>
                    <label id="lbl-book-date" class="block text-xs font-bold text-gray-600 mb-1">পছন্দসই তারিখ</label>
                    <input type="date" id="b-date" required class="w-full text-sm p-2 rounded-lg border border-orange-200">
                </div>
                <button type="submit" id="btn-confirm-booking" class="w-full bg-puja-orange text-white font-bold py-2 rounded-lg text-sm">বুকিং নিশ্চিত করুন</button>
            </form>
        </div>
    </div>

    <!-- FIXED FOOTER ACTIONS (Simulating Chat Input Row from Screenshot_20260612-104559_Claude.jpg) -->
    <footer class="fixed bottom-0 left-0 right-0 max-w-md mx-auto bg-puja-dark p-3 flex items-center justify-between border-t border-orange-950 shadow-2xl z-40">
        <div class="flex items-center space-x-2 bg-[#1F0E06] rounded-full px-4 py-2 w-full border border-orange-900/40">
            <i class="fa-solid fa-plus text-orange-400/70 text-sm cursor-pointer"></i>
            <input type="text" id="footer-search" placeholder="ক্যাটাগরি বা সেবা খুঁজুন..." class="bg-transparent text-white text-xs w-full focus:outline-none placeholder-orange-200/30">
            <i class="fa-solid fa-microphone text-orange-400/70 text-sm cursor-pointer"></i>
        </div>
        <div class="ml-3 bg-puja-orange p-2 rounded-full cursor-pointer hover:bg-orange-600 transition-colors">
            <i class="fa-solid fa-paper-plane text-white text-xs"></i>
        </div>
    </footer>

    <!-- LOCAL DATA & TRANSLATION ENGINE -->
    <script>
        // Language Database
        const localization = {
            bn: {
                subtitle: "পূজো সেবা ও বুকিং প্ল্যাটফর্ম",
                tabPurohit: "পুরोहित প্রোফাইল",
                tabFeatures: "সেবা ও পঞ্জিকা",
                createTitle: "নতুন পুরोहित প্রোফাইল তৈরি করুন",
                lblName: "পুরোহিতের নাম",
                lblDegree: "যোগ্যতা / ডিগ্রি",
                lblExp: "অভিজ্ঞতা (বছর)",
                lblFees: "ন্যূনতম দক্ষিণা (₹)",
                lblLoc: "অবস্থান / জেলা",
                btnSubmitProfile: "প্রোফাইল লাইভ করুন",
                panjikaHeader: "সংক্ষেপে আজকের পঞ্জিকা",
                panjikaDateLbl: "তারিখ ও বার:",
                panjikaDate: "১২ জুন, ২০২৬ | শুক্রবার",
                panjikaTithiLbl: "তিথি:",
                panjikaTithi: "কৃষ্ণাদ্বাদশীতিথি",
                panjikaNakshatraLbl: "নক্ষত্র:",
                panjikaNakshatra: "ভরনী নক্ষত্র",
                panjikaMuhurtaLbl: "শুভ মুহূর্ত:",
                panjikaMuhurta: "সকাল ০৫:২৪ - সকাল ০৭:১১",
                donationHeader: "ডিজিটাল দান ও কল্যাণ তহবিল",
                lblDonCat: "দানের খাত/ক্যাটাগরি নির্বাচন করুন:",
                donCat1: "১. নব উপনীত ব্রাহ্মণদের শিক্ষার ব্যবস্থা উন্নত করতে দান",
                donCat2: "২. গণ বিবাহের জন্য যৌথ দান",
                donCat3: "৩. গণ উপনয়নের আয়োজন ও সহায়তায় দান",
                donCat4: "৪. মন্দির বাস্তবায়নের (নির্মাণ ও সংস্কার) জন্যে দান",
                donCat5: "৫. বিশেষ মনস্কামনা পূরণে সংকল্পের দান",
                lblDonName: "দাতার নাম",
                lblDonGotra: "গোত্র",
                lblDonAmount: "দানের পরিমাণ (₹)",
                btnDonate: "ডিজিটাল সংকল্প ও দান করুন",
                footerPlaceholder: "ক্যাটাগরি বা সেবা খুঁজুন...",
                verified: "✓ যাচাইকৃত",
                experience: "বছরের অভিজ্ঞতা",
                totalPuja: "মোট পূজা",
                rating: "গড় রেটিং",
                reviews: "রিভিউ",
                available: "এখন উপলব্ধ",
                from: "থেকে",
                btnBook: "বুক করুন"
            },
            en: {
                subtitle: "Priest Services & Booking Platform",
                tabPurohit: "Priest Profiles",
                tabFeatures: "Services & Almanac",
                createTitle: "Create New Priest Profile",
                lblName: "Priest's Full Name",
                lblDegree: "Qualification / Degree",
                lblExp: "Experience (Years)",
                lblFees: "Minimum Fees (₹)",
                lblLoc: "Location / District",
                btnSubmitProfile: "Make Profile Live",
                panjikaHeader: "Brief Daily Almanac (Panjika)",
                panjikaDateLbl: "Date & Day:",
                panjikaDate: "12 June, 2026 | Friday",
                panjikaTithiLbl: "Tithi:",
                panjikaTithi: "Krishna Dwadashi",
                panjikaNakshatraLbl: "Nakshatra:",
                panjikaNakshatra: "Bharani Nakshatra",
                panjikaMuhurtaLbl: "Auspicious Muhurta:",
                panjikaMuhurta: "05:24 AM - 07:11 AM",
                donationHeader: "Digital Donation & Welfare Fund",
                lblDonCat: "Select Donation Category:",
                donCat1: "1. Upgrade education facilities for newly initiated Brahmins",
                donCat2: "2. Mass Wedding community donation drive",
                donCat3: "3. Mass Upanayana (Sacred Thread) ceremony support",
                donCat4: "4. Mandir Realization (Construction & Restoration) Fund",
                donCat5: "5. Special Sankalpa Donation for wish fulfillment",
                lblDonName: "Donor's Name",
                lblDonGotra: "Gotra",
                lblDonAmount: "Donation Amount (₹)",
                btnDonate: "Make Digital Sankalpa & Donate",
                footerPlaceholder: "Search categories or services...",
                verified: "✓ Verified",
                experience: "Years Exp",
                totalPuja: "Total Puja",
                rating: "Avg Rating",
                reviews: "Reviews",
                available: "Available Now",
                from: "onwards",
                btnBook: "Book Service"
            },
            hi: {
                subtitle: "पूजा सेवा एवं बुकिंग प्लेटफॉर्म",
                tabPurohit: "पुरोहित प्रोफाइल",
                tabFeatures: "सेवा एवं पंचांग",
                createTitle: "नई पुरोहित प्रोफाइल बनाएं",
                lblName: "पुरोहित का नाम",
                lblDegree: "योग्यता / डिग्री",
                lblExp: "अनुभव (वर्ष)",
                lblFees: "न्यूनतम दक्षिणा (₹)",
                lblLoc: "स्थान / जिला",
                btnSubmitProfile: "प्रोफ़ाइल लाइव करें",
                panjikaHeader: "आज का संक्षिप्त पंचांग",
                panjikaDateLbl: "दिनांक और वार:",
                panjikaDate: "१२ जून, २०२६ | शुक्रवार",
                panjikaTithiLbl: "तिथि:",
                panjikaTithi: "कृष्ण द्वादशी तिथि",
                panjikaNakshatraLbl: "नक्षत्र:",
                panjikaNakshatra: "भरणी नक्षत्र",
                panjikaMuhurtaLbl: "शुभ मुहूर्त:",
                panjikaMuhurta: "सुबह 05:24 - सुबह 07:11",
                donationHeader: "डिजिटल दान एवं कल्याण कोष",
                lblDonCat: "दान श्रेणी का चयन करें:",
                donCat1: "१. नव उपनीत ब्राह्मणों की शिक्षा व्यवस्था में सुधार हेतु दान",
                donCat2: "२. सामूहिक विवाह आयोजन के लिए दान",
                donCat3: "३. सामूहिक उपनयन (जनेऊ) आयोजन सहायता हेतु दान",
                donCat4: "४. मंदिर कार्यान्वयन (निर्माण और जीर्णोद्धार) हेतु दान",
                donCat5: "५. मनोकामना पूर्ति संकल्प हेतु विशेष दान",
                lblDonName: "दाता का नाम",
                lblDonGotra: "गोत्र",
                lblDonAmount: "दान राशि (₹)",
                btnDonate: "डिजिटल संकल्प और दान करें",
                footerPlaceholder: "श्रेणी या सेवा खोजें...",
                verified: "✓ सत्यापित",
                experience: "वर्षों का अनुभव",
                totalPuja: "कुल पूजा",
                rating: "औसत रेटिंग",
                reviews: "समीक्षाएं",
                available: "अभी उपलब्ध",
                from: "से शुरू",
                btnBook: "बुकिंग करें"
            },
            sa: {
                subtitle: "पूजा सेवा च आरक्षण मञ्चः",
                tabPurohit: "पुरोहित विवरणिका",
                tabFeatures: "सेवा च पञ्चाङ्गम्",
                createTitle: "नूतन पुरोहित विवरणिकां रचयन्तु",
                lblName: "पुरोहितस्य नाम",
                lblDegree: "योग्यता / उपाधिः",
                lblExp: "अनुभवः (वर्षाणि)",
                lblFees: "न्यूनतम दक्षिणा (₹)",
                lblLoc: "स्थानम् / मण्डलः",
                btnSubmitProfile: "विवरणिकां प्रकाशयन्तु",
                panjikaHeader: "अद्यतन संक्षिप्त पञ्चाङ्गम्",
                panjikaDateLbl: "तिथिवासरौ:",
                panjikaDate: "१२ जून, २०२६ | भृगुवासरः",
                panjikaTithiLbl: "तिथिः:",
                panjikaTithi: "कृष्णपक्ष द्वादशी तिथिः",
                panjikaNakshatraLbl: "नक्षत्रम्:",
                panjikaNakshatra: "भरणी नक्षत्रम्",
                panjikaMuhurtaLbl: "शुभमुहूर्तः:",
                panjikaMuhurta: "प्रातः ०५:२४ - प्रातः ०७:११",
                donationHeader: "डिजिटल दानम् एवं कल्याण कोषः",
                lblDonCat: "दानश्रेणीं चिनोतु:",
                donCat1: "१. नव उपनीत ब्राह्मणानां शिक्षण व्यवस्था सुधारार्थं दानम्",
                donCat2: "२. सामूहिक विवाह आयोजनार्थं संयुक्त दानम्",
                donCat3: "३. सामूहिक उपनयन संस्कार सहायतार्थं दानम्",
                donCat4: "४. मन्दिर निर्माणाय एवं जीर्णोद्धाराय दानम्",
                donCat5: "५. मनोकामना पूर्तये विशेष संकल्प दानम्",
                lblDonName: "दातुः नाम",
                lblDonGotra: "गोत्रम्",
                lblDonAmount: "दान राशिः (₹)",
                btnDonate: "डिजिटल संकल्पं कृत्वा दानं ददातु",
                footerPlaceholder: "श्रेणीं वा सेवां अन्विष्यन्तु...",
                verified: "✓ प्रमाणीकृत",
                experience: "वर्षानुभवः",
                totalPuja: "कुल पूजाः",
                rating: "औसत मूल्याङ्कनम्",
                reviews: "समीक्षाः",
                available: "अधुना उपलब्धः",
                from: "आरभ्य",
                btnBook: "आरक्षणं कुरु"
            }
        };

        // Default Sample Data matching Screenshot_20260612-104559_Claude.jpg
        let defaultProfiles = [
            {
                id: 1,
                name: "पণ্ডিত रामकृष्ण शास्त्री",
                degree: "वेदান্ত বিশারদ",
                experience: "২৮",
                totalPuja: "২,৮৪০",
                rating: "৪.৯★",
                reviews: "৩১২",
                location: "কলকাতা, পশ্চিমবঙ্গ",
                fees: "১,৫০১",
                languages: ["বাংলা", "সংস্কৃত"],
                avatar: "https://api.dicebear.com/7.x/bottts-neutral/svg?seed=priest1"
            }
        ];

        let currentLang = "bn";

        // Initialization
        window.onload = function() {
            if(!localStorage.getItem("puja_profiles")) {
                localStorage.setItem("puja_profiles", JSON.stringify(defaultProfiles));
            }
            renderProfiles();
            changeLanguage("bn");
        };

        function switchTab(tab) {
            const btnPurohit = document.getElementById("tab-purohit");
            const btnFeatures = document.getElementById("tab-features");
            const secPurohit = document.getElementById("section-purohit");
            const secFeatures = document.getElementById("section-features");

            if(tab === 'purohit') {
                btnPurohit.className = "w-1/2 bg-puja-orange text-white py-2.5 px-4 rounded-lg font-bold text-sm transition-all flex items-center justify-center space-x-2";
                btnFeatures.className = "w-1/2 text-orange-200 hover:text-white py-2.5 px-4 rounded-lg font-bold text-sm transition-all flex items-center justify-center space-x-2";
                secPurohit.classList.remove("hidden");
                secFeatures.classList.add("hidden");
            } else {
                btnFeatures.className = "w-1/2 bg-puja-orange text-white py-2.5 px-4 rounded-lg font-bold text-sm transition-all flex items-center justify-center space-x-2";
                btnPurohit.className = "w-1/2 text-orange-200 hover:text-white py-2.5 px-4 rounded-lg font-bold text-sm transition-all flex items-center justify-center space-x-2";
                secPurohit.classList.add("hidden");
                secFeatures.classList.remove("hidden");
            }
        }

        function toggleProfileForm() {
            const form = document.getElementById("profile-form");
            const chevron = document.getElementById("form-chevron");
            if(form.classList.contains("hidden")) {
                form.classList.remove("hidden");
                chevron.className = "fa-solid fa-chevron-up text-xs";
            } else {
                form.classList.add("hidden");
                chevron.className = "fa-solid fa-chevron-down text-xs";
            }
        }

        function saveProfile(e) {
            e.preventDefault();
            const profiles = JSON.parse(localStorage.getItem("puja_profiles")) || [];
            
            const newProfile = {
                id: Date.now(),
                name: document.getElementById("p-name").value,
                degree: document.getElementById("p-degree").value,
                experience: document.getElementById("p-exp").value,
                totalPuja: "0",
                rating: "5.0★",
                reviews: "0",
                location: document.getElementById("p-loc").value,
                fees: Number(document.getElementById("p-fees").value).toLocaleString('en-IN'),
                languages: ["বাংলা", "English"],
                avatar: "https://api.dicebear.com/7.x/bottts-neutral/svg?seed=" + Math.random()
            };

            profiles.push(newProfile);
            localStorage.setItem("puja_profiles", JSON.stringify(profiles));
            renderProfiles();
            document.getElementById("profile-form").reset();
            toggleProfileForm();
            alert("সফলভাবে প্রোফাইল তৈরি ও সংরক্ষণ হয়েছে!");
        }

        function renderProfiles() {
            const container = document.getElementById("profiles-container");
            const profiles = JSON.parse(localStorage.getItem("puja_profiles")) || [];
            container.innerHTML = "";

            profiles.forEach(p => {
                container.innerHTML += `
                    <!-- CARD ARCHITECTURE ROOT FROM SCREENSHOT -->
                    <div class="bg-white rounded-2xl border border-orange-100 shadow-sm overflow-hidden">
                        <!-- Orange Info Header Gradient Banner -->
                        <div class="bg-gradient-to-r from-orange-500 to-amber-600 p-4 relative flex items-center space-x-4">
                            <div class="w-16 h-16 rounded-full border-2 border-white bg-orange-100 overflow-hidden flex items-center justify-center">
                                <img src="${p.avatar}" class="w-14 h-14" alt="Priest Profile Picture">
                            </div>
                            <div class="text-white flex-1">
                                <h3 class="text-lg font-bold">${p.name}</h3>
                                <p class="text-xs text-orange-100">${p.degree}</p>
                            </div>
                            <span class="absolute top-4 right-4 bg-white text-orange-700 text-[10px] font-bold px-2 py-0.5 rounded-full shadow-sm">
                                ${localization[currentLang].verified}
                            </span>
                        </div>

                        <!-- Quad Counters Section -->
                        <div class="grid grid-cols-4 gap-1 p-3 text-center bg-orange-50/40 border-b border-orange-50">
                            <div class="p-1">
                                <span class="block text-sm font-bold text-puja-dark">${p.experience}</span>
                                <span class="text-[10px] text-gray-500">${localization[currentLang].experience}</span>
                            </div>
                            <div class="p-1">
                                <span class="block text-sm font-bold text-puja-dark">${p.totalPuja}</span>
                                <span class="text-[10px] text-gray-500">${localization[currentLang].totalPuja}</span>
                            </div>
                            <div class="p-1">
                                <span class="block text-sm font-bold text-[#E65100]">${p.rating}</span>
                                <span class="text-[10px] text-gray-500">${localization[currentLang].rating}</span>
                            </div>
                            <div class="p-1">
                                <span class="block text-sm font-bold text-puja-dark">${p.reviews}</span>
                                <span class="text-[10px] text-gray-500">${localization[currentLang].reviews}</span>
                            </div>
                        </div>

                        <!-- Metatags and Pricing Footer Row -->
                        <div class="p-3 space-y-3">
                            <div class="flex flex-wrap gap-1.5 text-[11px] font-semibold">
                                <span class="bg-green-100 text-green-800 px-2.5 py-1 rounded-full flex items-center">
                                    <span class="w-2 h-2 rounded-full bg-green-500 mr-1.5 inline-block"></span>${localization[currentLang].available}
                                </span>
                                <span class="bg-orange-50 text-puja-dark px-2.5 py-1 rounded-full">
                                    📍 ${p.location}
                                </span>
                            </div>

                            <div class="flex justify-between items-center pt-2 border-t border-gray-100">
                                <div class="text-sm">
                                    <span class="text-xs text-gray-500 font-medium">💰 ₹${p.fees}</span>
                                    <span class="text-[10px] text-gray-400 font-medium"> ${localization[currentLang].from}</span>
                                </div>
                                <button onclick="openBookingModal(${p.id})" class="bg-puja-orange hover:bg-orange-600 text-white font-bold text-xs px-4 py-2 rounded-xl transition-all">
                                    ${localization[currentLang].btnBook}
                                </button>
                            </div>
                        </div>
                    </div>
                `;
            });
        }

        function changeLanguage(lang) {
            currentLang = lang;
            const t = localization[lang];

            // UI Transmutation Elements
            document.getElementById("app-subtitle").innerText = t.subtitle;
            document.getElementById("text-tab-purohit").innerText = t.tabPurohit;
            document.getElementById("text-tab-features").innerText = t.tabFeatures;
            document.getElementById("text-create-title").innerHTML = `<i class="fa-solid fa-user-plus mr-1 text-puja-orange"></i> ${t.createTitle}`;
            
            // Input Fields Translation Labels
            document.getElementById("lbl-name").innerText = t.lblName;
            document.getElementById("lbl-degree").innerText = t.lblDegree;
            document.getElementById("lbl-exp").innerText = t.lblExp;
            document.getElementById("lbl-fees").innerText = t.lblFees;
            document.getElementById("lbl-loc").innerText = t.lblLoc;
            document.getElementById("btn-submit-profile").innerText = t.btnSubmitProfile;

            // Panjika Data Transmutation 
            document.getElementById("panjika-header").innerText = t.panjikaHeader;
            document.getElementById("panjika-date-lbl").innerText = t.panjikaDateLbl;
            document.getElementById("panjika-date").innerText = t.panjikaDate;
            document.getElementById("panjika-tithi-lbl").innerText = t.panjikaTithiLbl;
            document.getElementById("panjika-tithi").innerText = t.panjikaTithi;
            document.getElementById("panjika-nakshatra-lbl").innerText = t.panjikaNakshatraLbl;
            document.getElementById("panjika-nakshatra").innerText = t.panjikaNakshatra;
            document.getElementById("panjika-muhurta-lbl").innerText = t.panjikaMuhurtaLbl;
            document.getElementById("panjika-muhurta").innerText = t.panjikaMuhurta;

            // Donation Transmutation
            document.getElementById("donation-header").innerText = t.donationHeader;
            document.getElementById("lbl-don-cat").innerText = t.lblDonCat;
            document.getElementById("don-cat-1").innerText = t.donCat1;
            document.getElementById("don-cat-2").innerText = t.donCat2;
            document.getElementById("don-cat-3").innerText = t.donCat3;
            document.getElementById("don-cat-4").innerText = t.donCat4;
            document.getElementById("don-cat-5").innerText = t.donCat5;

            document.getElementById("lbl-don-name").innerText = t.lblDonName;
            document.getElementById("lbl-don-gotra").innerText = t.lblDonGotra;
            document.getElementById("lbl-don-amount").innerText = t.lblDonAmount;
            document.getElementById("txt-btn-donate").innerText = t.btnDonate;

            document.getElementById("footer-search").placeholder = t.footerPlaceholder;

            renderProfiles();
        }

        // Donation Execution Interceptor
        function handleDonation(e) {
            e.preventDefault();
            const donorName = document.getElementById("don-name").value;
            const donorGotra = document.getElementById("don-gotra").value;
            const amount = document.getElementById("don-amount").value;
            const categoryElement = document.querySelector('input[name="don_category"]:checked');
            
            let categoryId = categoryElement.value;
            let categoryText = document.getElementById("don-" + categoryId.replace("_", "-")).innerText;

            alert(`✨ সংকল্প ও দান সফল হয়েছে! ✨\n\nदाता: ${donorName}\nगोत्र: ${donorGotra}\nখাত: ${categoryText}\nপরিমাণ: ₹${amount}\n\nআপনার দান ও কল্যাণমূলক সংকল্পটি ডিজিটাল ডাটাবেজে নথিবদ্ধ করা হয়েছে।`);
            
            // Reset fields
            document.getElementById("don-name").value = "";
            document.getElementById("don-gotra").value = "";
            document.getElementById("don-amount").value = "";
        }

        function openBookingModal(purohitId) {
            document.getElementById("modal-purohit-id").value = purohitId;
            document.getElementById("booking-modal").classList.remove("hidden");
        }

        function closeBookingModal() {
            document.getElementById("booking-modal").classList.add("hidden");
        }

        function confirmBooking(e) {
            e.preventDefault();
            const userName = document.getElementById("b-user").value;
            const pujaType = document.getElementById("b-puja").value;
            const date = document.getElementById("b-date").value;
            
            alert(`✅ বুকিং অনুরোধ পাঠানো হয়েছে!\n\nনাম: ${userName}\nসেবা: ${pujaType}\nতারিখ: ${date}\n\nনির্দিষ্ট পুরোহিত শীঘ্রই আপনার সাথে যোগাযোগ করবেন।`);
            closeBookingModal();
        }
    </script>
</body>
</html># brambin-seva
