<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nền Tảng Ôn Thi Toán 10 THPT</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.8/dist/katex.min.css">
    <script src="https://cdn.jsdelivr.net/npm/katex@0.16.8/dist/katex.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/katex@0.16.8/dist/contrib/auto-render.min.js"></script>
    
    <!-- Chosen Palette: Indigo & Slate -->
    <!-- Application Structure Plan: Cấu trúc ứng dụng được chia thành dạng Dashboard học tập. Cột bên trái hiển thị phân tích cấu trúc đề thi bằng biểu đồ Donut và tóm tắt thông tin giúp người dùng nắm bắt trọng tâm bài thi. Cột bên phải là khu vực luyện tập tương tác (Không gian luyện tập), chia làm 3 tab tương ứng với 3 phần của đề thi thật (Trắc nghiệm 12 câu, Đúng/Sai 4 câu, Trả lời ngắn 6 câu). Cấu trúc này tối ưu hóa cho việc học chủ động: người dùng được định hướng chiến lược học tập qua biểu đồ trước, sau đó tự thực hành và tra cứu lời giải thay vì chỉ đọc văn bản thụ động. -->
    <!-- Visualization & Content Choices: Cấu trúc đề thi -> Goal: Inform -> Viz/Presentation Method: Donut Chart (Chart.js) -> Interaction: Hover to see exact numbers -> Justification: Giúp học sinh hình dung trực quan tỷ trọng các phần thi. Phần bài tập -> Goal: Practice/Compare -> Viz/Presentation Method: Interactive Cards -> Interaction: Click chọn đáp án, Tab navigation, Toggle lời giải -> Justification: Tăng tính tương tác, khuyến khích tự suy nghĩ trước khi xem đáp án. Không sử dụng SVG/Mermaid. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <style>
        body { background-color: #f8fafc; color: #1e293b; font-family: system-ui, -apple-system, sans-serif; }
        .chart-container { position: relative; width: 100%; max-width: 400px; margin-left: auto; margin-right: auto; height: 300px; max-height: 350px; }
        .math-block { overflow-x: auto; padding-bottom: 0.5rem; }
        .tab-btn.active { border-bottom: 2px solid #4f46e5; color: #4f46e5; font-weight: 600; }
        .solution-block { display: none; }
        .solution-block.show { display: block; animation: slideDown 0.3s ease-out forwards; }
        @keyframes slideDown { from { opacity: 0; transform: translateY(-10px); } to { opacity: 1; transform: translateY(0); } }
        input[type="radio"]:checked + label { background-color: #e0e7ff; border-color: #6366f1; color: #3730a3; }
        .tf-btn.active-true { background-color: #10b981; color: white; border-color: #10b981; }
        .tf-btn.active-false { background-color: #ef4444; color: white; border-color: #ef4444; }
    </style>
</head>
<body class="min-h-screen">

    <header class="bg-indigo-700 text-white shadow-md sticky top-0 z-40">
        <div class="max-w-7xl mx-auto px-4 py-4 flex flex-col md:flex-row justify-between items-center gap-4">
            <h1 class="text-2xl font-bold flex items-center gap-2">
                <span class="text-3xl">🎓</span> Ôn Thi Tuyển Sinh Vào Lớp 10 THPT - Môn Toán
            </h1>
            <div class="flex items-center gap-3">
                <span class="bg-indigo-800 text-indigo-100 text-sm font-semibold px-4 py-2 rounded-full flex items-center gap-2">
                    <span>⏱️</span> Thời gian: 90 phút
                </span>
            </div>
        </div>
    </header>

    <main class="max-w-7xl mx-auto px-4 py-8 grid grid-cols-1 lg:grid-cols-12 gap-8">
        
        <aside class="lg:col-span-4 flex flex-col gap-6">
            <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-6">
                <h2 class="text-xl font-bold text-slate-800 mb-2 border-b pb-3 flex items-center gap-2">
                    <span>📊</span> Phân Tích Cấu Trúc Đề
                </h2>
                <p class="text-sm text-slate-600 mb-6 mt-3">
                    Biểu đồ dưới đây thể hiện số lượng câu hỏi phân bổ theo định dạng thi mới (Tổng cộng 22 câu).
                </p>
                <div class="chart-container">
                    <canvas id="examStructureChart"></canvas>
                </div>
                <div class="mt-6 pt-4 border-t border-slate-100">
                    <ul class="space-y-3 text-sm">
                        <li class="flex justify-between items-center">
                            <span class="flex items-center gap-2"><span class="w-3 h-3 rounded-full bg-indigo-500"></span> Phần I (Trắc nghiệm)</span> 
                            <span class="font-bold text-slate-800">12 câu</span>
                        </li>
                        <li class="flex justify-between items-center">
                            <span class="flex items-center gap-2"><span class="w-3 h-3 rounded-full bg-amber-500"></span> Phần II (Đúng/Sai)</span> 
                            <span class="font-bold text-slate-800">4 câu</span>
                        </li>
                        <li class="flex justify-between items-center">
                            <span class="flex items-center gap-2"><span class="w-3 h-3 rounded-full bg-emerald-500"></span> Phần III (Trả lời ngắn)</span> 
                            <span class="font-bold text-slate-800">6 câu</span>
                        </li>
                    </ul>
                </div>
            </div>

            <div class="bg-indigo-50 rounded-2xl shadow-sm border border-indigo-100 p-6">
                <h2 class="text-lg font-bold text-indigo-900 mb-3 flex items-center gap-2">
                    <span>💡</span> Chiến Lược Ôn Tập
                </h2>
                <div class="text-sm text-indigo-800 space-y-3">
                    <p>Hệ thống cung cấp trải nghiệm làm bài tương tác dựa trên đề tài liệu gốc.</p>
                    <ul class="list-disc pl-5 space-y-1">
                        <li><strong>Bước 1:</strong> Chọn tab phần thi tương ứng.</li>
                        <li><strong>Bước 2:</strong> Tự làm bài và chọn/điền đáp án.</li>
                        <li><strong>Bước 3:</strong> Nhấn <em>"Xem Lời Giải"</em> để đối chiếu với đáp án chuẩn và phân tích các bước giải.</li>
                    </ul>
                </div>
            </div>
        </aside>

        <section class="lg:col-span-8 flex flex-col gap-6">
            
            <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-2">
                <div class="flex flex-wrap" id="tab-navigation">
                    <button class="tab-btn active flex-1 py-3 px-4 text-slate-500 hover:text-indigo-600 transition-colors text-center font-medium" data-target="part1">
                        Phần I: TN Khách Quan
                    </button>
                    <button class="tab-btn flex-1 py-3 px-4 text-slate-500 hover:text-indigo-600 transition-colors text-center font-medium" data-target="part2">
                        Phần II: Đúng/Sai
                    </button>
                    <button class="tab-btn flex-1 py-3 px-4 text-slate-500 hover:text-indigo-600 transition-colors text-center font-medium" data-target="part3">
                        Phần III: Trả Lời Ngắn
                    </button>
                </div>
            </div>

            <div id="content-area" class="flex flex-col gap-6 pb-12">
            </div>

        </section>
    </main>

    <script>
        const examData = {
            part1: {
                title: "Phần I. Câu Trắc Nghiệm Nhiều Phương Án Lựa Chọn",
                intro: "Thí sinh trả lời từ câu 1 đến câu 12. Mỗi câu hỏi thí sinh chỉ chọn một phương án đúng.",
                questions: [
                    { id: 1, text: "Căn bậc hai số học của $81$ là:", options: ["$-9$.", "$9$ và $-9$.", "$9$.", "$81$."], correct: 2, sol: "Căn bậc hai số học của một số thực dương $a$ là số dương $x$ sao cho $x^2 = a$. Vì $9^2 = 81$ và $9 > 0$ nên đáp án là $9$. Chọn C." },
                    { id: 2, text: "Hệ phương trình $\\begin{cases} x + 2y = 5 \\\\ 3x - 2y = 7 \\end{cases}$ có nghiệm $(x; y)$ là:", options: ["$(3; 1)$.", "$(1; 2)$.", "$(-3; 1)$.", "$(3; -1)$."], correct: 0, sol: "Cộng vế theo vế hai phương trình ta có: $4x = 12 \\Leftrightarrow x = 3$. Thay $x = 3$ vào $x + 2y = 5 \\Rightarrow 3 + 2y = 5 \\Rightarrow 2y = 2 \\Rightarrow y = 1$. Chọn A." },
                    { id: 3, text: "Cho tam giác $ABC$ vuông tại $A$ có $AB = 5cm$, $AC = 12cm$, $BC = 13cm$. Khẳng định nào sau đây đúng?", options: ["$\\sin B = \\frac{5}{13}$.", "$\\cos B = \\frac{12}{13}$.", "$\\tan B = \\frac{12}{5}$.", "$\\cot B = \\frac{13}{5}$."], correct: 2, sol: "Theo tỉ số lượng giác của góc nhọn trong tam giác vuông tại $A$: $\\tan B = \\frac{\\text{đối}}{\\text{kề}} = \\frac{AC}{AB} = \\frac{12}{5}$. Chọn C." },
                    { id: 4, text: "Gieo ngẫu nhiên một lần một con xúc xắc cân đối và đồng chất. Xác suất của biến cố \"Mặt xuất hiện của xúc xắc có số chấm lớn hơn 4\" là:", options: ["$\\frac{1}{2}$.", "$\\frac{1}{3}$.", "$\\frac{2}{3}$.", "$\\frac{1}{6}$."], correct: 1, sol: "Không gian mẫu có $6$ kết quả. Các kết quả thuận lợi là xuất hiện mặt $5$ chấm và $6$ chấm (có $2$ kết quả). Xác suất là $P = \\frac{2}{6} = \\frac{1}{3}$. Chọn B." },
                    { id: 5, text: "Điều kiện xác định của biểu thức $\\sqrt{5 - 2x}$ là:", options: ["$x \\ge \\frac{5}{2}$.", "$x \\le \\frac{5}{2}$.", "$x > \\frac{5}{2}$.", "$x < \\frac{5}{2}$."], correct: 1, sol: "Biểu thức dưới dấu căn phải không âm: $5 - 2x \\ge 0 \\Leftrightarrow -2x \\ge -5 \\Leftrightarrow x \\le \\frac{5}{2}$. Chọn B." },
                    { id: 6, text: "Hàm số $y = (m - 1)x + 3$ đồng biến trên $\\mathbb{R}$ khi:", options: ["$m < 1$.", "$m \\ne 1$.", "$m = 1$.", "$m > 1$."], correct: 3, sol: "Hàm số bậc nhất $y = ax + b$ đồng biến khi $a > 0$. Suy ra $m - 1 > 0 \\Leftrightarrow m > 1$. Chọn D." },
                    { id: 7, text: "Gọi $x_1, x_2$ là hai nghiệm của phương trình $x^2 - 7x + 10 = 0$. Tổng $x_1 + x_2$ bằng:", options: ["$7$.", "$-7$.", "$10$.", "$-10$."], correct: 0, sol: "Áp dụng hệ thức Vi-ét, tổng hai nghiệm $x_1 + x_2 = -\\frac{b}{a} = -\\frac{-7}{1} = 7$. Chọn A." },
                    { id: 8, text: "Đồ thị hàm số $y = 2x^2$ đi qua điểm nào dưới đây?", options: ["$M(1; -2)$.", "$N(-1; 2)$.", "$P(2; 4)$.", "$Q(-2; -8)$."], correct: 1, sol: "Thay tọa độ các điểm vào hàm số. Tại $x = -1 \\Rightarrow y = 2(-1)^2 = 2$. Vậy đồ thị đi qua $N(-1; 2)$. Chọn B." },
                    { id: 9, text: "Hai đường thẳng $d_1: y = 2x + 3$ và $d_2: y = (a - 1)x + 5$ song song với nhau khi và chỉ khi:", options: ["$a = 3$.", "$a = 2$.", "$a = -1$.", "$a = -3$."], correct: 0, sol: "Hai đường thẳng song song khi $a = a'$ và $b \\ne b'$. Tức là $a - 1 = 2 \\Leftrightarrow a = 3$ (và $5 \\ne 3$ luôn đúng). Chọn A." },
                    { id: 10, text: "Góc nội tiếp chắn nửa đường tròn có số đo bằng:", options: ["$45^\\circ$.", "$60^\\circ$.", "$90^\\circ$.", "$180^\\circ$."], correct: 2, sol: "Theo tính chất của đường tròn, góc nội tiếp chắn nửa đường tròn luôn là góc vuông ($90^\\circ$). Chọn C." },
                    { id: 11, text: "Một hình trụ có bán kính đáy $r = 3 cm$ và chiều cao $h = 4 cm$. Diện tích xung quanh của hình trụ đó là:", options: ["$12\\pi \\text{ cm}^2$.", "$24\\pi \\text{ cm}^2$.", "$36\\pi \\text{ cm}^2$.", "$48\\pi \\text{ cm}^2$."], correct: 1, sol: "Công thức tính diện tích xung quanh hình trụ: $S_{xq} = 2\\pi rh = 2\\pi \\cdot 3 \\cdot 4 = 24\\pi \\text{ cm}^2$. Chọn B." },
                    { id: 12, text: "Cho tứ giác $ABCD$ nội tiếp đường tròn $(O)$. Biết $\\angle A = 70^\\circ$, số đo của $\\angle C$ là:", options: ["$70^\\circ$.", "$110^\\circ$.", "$90^\\circ$.", "$20^\\circ$."], correct: 1, sol: "Tứ giác nội tiếp có tổng hai góc đối nhau bằng $180^\\circ$. Do đó $\\angle C = 180^\\circ - \\angle A = 180^\\circ - 70^\\circ = 110^\\circ$. Chọn B." }
                ]
            },
            part2: {
                title: "Phần II. Câu Trắc Nghiệm Đúng Sai",
                intro: "Thí sinh trả lời từ câu 13 đến câu 16. Trong mỗi ý a), b), c), d), chọn Đúng hoặc Sai.",
                questions: [
                    {
                        id: 13,
                        text: "Cho biểu thức $A = \\frac{\\sqrt{x} + 5}{\\sqrt{x} + 2}$ với $x \\ge 0$. Xét tính đúng, sai của các khẳng định sau:",
                        parts: [
                            { label: "a", text: "Khi $x = 9$, giá trị của biểu thức $A$ là $\\frac{8}{5}$.", ans: "ĐÚNG", sol: "Thay $x = 9$ (thỏa mãn ĐKXĐ) vào biểu thức $A$: <br> $A = \\frac{\\sqrt{9} + 5}{\\sqrt{9} + 2} = \\frac{3 + 5}{3 + 2} = \\frac{8}{5}$." },
                            { label: "b", text: "Biểu thức $A$ có thể biến đổi thành dạng $A = 1 + \\frac{3}{\\sqrt{x} + 2}$.", ans: "ĐÚNG", sol: "Ta biến đổi: <br> $A = \\frac{\\sqrt{x} + 5}{\\sqrt{x} + 2} = \\frac{\\sqrt{x} + 2 + 3}{\\sqrt{x} + 2} = \\frac{\\sqrt{x} + 2}{\\sqrt{x} + 2} + \\frac{3}{\\sqrt{x} + 2} = 1 + \\frac{3}{\\sqrt{x} + 2}$." },
                            { label: "c", text: "Với mọi $x \\ge 0$, ta luôn có $A \\ge 2$.", ans: "SAI", sol: "Ta có $x \\ge 0 \\Rightarrow \\sqrt{x} \\ge 0 \\Rightarrow \\sqrt{x} + 2 \\ge 2$. Suy ra $\\frac{3}{\\sqrt{x} + 2} \\le \\frac{3}{2}$. Do đó $A = 1 + \\frac{3}{\\sqrt{x} + 2} \\le 1 + \\frac{3}{2} = \\frac{5}{2}$. Ví dụ khi $x = 9 \\Rightarrow A = 1.6 < 2$. Vậy khẳng định $A \\ge 2$ với mọi $x$ là sai." },
                            { label: "d", text: "Có đúng $2$ giá trị nguyên của $x$ để biểu thức $A$ nhận giá trị nguyên.", ans: "SAI", sol: "Để $A$ nhận giá trị nguyên thì $\\frac{3}{\\sqrt{x} + 2}$ phải là số nguyên. Vì $x \\ge 0 \\Rightarrow \\sqrt{x} + 2 \\ge 2$. Nên $\\sqrt{x} + 2$ phải là ước nguyên dương lớn hơn hoặc bằng $2$ của $3$. Ước nguyên dương của $3$ thỏa mãn điều kiện này chỉ có $3$. Ta có: $\\sqrt{x} + 2 = 3 \\Leftrightarrow \\sqrt{x} = 1 \\Leftrightarrow x = 1$ (thỏa mãn). Vậy chỉ có đúng $1$ giá trị nguyên của $x$ để $A$ nguyên. Khẳng định sai." }
                        ]
                    },
                    {
                        id: 14,
                        text: "Cho hàm số $y = x^2$ có đồ thị $(P)$ và đường thẳng $(d): y = 2x + 3$. Xét tính đúng/sai của các khẳng định sau:",
                        parts: [
                            { label: "a", text: "Đồ thị $(P)$ đi qua điểm $M(-2; 4)$.", ans: "ĐÚNG", sol: "Thay $x = -2$ vào hàm số $y = x^2$, ta có $y = (-2)^2 = 4$. Vậy điểm $M(-2; 4)$ thuộc $(P)$." },
                            { label: "b", text: "Đường thẳng $(d)$ cắt trục tung tại điểm có tung độ bằng $-3$.", ans: "SAI", sol: "Giao điểm của $(d)$ với trục tung có hoành độ $x = 0$. Thay $x = 0$ vào $(d) \\Rightarrow y = 2(0) + 3 = 3$. Tung độ phải bằng $3$." },
                            { label: "c", text: "Đường thẳng $(d)$ cắt $(P)$ tại hai điểm phân biệt có hoành độ trái dấu.", ans: "ĐÚNG", sol: "Phương trình hoành độ giao điểm: $x^2 = 2x + 3 \\Leftrightarrow x^2 - 2x - 3 = 0$. Phương trình này có $a \\cdot c = 1 \\cdot (-3) = -3 < 0$ nên luôn có hai nghiệm phân biệt trái dấu." },
                            { label: "d", text: "Gọi $A, B$ là hai giao điểm của $(d)$ và $(P)$. Diện tích tam giác $OAB$ bằng $12$.", ans: "SAI", sol: "Giải phương trình $x^2 - 2x - 3 = 0$ được $x_1 = -1 \\Rightarrow A(-1; 1)$ và $x_2 = 3 \\Rightarrow B(3; 9)$. Kẻ $AH, BK$ vuông góc trục $Oy$. Diện tích $S_{OAB} = 6$ (chứ không phải $12$)." }
                        ]
                    },
                    {
                        id: 15,
                        text: "Cho đường tròn $(O; R)$ và điểm $M$ nằm ngoài đường tròn. Kẻ hai tiếp tuyến $MA, MB$ với $(O)$ ($A, B$ là tiếp điểm). Xét tính đúng sai:",
                        parts: [
                            { label: "a", text: "Tứ giác $MAOB$ nội tiếp đường tròn.", ans: "ĐÚNG", sol: "Vì $MA, MB$ là tiếp tuyến nên $\\angle MAO = \\angle MBO = 90^\\circ$. Suy ra $\\angle MAO + \\angle MBO = 180^\\circ$, nên tứ giác nội tiếp." },
                            { label: "b", text: "Kẻ đoạn thẳng $MO$ cắt đoạn $AB$ tại $H$. Ta có $\\angle MAB = \\angle MOA$.", ans: "ĐÚNG", sol: "Xét $\\Delta MAO$ vuông tại $A$, có đường cao $AH$. Ta có $\\angle MAB$ (tức $\\angle MAH$) và $\\angle MOA$ cùng phụ với $\\angle OMA$, do đó chúng bằng nhau." },
                            { label: "c", text: "Kẻ cát tuyến $MCD$ bất kỳ không đi qua $O$. Ta có $MA^2 = MC \\cdot MD$.", ans: "ĐÚNG", sol: "Xét $\\Delta MAC$ và $\\Delta MDA$ có $\\angle M$ chung, $\\angle MAC = \\angle MDA$ (cùng chắn cung $AC$). Suy ra hai tam giác đồng dạng, ta có $\\frac{MA}{MD} = \\frac{MC}{MA} \\Rightarrow MA^2 = MC \\cdot MD$." },
                            { label: "d", text: "Khi tam giác $MAB$ là tam giác đều, khoảng cách từ $M$ đến tâm $O$ là $R\\sqrt{3}$.", ans: "SAI", sol: "Nếu $\\Delta MAB$ đều thì $\\angle AMB = 60^\\circ \\Rightarrow \\angle AMO = 30^\\circ$. Trong tam giác vuông $MAO$, $\\sin 30^\\circ = \\frac{OA}{MO} \\Leftrightarrow \\frac{1}{2} = \\frac{R}{MO} \\Rightarrow MO = 2R$. Khẳng định $R\\sqrt{3}$ là sai." }
                        ]
                    },
                    {
                        id: 16,
                        text: "Cho phương trình $x^2 - (2m+1)x + m^2 - 1 = 0$ ($m$ là tham số). Xét tính đúng/sai:",
                        parts: [
                            { label: "a", text: "Khi $m = 0$, phương trình vô nghiệm.", ans: "SAI", sol: "Thay $m = 0$ vào, ta có phương trình: $x^2 - x - 1 = 0$. Có $\\Delta = (-1)^2 - 4(1)(-1) = 5 > 0$. Phương trình có 2 nghiệm phân biệt, vậy khẳng định vô nghiệm là sai." },
                            { label: "b", text: "Phương trình luôn có hai nghiệm phân biệt với mọi giá trị của tham số $m$.", ans: "SAI", sol: "Ta có $\\Delta = [-(2m+1)]^2 - 4(1)(m^2-1) = 4m + 5$. Để phương trình có 2 nghiệm phân biệt thì $\\Delta > 0 \\Leftrightarrow 4m + 5 > 0 \\Leftrightarrow m > -\\frac{5}{4}$. Khẳng định 'với mọi $m$' là sai." },
                            { label: "c", text: "Chỉ có duy nhất một giá trị nguyên của $m$ để phương trình có hai nghiệm trái dấu.", ans: "ĐÚNG", sol: "Để phương trình có 2 nghiệm trái dấu thì $a \\cdot c < 0 \\Leftrightarrow 1 \\cdot (m^2 - 1) < 0 \\Leftrightarrow -1 < m < 1$. Mà $m \\in \\mathbb{Z} \\Rightarrow m = 0$. Có đúng 1 giá trị nguyên thỏa mãn." },
                            { label: "d", text: "Gọi $x_1, x_2$ là hai nghiệm của phương trình (khi $m \\ge -\\frac{5}{4}$). Giá trị nhỏ nhất của biểu thức $P = x_1^2 + x_2^2 - x_1x_2$ là $1$.", ans: "SAI", sol: "Biến đổi $P = (x_1 + x_2)^2 - 3x_1x_2 = (2m+1)^2 - 3(m^2-1) = m^2+4m+4 = (m+2)^2$. Vì $m \\ge -\\frac{5}{4}$ nên $m+2 \\ge \\frac{3}{4} \\Rightarrow (m+2)^2 \\ge \\frac{9}{16}$. Giá trị nhỏ nhất là $\\frac{9}{16}$." }
                        ]
                    }
                ]
            },
            part3: {
                title: "Phần III. Câu Trả Lời Ngắn",
                intro: "Thí sinh điền đáp án/ trả lời ngắn gọn vào chỗ trống hoặc trình bày vắn tắt. Bạn có thể dùng nháp bên dưới trước khi xem cách giải chi tiết.",
                questions: [
                    {
                        id: 17,
                        text: "Một chiếc thang dài $5m$ được dựa vào một bức tường đứng thẳng. Biết góc tạo bởi chiếc thang và mặt đất là $65^\\circ$. Tính khoảng cách từ chân thang đến chân tường (làm tròn đến chữ số thập phân thứ hai).",
                        sol: "Gọi chiều dài chiếc thang là cạnh huyền $BC = 5m$, góc tạo bởi thang và mặt đất là góc nhọn $\\angle B = 65^\\circ$, khoảng cách từ chân thang đến chân tường là cạnh kề $AB$.<br>Xét tam giác vuông $ABC$ vuông tại $A$:<br>Ta có: $\\cos B = \\frac{AB}{BC} \\Rightarrow AB = BC \\cdot \\cos B$<br>$\\Rightarrow AB = 5 \\cdot \\cos 65^\\circ \\approx 2,11 \\text{ (m)}$<br><strong class='text-indigo-700 mt-2 block'>Đáp số: $2,11$ m</strong>"
                    },
                    {
                        id: 18,
                        text: "Một người quan sát đứng cách chân một tòa tháp $20m$ nhìn lên đỉnh tháp với góc nâng $60^\\circ$ (góc tạo bởi phương nhìn và phương nằm ngang). Biết khoảng cách từ mắt người quan sát đến mặt đất là $1,6m$. Tính chiều cao của tòa tháp (làm tròn đến chữ số thập phân thứ hai).",
                        sol: "Mô hình hóa bài toán: Gọi $CD$ là chiều cao tháp, điểm đặt mắt quan sát là $A$, khoảng cách từ mắt đến mặt đất là $AB = 1,6m$, khoảng cách từ người đến tháp là $BC = 20m$.<br>Kẻ $AH \\perp CD$ tại $H$. Khi đó tứ giác $ABCH$ là hình chữ nhật nên $AH = BC = 20m$; $HC = AB = 1,6m$.<br>Góc nâng $\\angle DAH = 60^\\circ$.<br>Xét $\\Delta AHD$ vuông tại $H$:<br>Ta có: $\\tan(\\angle DAH) = \\frac{DH}{AH} \\Rightarrow DH = AH \\cdot \\tan 60^\\circ = 20 \\cdot \\sqrt{3} \\approx 34,64 \\text{ (m)}$.<br>Chiều cao của tòa tháp là:<br>$CD = DH + HC \\approx 34,64 + 1,6 = 36,24 \\text{ (m)}$.<br><strong class='text-indigo-700 mt-2 block'>Đáp số: $36,24$ m</strong>"
                    },
                    {
                        id: 19,
                        text: "Bác An gửi tiết kiệm $300$ triệu đồng vào ngân hàng với kỳ hạn $1$ năm, lãi suất $6\\%$/năm theo hình thức lãi kép (tiền lãi của năm trước được cộng gộp vào tiền vốn để tính lãi cho năm sau). Hỏi sau đúng $2$ năm, bác An rút cả vốn lẫn lãi được bao nhiêu triệu đồng?",
                        sol: "Áp dụng công thức tính lãi kép: $T = A \\cdot (1 + r)^n$<br>Trong đó: $A = 300$ (triệu đồng), $r = 6\\% = 0,06$, $n = 2$ (năm).<br>Số tiền cả vốn lẫn lãi bác An nhận được sau 2 năm là:<br>$T = 300 \\cdot (1 + 0,06)^2 = 300 \\cdot 1,1236 = 337,08$ (triệu đồng).<br><strong class='text-indigo-700 mt-2 block'>Đáp số: $337,08$ triệu đồng</strong>"
                    },
                    {
                        id: 20,
                        text: "Gọi $x_1, x_2$ là hai nghiệm của phương trình $x^2 - 5x + 3 = 0$. Tính giá trị của biểu thức $T = x_1^2 + x_2^2$.",
                        sol: "Phương trình có $\\Delta = (-5)^2 - 4(1)(3) = 13 > 0$ nên luôn có hai nghiệm phân biệt.<br>Áp dụng hệ thức Vi-ét, ta có: $x_1 + x_2 = 5$ và $x_1x_2 = 3$.<br>Ta biến đổi biểu thức: $T = x_1^2 + x_2^2 = (x_1 + x_2)^2 - 2x_1x_2$.<br>Thay số vào, ta được: $T = 5^2 - 2 \\cdot 3 = 25 - 6 = 19$.<br><strong class='text-indigo-700 mt-2 block'>Đáp số: $19$</strong>"
                    },
                    {
                        id: 21,
                        text: "Hai vòi nước cùng chảy vào một bể không có nước thì sau $6$ giờ đầy bể. Nếu mở vòi 1 chảy một mình trong $2$ giờ rồi khóa lại, mở tiếp vòi 2 chảy trong $3$ giờ thì được $\\frac{2}{5}$ bể. Hỏi nếu chảy một mình thì vòi 1 chảy đầy bể trong bao lâu?",
                        sol: "Gọi thời gian vòi 1 và vòi 2 chảy một mình đầy bể lần lượt là $x$ và $y$ (giờ) ($x, y > 6$).<br>Trong 1 giờ, vòi 1 chảy được $\\frac{1}{x}$ bể, vòi 2 chảy được $\\frac{1}{y}$ bể. Cả hai vòi chảy được $\\frac{1}{6}$ bể.<br>Ta có hệ phương trình: $\\begin{cases} \\frac{1}{x} + \\frac{1}{y} = \\frac{1}{6} \\\\ \\frac{2}{x} + \\frac{3}{y} = \\frac{2}{5} \\end{cases}$<br>Đặt $u = \\frac{1}{x}, v = \\frac{1}{y}$. Hệ trở thành: $\\begin{cases} u + v = \\frac{1}{6} \\\\ 2u + 3v = \\frac{2}{5} \\end{cases} \\Rightarrow \\begin{cases} 2u + 2v = \\frac{1}{3} \\\\ 2u + 3v = \\frac{2}{5} \\end{cases} \\Rightarrow v = \\frac{2}{5} - \\frac{1}{3} = \\frac{1}{15}$<br>Suy ra $u = \\frac{1}{6} - \\frac{1}{15} = \\frac{1}{10}$.<br>Vậy $\\frac{1}{x} = \\frac{1}{10} \\Rightarrow x = 10$ (thỏa mãn ĐK).<br><strong class='text-indigo-700 mt-2 block'>Đáp số: $10$ giờ</strong>"
                    },
                    {
                        id: 22,
                        text: "Một quả bóng đá tiêu chuẩn có dạng hình cầu với bán kính khoảng $11cm$. Tính thể tích của quả bóng đó (Lấy $\\pi \\approx 3,14$ và làm tròn đến hàng đơn vị).",
                        sol: "Thể tích của hình cầu được tính theo công thức: $V = \\frac{4}{3}\\pi R^3$<br>Trong đó $R = 11cm$ và $\\pi \\approx 3,14$.<br>Thay số vào, ta có: $V = \\frac{4}{3} \\cdot 3,14 \\cdot 11^3 = \\frac{4}{3} \\cdot 3,14 \\cdot 1331 \\approx 5572,45 \\text{ (cm}^3)$<br>Làm tròn đến hàng đơn vị ta được $5572 \\text{ cm}^3$.<br><strong class='text-indigo-700 mt-2 block'>Đáp số: $5572 \\text{ cm}^3$</strong>"
                    }
                ]
            }
        };

        const contentArea = document.getElementById('content-area');
        const tabBtns = document.querySelectorAll('.tab-btn');

        function renderKaTeX() {
            renderMathInElement(contentArea, {
                delimiters: [
                    {left: "$$", right: "$$", display: true},
                    {left: "$", right: "$", display: false}
                ],
                throwOnError: false
            });
        }

        function toggleSolutionBlock(id, btnElement) {
            const solBlock = document.getElementById(id);
            if (solBlock.classList.contains('show')) {
                solBlock.classList.remove('show');
                btnElement.innerHTML = '<span>👁️</span> Xem Lời Giải';
                btnElement.classList.replace('bg-slate-200', 'bg-indigo-100');
                btnElement.classList.replace('text-slate-700', 'text-indigo-800');
            } else {
                solBlock.classList.add('show');
                btnElement.innerHTML = '<span>🙈</span> Ẩn Lời Giải';
                btnElement.classList.replace('bg-indigo-100', 'bg-slate-200');
                btnElement.classList.replace('text-indigo-800', 'text-slate-700');
            }
        }

        function renderHeader(title, intro) {
            return `
                <div class="mb-4">
                    <h2 class="text-xl font-bold text-slate-800 mb-2">${title}</h2>
                    <p class="bg-indigo-50 border-l-4 border-indigo-500 p-4 rounded-r-lg text-indigo-900 text-sm">${intro}</p>
                </div>
            `;
        }

        function renderPart1() {
            let html = renderHeader(examData.part1.title, examData.part1.intro);
            const letters = ['A', 'B', 'C', 'D'];
            
            examData.part1.questions.forEach((q) => {
                let optionsHtml = '';
                q.options.forEach((opt, oIndex) => {
                    optionsHtml += `
                        <div class="relative">
                            <input type="radio" name="q${q.id}" id="q${q.id}_${oIndex}" class="peer hidden">
                            <label for="q${q.id}_${oIndex}" class="flex items-center border border-slate-200 rounded-xl p-3 cursor-pointer hover:bg-slate-50 peer-checked:bg-indigo-50 peer-checked:border-indigo-400 peer-checked:text-indigo-900 transition-all math-block text-sm">
                                <span class="font-bold mr-3 w-6 h-6 flex items-center justify-center rounded-full bg-slate-100 text-slate-600 peer-checked:bg-indigo-600 peer-checked:text-white transition-colors">${letters[oIndex]}</span> 
                                <span>${opt}</span>
                            </label>
                        </div>
                    `;
                });

                html += `
                    <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-6 hover:shadow-md transition-shadow">
                        <div class="flex items-center justify-between mb-4 border-b pb-3">
                            <h3 class="font-bold text-lg text-slate-800">Câu ${q.id}</h3>
                        </div>
                        <div class="text-slate-800 mb-6 math-block text-base leading-relaxed">${q.text}</div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                            ${optionsHtml}
                        </div>
                        <div class="border-t pt-4 mt-2">
                            <button onclick="toggleSolutionBlock('sol-${q.id}', this)" class="bg-indigo-100 text-indigo-800 hover:bg-indigo-200 font-semibold py-2.5 px-5 rounded-xl transition-colors flex items-center gap-2 text-sm">
                                <span>👁️</span> Xem Lời Giải
                            </button>
                        </div>
                        <div id="sol-${q.id}" class="solution-block mt-4">
                            <div class="bg-slate-50 border border-slate-200 rounded-xl p-5">
                                <p class="font-bold text-emerald-600 mb-3 flex items-center gap-2"><span>✅</span> Đáp án đúng: ${letters[q.correct]}</p>
                                <div class="text-slate-700 math-block leading-relaxed border-t border-slate-200 pt-3">${q.sol}</div>
                            </div>
                        </div>
                    </div>
                `;
            });
            contentArea.innerHTML = html;
            renderKaTeX();
        }

        window.toggleTF = function(btn, type) {
            const container = btn.closest('.tf-container');
            const btns = container.querySelectorAll('.tf-btn');
            btns.forEach(b => b.classList.remove('active-true', 'active-false'));
            if(type === 'true') {
                btn.classList.add('active-true');
            } else {
                btn.classList.add('active-false');
            }
        };

        function renderPart2() {
            let html = renderHeader(examData.part2.title, examData.part2.intro);
            
            examData.part2.questions.forEach((q) => {
                let partsHtml = '';
                q.parts.forEach((p) => {
                    partsHtml += `
                        <div class="border border-slate-200 rounded-xl p-5 bg-white shadow-sm hover:border-indigo-200 transition-colors">
                            <div class="flex flex-col md:flex-row md:justify-between md:items-start gap-5">
                                <div class="math-block text-slate-800 flex-1 text-base leading-relaxed">
                                    <span class="font-bold text-indigo-600 mr-2 bg-indigo-50 w-8 h-8 inline-flex items-center justify-center rounded-full">${p.label}</span> 
                                    ${p.text}
                                </div>
                                <div class="flex gap-2 shrink-0 tf-container bg-slate-50 p-1 rounded-lg border border-slate-100">
                                    <button onclick="toggleTF(this, 'true')" class="tf-btn border border-slate-300 text-slate-600 px-4 py-1.5 rounded-md hover:bg-emerald-50 hover:text-emerald-700 transition font-medium text-sm">Đúng</button>
                                    <button onclick="toggleTF(this, 'false')" class="tf-btn border border-slate-300 text-slate-600 px-4 py-1.5 rounded-md hover:bg-red-50 hover:text-red-700 transition font-medium text-sm">Sai</button>
                                </div>
                            </div>
                            <div class="mt-5 pt-4 border-t border-slate-100">
                                <button onclick="toggleSolutionBlock('sol-${q.id}-${p.label}', this)" class="text-sm bg-slate-100 text-slate-600 font-semibold py-1.5 px-4 rounded-lg hover:bg-slate-200 transition">Hiển thị giải thích</button>
                                <div id="sol-${q.id}-${p.label}" class="solution-block mt-3">
                                    <div class="bg-indigo-50 border border-indigo-100 rounded-xl p-4 text-sm">
                                        <div class="flex items-center gap-2 mb-2 pb-2 border-b border-indigo-100">
                                            <span class="font-bold ${p.ans === 'ĐÚNG' ? 'text-emerald-600' : 'text-rose-600'}">Kết luận: Khẳng định này ${p.ans}</span>
                                        </div>
                                        <div class="text-slate-700 math-block leading-relaxed">${p.sol}</div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    `;
                });

                html += `
                    <div class="bg-slate-50 rounded-2xl shadow-inner border border-slate-200 p-6">
                        <div class="flex items-center justify-between mb-4 border-b border-slate-300 pb-3">
                            <h3 class="font-bold text-lg text-slate-800">Câu ${q.id}</h3>
                        </div>
                        <div class="text-slate-800 mb-6 math-block text-lg font-medium bg-white p-4 rounded-xl shadow-sm border border-slate-100">${q.text}</div>
                        <div class="space-y-4">
                            ${partsHtml}
                        </div>
                    </div>
                `;
            });
            contentArea.innerHTML = html;
            renderKaTeX();
        }

        function renderPart3() {
            let html = renderHeader(examData.part3.title, examData.part3.intro);
            
            examData.part3.questions.forEach((q) => {
                html += `
                    <div class="bg-white rounded-2xl shadow-sm border border-slate-200 p-6 hover:shadow-md transition-shadow">
                        <div class="flex items-center justify-between mb-4 border-b pb-3">
                            <h3 class="font-bold text-lg text-slate-800">Câu ${q.id}</h3>
                        </div>
                        <div class="text-slate-800 mb-5 math-block text-base leading-relaxed bg-slate-50 p-5 rounded-xl border border-slate-100">${q.text}</div>
                        
                        <div class="mb-5">
                            <label class="block text-sm font-semibold text-slate-600 mb-2">Khu vực nháp / Ghi chú kết quả:</label>
                            <textarea placeholder="Ghi chú các bước tính toán hoặc đáp số cuối cùng của bạn..." class="w-full border border-slate-300 rounded-xl p-4 text-sm h-28 focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500 outline-none transition-shadow bg-slate-50"></textarea>
                        </div>

                        <div class="border-t pt-4 mt-2">
                            <button onclick="toggleSolutionBlock('sol-${q.id}', this)" class="bg-indigo-100 text-indigo-800 hover:bg-indigo-200 font-semibold py-2.5 px-5 rounded-xl transition-colors flex items-center gap-2 text-sm">
                                <span>✍️</span> Xem Lời Giải Chi Tiết
                            </button>
                        </div>
                        <div id="sol-${q.id}" class="solution-block mt-4">
                            <div class="bg-indigo-50 border border-indigo-200 rounded-xl p-6">
                                <h4 class="font-bold text-indigo-900 mb-3 border-b border-indigo-200 pb-2">Hướng dẫn giải:</h4>
                                <div class="text-slate-800 math-block leading-relaxed space-y-2">${q.sol}</div>
                            </div>
                        </div>
                    </div>
                `;
            });
            contentArea.innerHTML = html;
            renderKaTeX();
        }

        tabBtns.forEach(btn => {
            btn.addEventListener('click', (e) => {
                tabBtns.forEach(b => b.classList.remove('active', 'border-indigo-600', 'text-indigo-600'));
                e.target.classList.add('active', 'border-indigo-600', 'text-indigo-600');
                
                const target = e.target.getAttribute('data-target');
                if (target === 'part1') renderPart1();
                if (target === 'part2') renderPart2();
                if (target === 'part3') renderPart3();
            });
        });

        document.addEventListener('DOMContentLoaded', () => {
            renderPart1();

            const ctx = document.getElementById('examStructureChart').getContext('2d');
            new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ['Phần I: Trắc nghiệm', 'Phần II: Đúng/Sai', 'Phần III: Trả lời ngắn'],
                    datasets: [{
                        data: [12, 4, 6],
                        backgroundColor: [
                            '#6366f1', 
                            '#f59e0b', 
                            '#10b981'  
                        ],
                        borderWidth: 2,
                        borderColor: '#ffffff',
                        hoverOffset: 6
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        },
                        tooltip: {
                            backgroundColor: 'rgba(15, 23, 42, 0.9)',
                            titleFont: { size: 13, family: 'system-ui' },
                            bodyFont: { size: 14, family: 'system-ui', weight: 'bold' },
                            padding: 12,
                            cornerRadius: 8,
                            callbacks: {
                                label: function(context) {
                                    return ' ' + context.raw + ' câu hỏi';
                                }
                            }
                        }
                    },
                    cutout: '70%'
                }
            });
        });

    </script>
</body>
</html>
