<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>تقييم خطورة الصيام لمرضى السكري</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background: #f8f9fa;
            color: #1D3E6A;
        }
        .question-box {
            background: white;
            padding: 20px;
            margin: 15px 0;
            border-radius: 10px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }
        .result-box {
            padding: 25px;
            margin: 25px 0;
            border-radius: 12px;
            font-size: 20px;
            text-align: center;
        }
        .high-risk { background: #F15E5D; border: 2px solid #c62828; color: white; }
        .medium-risk { background: #fff3e0; border: 2px solid #ef6c00; }
        .low-risk { background: #e8f5e9; border: 2px solid #2e7d32; }
        button {
            background: #1D3E6A;
            color: white;
            padding: 15px 30px;
            font-size: 18px;
            border-radius: 8px;
            margin: 20px 0;
            cursor: pointer;
        }
    </style>
</head>
<body>
    
    <h1 style="text-align: center;">تقييم خطورة الصيام في شهر رمضان لمرضى السكري<br>عيادة الدكتور أبو كياس</h1>

    <div class="question-box">
        <h3>1. نوع السكري:</h3>
        <select id="q1">
            <option value="1.5">النوع الأول</option>
            <option value="1">النوع الثاني</option>
            <option value="0.5">سكري الحمل</option>
        </select>
    </div>

    <div class="question-box">
        <h3>2. مدة الإصابة بالسكري:</h3>
        <select id="q2">
            <option value="2">أكثر من 10 سنوات</option>
            <option value="1">5-10 سنوات</option>
            <option value="0.5">أقل من 5 سنوات</option>
        </select>
    </div>

    <div class="question-box">
        <h3>3. هل أنتِ حامل؟</h3>
        <select id="q3">
            <option value="2">نعم - مع سكري غير متوازن</option>
            <option value="1">نعم - مع سكري متوازن</option>
            <option value="0">لا</option>
        </select>
    </div>

    <div class="question-box">
        <h3>4. نوع العلاج:</h3>
        <select id="q4">
            <option value="2">مضخة الأنسولين</option>
            <option value="1.5">الأنسولين المخلوط</option>
            <option value="1">السلفونيل يوريا</option>
            <option value="0.5">أدوية غير مسببة لهبوط السكر</option>
        </select>
    </div>

    <div class="question-box">
        <h3>5. العمر:</h3>
        <select id="q5">
            <option value="2">فوق 70 سنة</option>
            <option value="1">65-70 سنة</option>
            <option value="0.5">أقل من 65 سنة</option>
        </select>
    </div>

    <div class="question-box">
        <h3>6. مستوى النشاط البدني:</h3>
        <select id="q6">
            <option value="2">عمل بدني شاق يوميًا</option>
            <option value="1">تمارين متوسطة 3-4 مرات أسبوعيًا</option>
            <option value="0.5">نشاط خفيف</option>
        </select>
    </div>

    <div class="question-box">
        <h3>7. تجارب سابقة مع الصيام:</h3>
        <select id="q7">
            <option value="2">تعرضت لمضاعفات خطيرة</option>
            <option value="1">بعض الصعوبات البسيطة</option>
            <option value="0">لا مشاكل سابقة</option>
        </select>
    </div>

    <div class="question-box">
        <h3>8. وظائف الكلى (eGFR): <span style='color: #F15E5D;'>اسأل الطبيب</span></h3>
        <select id="q8">
            <option value="2">أقل من 30</option>
            <option value="1.5">30-45</option>
            <option value="1">45-60</option>
            <option value="0">أعلى من 60</option>
        </select>
    </div>

    <div style="text-align: center;">
        <button onclick="calculateRisk()">احسب مستوى الخطورة</button>
    </div>

    <div id="result" class="result-box"></div>

    <div class="question-box">
        <h3>تصنيف خطورة الصيام وفقًا لمجموع النقاط:</h3>
        <ul>
            <li><strong>إذا كان مجموع النقاط أكثر من 6:</strong> خطورة عالية، يجب تجنب الصيام.</li>
            <li><strong>إذا كان مجموع النقاط بين 3.5 و 6:</strong> خطورة متوسطة، يجب تقييم الحالة بشكل فردي.</li>
            <li><strong>إذا كان المجموع أقل من 3.5:</strong> يمكن للمريض الصيام بشكل آمن مع الالتزام بالإرشادات الطبية.</li>
        </ul>
    </div>

    <script>
        function calculateRisk() {
            let total = 0;
            for(let i=1; i<=8; i++) {
                total += parseFloat(document.getElementById(`q${i}`).value);
            }

            const resultDiv = document.getElementById('result');
            if (total >= 8) {
                resultDiv.className = 'result-box high-risk';
                resultDiv.innerHTML = `🚨 <strong>ممنوع الصيام:</strong> يُنصح بمراجعة الطبيب فورًا لتقييم الحالة وتعديل العلاج. قد يؤدي الصيام إلى مخاطر مثل هبوط السكر الحاد، الجفاف، واضطراب وظائف الكلى. خطورة عالية جدًا، راجع الطبيب.`;
            } else if (total >= 5) {
                resultDiv.className = 'result-box medium-risk';
                resultDiv.innerHTML = `⚠️ <strong>تقييم طبي مطلوب:</strong> يحتاج إلى متابعة دقيقة وقياس مستوى السكر بشكل متكرر أثناء الصيام. قد يكون هناك خطر من حدوث مضاعفات مثل انخفاض أو ارتفاع حاد في مستوى السكر. راقب وظائف الكلى.`;
            } else {
                resultDiv.className = 'result-box low-risk';
                resultDiv.innerHTML = `✅ <strong>صيام آمن مع المراقبة:</strong> يوصى بالالتزام بالإرشادات الطبية وقياس السكر بانتظام. تجنب الجفاف، وتأكد من تناول وجبة سحور متوازنة. لا توجد خطورة كبيرة.`;
            }
        }
    </script>
</body>
</html>
