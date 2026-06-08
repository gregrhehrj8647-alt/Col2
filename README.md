<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>대학 진학 컨설팅 시스템</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
            overflow: hidden;
        }

        header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 40px 20px;
            text-align: center;
        }

        header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
        }

        header p {
            font-size: 1.1em;
            opacity: 0.9;
        }

        .content {
            display: flex;
            gap: 20px;
            padding: 30px;
        }

        .sidebar {
            width: 300px;
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            height: fit-content;
            position: sticky;
            top: 20px;
        }

        .sidebar h2 {
            color: #667eea;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .nav-button {
            display: block;
            width: 100%;
            padding: 12px 15px;
            margin-bottom: 10px;
            background: white;
            border: 2px solid #667eea;
            color: #667eea;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1em;
            transition: all 0.3s ease;
        }

        .nav-button:hover,
        .nav-button.active {
            background: #667eea;
            color: white;
        }

        .main-content {
            flex: 1;
        }

        .section {
            display: none;
            animation: fadeIn 0.5s ease;
        }

        .section.active {
            display: block;
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

        .card {
            background: white;
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 20px;
            border-left: 5px solid #667eea;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }

        .card h3 {
            color: #667eea;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #333;
            font-weight: 600;
        }

        input,
        select {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 1em;
            transition: border-color 0.3s ease;
        }

        input:focus,
        select:focus {
            outline: none;
            border-color: #667eea;
        }

        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }

        button {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 12px 30px;
            border: none;
            border-radius: 8px;
            font-size: 1em;
            cursor: pointer;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(102, 126, 234, 0.4);
        }

        .info-box {
            background: #f0f4ff;
            border-left: 4px solid #667eea;
            padding: 15px;
            margin-bottom: 15px;
            border-radius: 5px;
        }

        .grade-table {
            width: 100%;
            border-collapse: collapse;
            margin: 15px 0;
        }

        .grade-table th,
        .grade-table td {
            padding: 12px;
            text-align: center;
            border: 1px solid #ddd;
        }

        .grade-table th {
            background: #667eea;
            color: white;
        }

        .grade-table tr:nth-child(even) {
            background: #f8f9fa;
        }

        .result-item {
            background: #f8f9fa;
            padding: 15px;
            margin-bottom: 15px;
            border-radius: 8px;
            border-left: 4px solid #667eea;
        }

        .result-item h4 {
            color: #667eea;
            margin-bottom: 8px;
        }

        .result-item p {
            margin: 5px 0;
            color: #555;
        }

        .university-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
        }

        .university-card {
            background: white;
            border-radius: 10px;
            padding: 20px;
            border: 2px solid #e0e0e0;
            transition: all 0.3s ease;
        }

        .university-card:hover {
            border-color: #667eea;
            box-shadow: 0 5px 20px rgba(102, 126, 234, 0.3);
        }

        .university-card h4 {
            color: #667eea;
            margin-bottom: 10px;
        }

        .university-card p {
            margin: 5px 0;
            color: #666;
            font-size: 0.95em;
        }

        .tag {
            display: inline-block;
            background: #667eea;
            color: white;
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 0.85em;
            margin-right: 5px;
            margin-top: 5px;
        }

        .recommendation-result {
            background: linear-gradient(135deg, #e8f5e9 0%, #f1f8e9 100%);
            border-left: 4px solid #4caf50;
            padding: 20px;
            margin: 20px 0;
            border-radius: 8px;
        }

        .recommendation-result h3 {
            color: #2e7d32;
            margin-bottom: 15px;
        }

        .warning-box {
            background: #fff3cd;
            border-left: 4px solid #ffc107;
            padding: 15px;
            margin: 15px 0;
            border-radius: 5px;
        }

        @media (max-width: 768px) {
            .content {
                flex-direction: column;
            }

            .sidebar {
                width: 100%;
                position: static;
            }

            .form-row {
                grid-template-columns: 1fr;
            }

            .university-list {
                grid-template-columns: 1fr;
            }

            header h1 {
                font-size: 1.8em;
            }
        }

        .footer {
            background: #f8f9fa;
            padding: 20px;
            text-align: center;
            color: #666;
            border-top: 1px solid #ddd;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🎓 대학 진학 컨설팅 시스템</h1>
            <p>당신의 내신 성적으로 지원 가능한 대학을 찾아보세요</p>
        </header>

        <div class="content">
            <div class="sidebar">
                <h2>메뉴</h2>
                <button class="nav-button active" onclick="showSection('intro')">소개</button>
                <button class="nav-button" onclick="showSection('gradeSystem')">등급제 정보</button>
                <button class="nav-button" onclick="showSection('calculator')">내신 계산기</button>
                <button class="nav-button" onclick="showSection('recommendation')">대학 추천</button>
                <button class="nav-button" onclick="showSection('database')">대학 정보</button>
            </div>

            <div class="main-content">
                <!-- 소개 섹션 -->
                <div id="intro" class="section active">
                    <div class="card">
                        <h3>🎯 시스템 소개</h3>
                        <p>이 시스템은 고등학생 여러분이 자신의 내신 성적과 관심 교과를 바탕으로 지원 가능한 대학과 학과를 탐색할 수 있도록 설계되었습니다.</p>
                    </div>

                    <div class="card">
                        <h3>📚 주요 기능</h3>
                        <ul style="margin-left: 20px; line-height: 1.8;">
                            <li><strong>등급제 정보 제공:</strong> 9등급제와 2028학년도 적용 5등급제 비교</li>
                            <li><strong>내신 계산:</strong> 학년별 성적을 입력하면 종합 내신 계산</li>
                            <li><strong>대학 추천:</strong> 당신의 성적에 맞는 대학 실시간 추천</li>
                            <li><strong>대학 정보:</strong> 전국 주요 대학 입시 정보 데이터베이스</li>
                        </ul>
                    </div>

                    <div class="card">
                        <h3>💡 활용 팁</h3>
                        <div class="info-box">
                            <p>📌 <strong>등급제 정보</strong>에서 9등급제와 5등급제의 차이를 먼저 이해하세요.</p>
                        </div>
                        <div class="info-box">
                            <p>📌 <strong>내신 계산기</strong>를 통해 학년별 성적을 입력하면 종합 내신이 자동 계산됩니다.</p>
                        </div>
                        <div class="info-box">
                            <p>📌 <strong>대학 추천</strong>에서 당신의 성적에 맞는 대학을 확인하세요. 수시와 정시 전형을 모두 고려합니다.</p>
                        </div>
                    </div>
                </div>

                <!-- 등급제 정보 섹션 -->
                <div id="gradeSystem" class="section">
                    <div class="card">
                        <h3>📊 현행 9등급제 (2025학년도까지)</h3>
                        <table class="grade-table">
                            <thead>
                                <tr>
                                    <th>등급</th>
                                    <th>1등급</th>
                                    <th>2등급</th>
                                    <th>3등급</th>
                                    <th>4등급</th>
                                    <th>5등급</th>
                                    <th>6등급</th>
                                    <th>7등급</th>
                                    <th>8등급</th>
                                    <th>9등급</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td style="font-weight: bold;">누적 인원비율</td>
                                    <td>4%</td>
                                    <td>11%</td>
                                    <td>23%</td>
                                    <td>40%</td>
                                    <td>60%</td>
                                    <td>77%</td>
                                    <td>89%</td>
                                    <td>96%</td>
                                    <td>100%</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>

                    <div class="card">
                        <h3>📈 신규 5등급제 (2028학년도부터)</h3>
                        <table class="grade-table">
                            <thead>
                                <tr>
                                    <th>등급</th>
                                    <th>1등급</th>
                                    <th>2등급</th>
                                    <th>3등급</th>
                                    <th>4등급</th>
                                    <th>5등급</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td style="font-weight: bold;">인원비율</td>
                                    <td>10%</td>
                                    <td>24%</td>
                                    <td>32%</td>
                                    <td>24%</td>
                                    <td>10%</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- 내신 계산기 섹션 -->
                <div id="calculator" class="section">
                    <div class="card">
                        <h3>📝 내신 계산기</h3>
                        <div class="form-group">
                            <label>1학년 내신 등급 (반영 비율 10%)</label>
                            <input type="number" id="grade1" min="1" max="9" placeholder="1~9 사이의 값">
                        </div>
                        <div class="form-group">
                            <label>2학년 내신 등급 (반영 비율 20%)</label>
                            <input type="number" id="grade2" min="1" max="9" placeholder="1~9 사이의 값">
                        </div>
                        <div class="form-group">
                            <label>3학년 내신 등급 (반영 비율 70%)</label>
                            <input type="number" id="grade3" min="1" max="9" placeholder="1~9 사이의 값">
                        </div>
                        <button onclick="calculateGPA()" style="width: 100%;">내신 계산하기</button>
                        <div id="calculatorResult" style="margin-top: 20px;"></div>
                    </div>
                </div>

                <!-- 대학 추천 섹션 -->
                <div id="recommendation" class="section">
                    <div class="card">
                        <h3>🎓 대학 추천</h3>
                        <div class="form-group">
                            <label>내신 등급을 입력하세요</label>
                            <input type="number" id="recommendGrade" min="1" max="9" step="0.1" placeholder="예: 2.5">
                        </div>
                        <button onclick="recommendUniversities()" style="width: 100%;">대학 추천받기</button>
                        <div id="recommendationResult" style="margin-top: 20px;"></div>
                    </div>
                </div>

                <!-- 대학 정보 섹션 -->
                <div id="database" class="section">
                    <div class="card">
                        <h3>🏫 대학 정보 데이터베이스</h3>
                        <div id="databaseResult" style="margin-top: 20px;"></div>
                    </div>
                </div>
            </div>
        </div>

        <div class="footer">
            <p>📚 본 시스템의 데이터는 참고용입니다. 각 대학 입학처 공식 홈페이지에서 최신 정보를 확인하세요.</p>
        </div>
    </div>

    <script>
        const universityDatabase = [
            { name: '서울대학교', region: '서울', minGrade: 1.0, maxGrade: 2.0, susuRate: '60%', jeongsiRate: '40%' },
            { name: '카이스트(KAIST)', region: '대전', minGrade: 1.0, maxGrade: 2.0, susuRate: '50%', jeongsiRate: '50%' },
            { name: '연세대학교', region: '서울', minGrade: 1.2, maxGrade: 2.5, susuRate: '70%', jeongsiRate: '30%' },
            { name: '고려대학교', region: '서울', minGrade: 1.2, maxGrade: 2.5, susuRate: '75%', jeongsiRate: '25%' },
            { name: '성균관대학교', region: '서울', minGrade: 2.0, maxGrade: 3.0, susuRate: '80%', jeongsiRate: '20%' },
            { name: '한양대학교', region: '서울', minGrade: 2.0, maxGrade: 3.2, susuRate: '75%', jeongsiRate: '25%' },
            { name: '중앙대학교', region: '서울', minGrade: 2.3, maxGrade: 3.5, susuRate: '85%', jeongsiRate: '15%' },
            { name: '경희대학교', region: '서울', minGrade: 3.5, maxGrade: 4.5, susuRate: '75%', jeongsiRate: '25%' },
            { name: '인하대학교', region: '인천', minGrade: 3.5, maxGrade: 4.5, susuRate: '70%', jeongsiRate: '30%' },
            { name: '단국대학교', region: '경기', minGrade: 3.8, maxGrade: 5.0, susuRate: '85%', jeongsiRate: '15%' }
        ];

        function showSection(sectionId) {
            document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
            document.getElementById(sectionId).classList.add('active');
            document.querySelectorAll('.nav-button').forEach(b => b.classList.remove('active'));
            event.target.classList.add('active');
        }

        function calculateGPA() {
            const grade1 = parseFloat(document.getElementById('grade1').value);
            const grade2 = parseFloat(document.getElementById('grade2').value);
            const grade3 = parseFloat(document.getElementById('grade3').value);

            if (!grade1 || !grade2 || !grade3) {
                alert('모든 학년의 등급을 입력해주세요.');
                return;
            }

            const gpa = (grade1 * 0.1) + (grade2 * 0.2) + (grade3 * 0.7);
            const roundedGpa = Math.round(gpa * 100) / 100;

            let evaluation = roundedGpa <= 2.0 ? '최상위권' : roundedGpa <= 3.0 ? '상위권' : roundedGpa <= 4.0 ? '중상위권' : '중위권 이하';

            document.getElementById('calculatorResult').innerHTML = `
                <div class="recommendation-result">
                    <h3>계산 결과</h3>
                    <p style="font-size: 1.3em; font-weight: bold; color: #2e7d32;">
                        종합 내신 등급: <span style="color: #667eea;">${roundedGpa}</span>
                    </p>
                    <p style="margin-top: 15px;">평가: <strong>${evaluation}</strong></p>
                </div>
            `;
        }

        function recommendUniversities() {
            const grade = parseFloat(document.getElementById('recommendGrade').value);
            if (!grade) {
                alert('내신 등급을 입력해주세요.');
                return;
            }

            const filtered = universityDatabase.filter(uni => grade >= uni.minGrade && grade <= uni.maxGrade);

            if (filtered.length === 0) {
                document.getElementById('recommendationResult').innerHTML = '<p>검색 결과가 없습니다.</p>';
                return;
            }

            let html = '<div class="university-list>';
            filtered.forEach(uni => {
                html += `
                    <div class="university-card">
                        <h4>${uni.name}</h4>
                        <p><strong>지역:</strong> ${uni.region}</p>
                        <p><strong>등급:</strong> ${uni.minGrade}~${uni.maxGrade}</p>
                        <p><strong>수시:</strong> ${uni.susuRate} / <strong>정시:</strong> ${uni.jeongsiRate}</p>
                    </div>
                `;
            });
            html += '</div>';
            document.getElementById('recommendationResult').innerHTML = html;
        }

        window.addEventListener('load', function() {
            let html = '<div class="university-list>';
            universityDatabase.forEach(uni => {
                html += `
                    <div class="university-card">
                        <h4>${uni.name}</h4>
                        <p><strong>지역:</strong> ${uni.region}</p>
                        <p><strong>등급:</strong> ${uni.minGrade}~${uni.maxGrade}</p>
                        <p><strong>수시:</strong> ${uni.susuRate} / <strong>정시:</strong> ${uni.jeongsiRate}</p>
                    </div>
                `;
            });
            html += '</div>';
            document.getElementById('databaseResult').innerHTML = html;
        });
    </script>
</body>
</html>
