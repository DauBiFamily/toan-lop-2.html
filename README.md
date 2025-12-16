# toan-lop-2.html
Ô thi học kỳ 1
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ôn Tập Toán Lớp 2 - Học Kỳ 1</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700&display=swap');
        
        body {
            font-family: 'Nunito', sans-serif, Arial, sans-serif;
            background-color: #FDFBF7;
            color: #4A4A4A;
        }

        .chart-container {
            position: relative;
            width: 100%;
            max-width: 500px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 400px;
        }

        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1; 
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e0; 
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #a0aec0; 
        }

        .card-hover:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }
        
        .tab-active {
            background-color: #ED8936;
            color: white;
            font-weight: 700;
        }
        
        .tab-inactive {
            background-color: #FFF;
            color: #718096;
            font-weight: 600;
        }
        .tab-inactive:hover {
            background-color: #FEF3C7;
            color: #D97706;
        }

        .correct-answer {
            background-color: #C6F6D5;
            border: 2px solid #48BB78;
        }
        .incorrect-answer {
            background-color: #FED7D7;
            border: 2px solid #F56565;
        }
    </style>
    <!-- Chosen Palette: Warm Paper (Neutral Beige #FDFBF7 background, Text #4A4A4A, Accents #ED8936 Orange & #48BB78 Green) -->
    <!-- Application Structure Plan: Cấu trúc SPA được thiết kế theo luồng tương tác: Tổng Quan (Dashboard) -> Kiến Thức (Concepts) -> Luyện Tập (Practice). Mục tiêu là cung cấp một lộ trình học tập logic, tập trung vào việc khắc phục các điểm yếu đã được báo cáo. Sử dụng Flexbox/Grid và hệ thống tab để đảm bảo điều hướng dễ dàng và trải nghiệm mượt mà trên mọi thiết bị. -->
    <!-- Visualization & Content Choices: Sử dụng Chart.js (Doughnut Chart) cho phần Tổng Quan để tóm tắt nhanh tình trạng kỹ năng. Các phần Kiến Thức và Từ Vựng dùng thẻ (cards) và chức năng toggle (bật/tắt) để trình bày các lỗi sai và giải thích cụ thể, đảm bảo tính tương tác cao. Phần Luyện Tập là một công cụ Quiz với phản hồi ngay lập tức. KHÔNG sử dụng SVG, KHÔNG sử dụng Mermaid JS. -->
</head>
<body class="min-h-screen flex flex-col items-center py-6 px-4">

    <!-- Main App Container -->
    <div id="app" class="w-full max-w-4xl bg-white shadow-xl rounded-2xl overflow-hidden min-h-[800px] flex flex-col">
        
        <!-- Header -->
        <header class="bg-[#FFEDD5] p-6 text-center border-b border-orange-100">
            <h1 class="text-3xl md:text-4xl font-bold text-orange-800 mb-2">🐻 Ôn Tập Toán Lớp 2</h1>
            <p class="text-orange-700 font-medium">Học Kỳ 1: Phép cộng trừ, Hình học & Đại lượng</p>
        </header>

        <!-- Navigation Tabs -->
        <nav class="flex flex-wrap justify-center bg-orange-50 border-b border-orange-100 p-2 gap-2">
            <button onclick="switchTab('dashboard')" id="tab-dashboard" class="px-6 py-2 rounded-lg transition-all duration-300 tab-active">Tổng Quan</button>
            <button onclick="switchTab('concepts')" id="tab-concepts" class="px-6 py-2 rounded-lg transition-all duration-300 tab-inactive">Kiến Thức</button>
            <button onclick="switchTab('vocab')" id="tab-vocab" class="px-6 py-2 rounded-lg transition-all duration-300 tab-inactive">Từ Vựng</button>
            <button onclick="switchTab('practice')" id="tab-practice" class="px-6 py-2 rounded-lg transition-all duration-300 tab-inactive">Luyện Tập</button>
        </nav>

        <!-- Content Area -->
        <main id="content-area" class="flex-grow p-6 overflow-y-auto bg-[#FDFBF7]">
            <!-- Content is injected via JS -->
        </main>

        <!-- Footer -->
        <footer class="bg-gray-50 p-4 text-center text-gray-500 text-sm border-t">
            <p>Dựa trên kết quả ôn tập cá nhân • Chúc bạn học tốt!</p>
        </footer>
    </div>

    <script>
        const reportData = {
            summary: {
                strengths: ["Thành phần phép tính (Số hạng, Tổng)", "Đổi đơn vị (dm, cm)", "Xem đồng hồ giờ đúng"],
                weaknesses: ["Tính chính xác khi cộng trừ (có nhớ)", "Tư duy cấu tạo số (số lớn nhất/nhỏ nhất)", "Giải toán có lời văn"],
                intro: "Chào mừng bạn trở lại! Dựa trên bài kiểm tra vừa qua, chúng mình đã tổng hợp lại lộ trình ôn tập này. Bạn đã làm rất tốt các phần cơ bản, nhưng chúng ta cần rèn luyện thêm một chút về tính toán cẩn thận và các bài toán đố nhé."
            },
            concepts: [
                {
                    id: "calc",
                    title: "🔢 Phép Cộng & Trừ (Có Nhớ)",
                    intro: "Phần này tập trung sửa các lỗi tính toán thường gặp. Nguyên tắc quan trọng nhất: Luôn tính từ phải sang trái (Hàng đơn vị trước, Hàng chục sau).",
                    points: [
                        {
                            label: "Lỗi sai thường gặp (34 + 25)",
                            wrong: "69 (Sai ở hàng chục)",
                            right: "59 (Đúng)",
                            explanation: "4 + 5 = 9 (viết 9). 3 + 2 = 5 (viết 5). Kết quả là 59. Hãy cẩn thận khi cộng các số hàng chục!"
                        },
                        {
                            label: "Phép trừ có nhớ (62 - 28)",
                            wrong: "Quên mượn",
                            right: "34",
                            explanation: "2 không trừ được 8, mượn 1 chục thành 12 - 8 = 4 (nhớ 1). 2 thêm 1 là 3. 6 - 3 = 3."
                        }
                    ]
                },
                {
                    id: "structure",
                    title: "🏗️ Cấu Tạo Số",
                    intro: "Hiểu rõ về vị trí các chữ số giúp bạn tìm ra số lớn nhất hoặc nhỏ nhất một cách chính xác.",
                    points: [
                        {
                            label: "Số lớn nhất có 2 chữ số khác nhau",
                            wrong: "89 (Chọn hàng đơn vị lớn trước)",
                            right: "98",
                            explanation: "Bước 1: Chọn hàng chục lớn nhất -> 9. Bước 2: Chọn hàng đơn vị lớn nhất khác 9 -> 8. Kết quả: 98."
                        },
                        {
                            label: "Số liền trước/sau",
                            wrong: "Nhầm lẫn khái niệm",
                            right: "Trước (-1), Sau (+1)",
                            explanation: "Số liền trước của 80 là 79 (80 - 1). Số liền sau của 80 là 81 (80 + 1)."
                        }
                    ]
                },
                {
                    id: "wordproblems",
                    title: "📝 Toán Có Lời Văn",
                    intro: "Đọc kỹ đề bài để chọn phép tính đúng. Các từ khóa quan trọng sẽ giúp bạn quyết định nên Cộng hay Trừ.",
                    points: [
                        {
                            label: "Nhiều hơn / Tất cả / Cả hai",
                            type: "Cộng (+)",
                            example: "A nhiều hơn B 5 viên. Tìm A -> Lấy B + 5."
                        },
                        {
                            label: "Ít hơn / Nhẹ hơn / Còn lại",
                            type: "Trừ (-)",
                            example: "Bao bé nhẹ hơn bao to 5kg. Tìm bao bé -> Lấy Bao to - 5kg."
                        }
                    ]
                },
                {
                    id: "geometry",
                    title: "📐 Hình Học & Thời Gian",
                    intro: "Các quy tắc cần nhớ về hình phẳng và cách tính ngày tháng.",
                    points: [
                        {
                            label: "Điểm thẳng hàng",
                            content: "3 điểm cùng nằm trên một đường thẳng (dùng thước kẻ kiểm tra)."
                        },
                        {
                            label: "Lịch (Tuần)",
                            content: "1 tuần = 7 ngày. Thứ này tuần sau = Ngày hôm nay + 7. (Ví dụ: Ngày 15 + 7 = 22)."
                        }
                    ]
                }
            ],
            vocab: [
                { term: "Số hạng", def: "Thành phần trong phép cộng (VD: 3 + 2 = 5, thì 3 và 2 là số hạng)." },
                { term: "Tổng", def: "Kết quả của phép cộng." },
                { term: "Số bị trừ", def: "Số đứng trước dấu trừ." },
                { term: "Số trừ", def: "Số đứng sau dấu trừ." },
                { term: "Hiệu", def: "Kết quả của phép trừ." },
                { term: "Chu vi", def: "Tổng độ dài các đường bao quanh một hình." },
                { term: "dm (Đề-xi-mét)", def: "Đơn vị đo độ dài. 1 dm = 10 cm." },
                { term: "Điểm thẳng hàng", def: "Ba điểm cùng nằm trên một đường thẳng." }
            ],
            quiz: [
                {
                    q: "Đặt tính rồi tính: 47 + 35 = ?",
                    options: ["72", "82", "81", "712"],
                    correct: 1,
                    explain: "7 + 5 = 12 (viết 2 nhớ 1). 4 + 3 = 7, thêm 1 bằng 8. Kết quả là 82."
                },
                {
                    q: "Đặt tính rồi tính: 81 - 26 = ?",
                    options: ["65", "55", "54", "64"],
                    correct: 1,
                    explain: "1 không trừ được 6, lấy 11 - 6 = 5 (nhớ 1). 2 thêm 1 bằng 3. 8 - 3 = 5. Kết quả là 55."
                },
                {
                    q: "Số bé nhất có hai chữ số khác nhau là số nào?",
                    options: ["10", "11", "12", "01"],
                    correct: 0,
                    explain: "Hàng chục bé nhất khác 0 là 1. Hàng đơn vị bé nhất khác 1 là 0. Vậy số đó là 10."
                },
                {
                    q: "Lan có 14 hạc giấy. Mai gấp ít hơn Lan 5 con. Hỏi Mai gấp được bao nhiêu?",
                    options: ["19 con", "9 con", "10 con", "11 con"],
                    correct: 1,
                    explain: "Bài toán 'ít hơn' dùng phép trừ: 14 - 5 = 9 con."
                },
                {
                    q: "Hôm nay là thứ Tư ngày 10. Thứ Tư tuần sau là ngày bao nhiêu?",
                    options: ["Ngày 16", "Ngày 18", "Ngày 17", "Ngày 20"],
                    correct: 2,
                    explain: "Một tuần có 7 ngày. Thứ Tư tuần sau là ngày: 10 + 7 = 17."
                }
            ]
        };

        let currentTab = 'dashboard';
        const contentArea = document.getElementById('content-area');

        function switchTab(tabId) {
            document.querySelectorAll('nav button').forEach(btn => {
                if(btn.id === `tab-${tabId}`) {
                    btn.classList.remove('tab-inactive');
                    btn.classList.add('tab-active');
                } else {
                    btn.classList.remove('tab-active');
                    btn.classList.add('tab-inactive');
                }
            });

            currentTab = tabId;
            renderContent(tabId);
        }

        function renderContent(tabId) {
            contentArea.innerHTML = '';
            
            switch(tabId) {
                case 'dashboard':
                    renderDashboard();
                    break;
                case 'concepts':
                    renderConcepts();
                    break;
                case 'vocab':
                    renderVocab();
                    break;
                case 'practice':
                    renderPractice();
                    break;
            }
        }

        function renderDashboard() {
            const introDiv = document.createElement('div');
            introDiv.className = "mb-8 bg-blue-50 p-6 rounded-xl border border-blue-100";
            introDiv.innerHTML = `
                <h2 class="text-2xl font-bold text-blue-800 mb-2">👋 Tổng Quan Kết Quả</h2>
                <p class="text-blue-700 leading-relaxed">${reportData.summary.intro}</p>
            `;
            contentArea.appendChild(introDiv);

            const gridDiv = document.createElement('div');
            gridDiv.className = "grid grid-cols-1 md:grid-cols-2 gap-8";

            const chartSection = document.createElement('div');
            chartSection.className = "bg-white p-6 rounded-xl shadow-sm border border-gray-100 flex flex-col items-center";
            chartSection.innerHTML = `
                <h3 class="font-bold text-gray-700 mb-4 text-lg">Biểu Đồ Kỹ Năng</h3>
                <div class="chart-container">
                    <canvas id="skillsChart"></canvas>
                </div>
                <p class="text-sm text-gray-400 mt-4 text-center italic">Tỉ lệ dựa trên số lượng khái niệm cần ôn tập thêm</p>
            `;
            gridDiv.appendChild(chartSection);

            const listsSection = document.createElement('div');
            listsSection.className = "flex flex-col gap-6";

            const strengthHTML = reportData.summary.strengths.map(s => `<li class="flex items-start"><span class="mr-2 text-green-500">✔</span> ${s}</li>`).join('');
            const strengthBox = document.createElement('div');
            strengthBox.className = "bg-green-50 p-5 rounded-xl border border-green-100";
            strengthBox.innerHTML = `
                <h3 class="font-bold text-green-800 mb-3 flex items-center"><span class="text-xl mr-2">🌟</span> Đã Làm Tốt</h3>
                <ul class="text-green-700 space-y-2 text-sm md:text-base">${strengthHTML}</ul>
            `;

            const weakHTML = reportData.summary.weaknesses.map(w => `<li class="flex items-start"><span class="mr-2 text-red-500">⚠️</span> ${w}</li>`).join('');
            const weakBox = document.createElement('div');
            weakBox.className = "bg-red-50 p-5 rounded-xl border border-red-100";
            weakBox.innerHTML = `
                <h3 class="font-bold text-red-800 mb-3 flex items-center"><span class="text-xl mr-2">🎯</span> Cần Cải Thiện</h3>
                <ul class="text-red-700 space-y-2 text-sm md:text-base">${weakHTML}</ul>
            `;

            listsSection.appendChild(strengthBox);
            listsSection.appendChild(weakBox);
            gridDiv.appendChild(listsSection);

            contentArea.appendChild(gridDiv);

            setTimeout(initChart, 0);
        }

        function initChart() {
            const ctx = document.getElementById('skillsChart').getContext('2d');
            new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ['Đã Nắm Vững', 'Cần Ôn Tập'],
                    datasets: [{
                        data: [60, 40],
                        backgroundColor: ['#48BB78', '#ED8936'],
                        borderWidth: 0,
                        hoverOffset: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                font: {
                                    family: "'Nunito', sans-serif",
                                    size: 14
                                },
                                usePointStyle: true
                            }
                        }
                    }
                }
            });
        }

        function renderConcepts() {
            const introHeader = document.createElement('div');
            introHeader.className = "mb-6";
            introHeader.innerHTML = `
                <h2 class="text-2xl font-bold text-gray-800 mb-2">📚 Bài Học & Phân Tích Lỗi Sai</h2>
                <p class="text-gray-600">Dưới đây là các chủ đề chính bạn cần xem lại. Bấm vào từng mục để xem chi tiết nhé!</p>
            `;
            contentArea.appendChild(introHeader);

            const container = document.createElement('div');
            container.className = "space-y-4";

            reportData.concepts.forEach(concept => {
                const card = document.createElement('div');
                card.className = "bg-white rounded-xl shadow-sm border border-gray-200 overflow-hidden";
                
                const header = document.createElement('div');
                header.className = "p-4 bg-orange-50 cursor-pointer flex justify-between items-center hover:bg-orange-100 transition-colors";
                header.onclick = () => toggleConcept(card);
                header.innerHTML = `
                    <h3 class="font-bold text-orange-900 text-lg">${concept.title}</h3>
                    <span class="text-orange-500 text-xl transform transition-transform duration-200">▼</span>
                `;

                const body = document.createElement('div');
                body.className = "p-5 hidden bg-white";
                
                let bodyContent = `<p class="mb-4 text-gray-600 italic border-l-4 border-orange-300 pl-3">${concept.intro}</p>`;
                
                bodyContent += `<div class="grid grid-cols-1 md:grid-cols-2 gap-4">`;
                concept.points.forEach(point => {
                    bodyContent += `
                        <div class="bg-gray-50 p-4 rounded-lg border border-gray-100">
                            <h4 class="font-bold text-gray-700 mb-2 border-b pb-1">${point.label}</h4>
                            ${point.wrong ? `<p class="text-red-500 text-sm mb-1">❌ Sai: <span class="line-through">${point.wrong}</span></p>` : ''}
                            ${point.right ? `<p class="text-green-600 font-bold text-sm mb-2">✅ Đúng: ${point.right}</p>` : ''}
                            ${point.content ? `<p class="text-gray-700 text-sm mb-2">${point.content}</p>` : ''}
                            ${point.explanation ? `<p class="text-gray-500 text-xs bg-white p-2 rounded mt-2">💡 ${point.explanation}</p>` : ''}
                            ${point.type ? `<div class="mt-2 text-center py-1 rounded bg-blue-100 text-blue-800 font-bold">${point.type}</div>` : ''}
                            ${point.example ? `<p class="text-xs text-gray-500 mt-1 italic">VD: ${point.example}</p>` : ''}
                        </div>
                    `;
                });
                bodyContent += `</div>`;

                body.innerHTML = bodyContent;
                
                card.appendChild(header);
                card.appendChild(body);
                container.appendChild(card);
            });

            contentArea.appendChild(container);
        }

        function toggleConcept(cardElement) {
            const body = cardElement.querySelector('div:last-child');
            const icon = cardElement.querySelector('span');
            
            if (body.classList.contains('hidden')) {
                body.classList.remove('hidden');
                icon.style.transform = "rotate(180deg)";
            } else {
                body.classList.add('hidden');
                icon.style.transform = "rotate(0deg)";
            }
        }

        function renderVocab() {
            const intro = document.createElement('div');
            intro.innerHTML = `<h2 class="text-2xl font-bold text-gray-800 mb-6">📖 Từ Vựng Toán Học</h2>`;
            contentArea.appendChild(intro);

            const grid = document.createElement('div');
            grid.className = "grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4";

            reportData.vocab.forEach(item => {
                const card = document.createElement('div');
                card.className = "bg-white p-5 rounded-xl border border-gray-200 shadow-sm card-hover flex flex-col justify-center items-center text-center h-40";
                card.innerHTML = `
                    <h3 class="text-lg font-bold text-indigo-600 mb-2">${item.term}</h3>
                    <p class="text-sm text-gray-600">${item.def}</p>
                `;
                grid.appendChild(card);
            });

            contentArea.appendChild(grid);
        }

        function renderPractice() {
            const intro = document.createElement('div');
            intro.className = "mb-6";
            intro.innerHTML = `
                <h2 class="text-2xl font-bold text-gray-800 mb-2">✍️ Luyện Tập</h2>
                <p class="text-gray-600">Hãy thử sức với 5 câu hỏi dưới đây để xem bạn đã nắm vững bài chưa nhé!</p>
            `;
            contentArea.appendChild(intro);

            const quizContainer = document.createElement('div');
            quizContainer.className = "space-y-8";

            reportData.quiz.forEach((q, index) => {
                const qBox = document.createElement('div');
                qBox.className = "bg-white p-6 rounded-xl border border-gray-200 shadow-sm";
                qBox.id = `q-box-${index}`;

                let optionsHTML = `<div class="grid grid-cols-1 sm:grid-cols-2 gap-3 mt-4">`;
                q.options.forEach((opt, optIndex) => {
                    optionsHTML += `
                        <button onclick="checkAnswer(${index}, ${optIndex})" 
                                class="opt-btn-${index} w-full text-left p-3 rounded-lg border border-gray-200 hover:bg-gray-50 transition-colors focus:outline-none">
                            <span class="font-bold mr-2 text-gray-400">${String.fromCharCode(65+optIndex)}.</span> ${opt}
                        </button>
                    `;
                });
                optionsHTML += `</div>`;

                qBox.innerHTML = `
                    <h3 class="font-bold text-lg text-gray-800"><span class="bg-orange-100 text-orange-600 px-2 py-1 rounded text-sm mr-2">Câu ${index + 1}</span> ${q.q}</h3>
                    ${optionsHTML}
                    <div id="feedback-${index}" class="hidden mt-4 p-4 rounded-lg bg-gray-50 text-sm"></div>
                `;
                
                quizContainer.appendChild(qBox);
            });

            contentArea.appendChild(quizContainer);
        }

        function checkAnswer(qIndex, selectedOptIndex) {
            const questionData = reportData.quiz[qIndex];
            const feedbackBox = document.getElementById(`feedback-${qIndex}`);
            const buttons = document.querySelectorAll(`.opt-btn-${qIndex}`);

            buttons.forEach(btn => btn.disabled = true);

            const isCorrect = selectedOptIndex === questionData.correct;

            buttons[selectedOptIndex].classList.remove('hover:bg-gray-50');
            if (isCorrect) {
                buttons[selectedOptIndex].classList.add('correct-answer', 'text-green-800');
            } else {
                buttons[selectedOptIndex].classList.add('incorrect-answer', 'text-red-800');
                buttons[questionData.correct].classList.add('correct-answer', 'text-green-800');
            }

            feedbackBox.classList.remove('hidden', 'bg-gray-50', 'bg-green-50', 'bg-red-50');
            feedbackBox.classList.add(isCorrect ? 'bg-green-50' : 'bg-red-50');
            feedbackBox.innerHTML = `
                <p class="font-bold ${isCorrect ? 'text-green-700' : 'text-red-700'} mb-1">
                    ${isCorrect ? '🎉 Chính xác!' : '😅 Chưa đúng rồi.'}
                </p>
                <p class="text-gray-700">${questionData.explain}</p>
            `;
        }

        renderDashboard();

    </script>
</body>
</html>
