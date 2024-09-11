<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>منظومة العضوية الكنسية</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        .container {
            width: 80%;
            margin: 0 auto;
            padding: 2em;
        }
        h1 {
            text-align: center;
        }
        form {
            background: #fff;
            padding: 2em;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        input, select, textarea {
            width: calc(100% - 22px);
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        button {
            padding: 10px 15px;
            background-color: #333;
            color: #fff;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #555;
        }
        .login-form {
            max-width: 400px;
            margin: 2em auto;
            background: #fff;
            padding: 2em;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="login-form">
            <h2>تسجيل الدخول</h2>
            <form id="loginForm">
                <input type="text" id="username" placeholder="اسم المستخدم" required>
                <input type="password" id="password" placeholder="كلمة المرور" required>
                <button type="submit">تسجيل الدخول</button>
            </form>
        </div>
        <div id="membershipForm" style="display:none;">
            <h1>إضافة بيانات العضو</h1>
            <form id="memberForm">
                <input type="text" id="name" placeholder="الاسم" required>
                <input type="number" id="age" placeholder="السن" required>
                <input type="text" id="building" placeholder="العمارة" required>
                <input type="text" id="area" placeholder="المنطقة" required>
                <input type="date" id="birthdate" placeholder="تاريخ الميلاد" required>
                <input type="date" id="marriageDate" placeholder="تاريخ الزواج">
                <input type="text" id="children" placeholder="الأبناء">
                <button type="button" onclick="addMember()">إضافة</button>
                <button type="button" onclick="exportToExcel()">تصدير إلى Excel</button>
            </form>
            <table id="membersTable" style="width:100%; margin-top:20px; border-collapse:collapse;">
                <thead>
                    <tr>
                        <th>الاسم</th>
                        <th>السن</th>
                        <th>العمارة</th>
                        <th>المنطقة</th>
                        <th>تاريخ الميلاد</th>
                        <th>تاريخ الزواج</th>
                        <th>الأبناء</th>
                    </tr>
                </thead>
                <tbody>
                </tbody>
            </table>
        </div>
    </div>

    <script src="https://cdn.sheetjs.com/xlsx-0.18.5/xlsx.full.min.js"></script>
    <script>
        document.getElementById('loginForm').addEventListener('submit', function(event) {
            event.preventDefault();
            // Simple login logic (for demonstration)
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            if (username === 'admin' && password === 'password') {
                document.querySelector('.login-form').style.display = 'none';
                document.getElementById('membershipForm').style.display = 'block';
            } else {
                alert('اسم المستخدم أو كلمة المرور غير صحيحة');
            }
        });

        function addMember() {
            const name = document.getElementById('name').value;
            const age = document.getElementById('age').value;
            const building = document.getElementById('building').value;
            const area = document.getElementById('area').value;
            const birthdate = document.getElementById('birthdate').value;
            const marriageDate = document.getElementById('marriageDate').value;
            const children = document.getElementById('children').value;

            const tableBody = document.querySelector('#membersTable tbody');
            const row = document.createElement('tr');
            row.innerHTML = `
                <td>${name}</td>
                <td>${age}</td>
                <td>${building}</td>
                <td>${area}</td>
                <td>${birthdate}</td>
                <td>${marriageDate}</td>
                <td>${children}</td>
            `;
            tableBody.appendChild(row);
        }

        function exportToExcel() {
            const wb = XLSX.utils.book_new();
            const ws = XLSX.utils.table_to_sheet(document.querySelector('#membersTable'));
            XLSX.utils.book_append_sheet(wb, ws, 'أعضاء');
            XLSX.writeFile(wb, 'members.xlsx');
        }
    </script>
</body>
</html>
# church-membership-system
