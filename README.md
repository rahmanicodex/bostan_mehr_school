
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <title>سامانه مدیریت مکتب افغان</title>
  <link href="https://fonts.googleapis.com/css2?family=Vazirmatn&display=swap" rel="stylesheet" />
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css"
  />
  <style>
    * {
      font-family: 'Vazirmatn', sans-serif;
    }
    body {
      background: url('https://images.unsplash.com/photo-1577896851231-70ef18881754?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80')
        no-repeat center center fixed;
      background-size: cover;
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }
    .container,
    .admin-panel,
    .teacher-panel,
    .parent-panel {
      background-color: rgba(255, 255, 255, 0.95);
      border-radius: 15px;
      padding: 30px;
      width: 90%;
      max-width: 600px;
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
      text-align: center;
    }
    h1,
    h2,
    h3 {
      color: #1d3557;
    }
    input,
    select,
    textarea {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      border-radius: 10px;
      border: 1px solid #ccc;
      box-sizing: border-box;
    }
    button {
      width: 100%;
      padding: 10px;
      background-color: #1d3557;
      color: white;
      border: none;
      border-radius: 10px;
      margin-top: 10px;
      font-size: 16px;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #0d1c34;
    }
    .hidden {
      display: none;
    }
    .record {
      background: #f8f9fa;
      border: 1px solid #ccc;
      border-radius: 8px;
      padding: 10px;
      margin-top: 10px;
      text-align: right;
    }
    .record input,
    .record select,
    .record textarea {
      width: auto;
      margin-top: 5px;
      margin-bottom: 5px;
      padding: 6px;
      border-radius: 6px;
      border: 1px solid #ccc;
      box-sizing: border-box;
    }
    .record-buttons {
      display: flex;
      justify-content: flex-end;
      gap: 10px;
    }
    .school-info {
      margin-top: 20px;
      text-align: right;
      font-size: 14px;
      line-height: 1.8;
      color: #333;
    }
    .school-info i {
      margin-left: 8px;
      color: #1d3557;
    }
    /* لینک های تلگرام و فیسبوک بدون خط و رنگ تیره */
    .school-info a {
      text-decoration: none;
      color: #2c3e50;
      font-weight: 600;
    }
    .school-info a:hover {
      color: #2980b9;
      text-decoration: underline;
    }
    .user-list {
      text-align: right;
      margin-top: 20px;
    }
    .user-item {
      background: #f1f1f1;
      padding: 10px;
      border-radius: 8px;
      margin-top: 10px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .user-item input {
      margin: 0 5px;
      flex: 1;
      border-radius: 6px;
      border: 1px solid #ccc;
      padding: 6px;
    }
    .user-item button {
      flex: 0 0 auto;
      width: auto;
      padding: 6px 12px;
      font-size: 14px;
      border-radius: 6px;
    }
  </style>
</head>
<body>
  <div class="container" id="login-panel">
    <h1>سامانه مدیریت مکتب خصوصی بامیکا</h1>
    <div class="school-info">
      <p><i class="fas fa-map-marker-alt"></i> آدرس: کابل، دشت برچی، ریگریشن</p>
      <p><i class="fas fa-phone"></i> شماره تماس: ۰۷۰۰۱۲۳۴۵۶</p>
      <p><i class="fab fa-whatsapp"></i> واتساپ: ۰۷۰۰۱۲۳۴۵۶</p>
      <p>
        <i class="fab fa-telegram"></i>
        کانال تلگرام:
        <a href="https://t.me/maktabbamika" target="_blank">مکتب خصوصی بامیکا</a>
      </p>
      <p>
        <i class="fab fa-facebook"></i>
        صفحه فیسبوک:
        <a href="https://facebook.com/maktabbamika" target="_blank">مکتب خصوصی بامیکا</a>
      </p>
    </div>
    <select id="userTypeSelect">
      <option value="admin">مدیر</option>
      <option value="teacher">معلم</option>
      <option value="parent">والدین</option>
    </select>
    <input type="text" id="username" placeholder="نام کاربری" />
    <input type="password" id="password" placeholder="رمز عبور" />
    <button onclick="handleLogin()">ورود</button>
  </div>

  <div class="admin-panel hidden" id="admin-panel">
    <h2>پنل مدیریت</h2>
    <h3>افزودن معلم</h3>
    <input type="text" id="teacherUser" placeholder="نام کاربری معلم" />
    <input type="password" id="teacherPass" placeholder="رمز عبور معلم" />
    <button onclick="registerSpecificUser('teacher')">ثبت معلم</button>
    <div id="teacherList" class="user-list"></div>

    <h3>افزودن والد</h3>
    <input type="text" id="parentUser" placeholder="نام کاربری والد" />
    <input type="password" id="parentPass" placeholder="رمز عبور والد" />
    <button onclick="registerSpecificUser('parent')">ثبت والد</button>
    <div id="parentList" class="user-list"></div>

    <button onclick="logout()">خروج</button>
  </div>

  <div class="teacher-panel hidden" id="teacher-panel">
    <h2>پنل معلم</h2>
    <input type="text" id="studentName" placeholder="نام شاگرد" />
    <input type="text" id="studentFather" placeholder="نام پدر شاگرد" />
    <select id="grade">
      <option disabled selected>انتخاب صنف</option>
      <script>
        for (let i = 1; i <= 10; i++) {
          document.write(
            `<option value="${i}الف">صنف ${i} الف</option><option value="${i}ب">صنف ${i} ب</option>`
          );
        }
      </script>
    </select>
    <input type="text" id="subject" placeholder="مضمون" />
    <select id="performance">
      <option value="عالی">عالی</option>
      <option value="متوسط">متوسط</option>
      <option value="ضعیف">ضعیف</option>
    </select>
    <textarea id="extraNote" placeholder="توضیحات اضافی"></textarea>
    <input type="date" id="recordDate" />
    <button onclick="submitStudentData()">ثبت آمار</button>
    <div id="teacherRecords"></div>
    <button onclick="logout()">خروج</button>
  </div>

  <div class="parent-panel hidden" id="parent-panel">
    <h2>پنل والدین</h2>
    <div id="studentInfo"></div>
    <button onclick="logout()">خروج</button>
  </div>

  <script>
    let users = JSON.parse(localStorage.getItem('users')) || {
      admin: { مدیر: '1234' },
      teacher: {},
      parent: {},
    };
    let studentRecords = JSON.parse(localStorage.getItem('records')) || [];
    let currentUser = null;
    let currentRole = null;

    function saveData() {
      localStorage.setItem('users', JSON.stringify(users));
      localStorage.setItem('records', JSON.stringify(studentRecords));
    }

    function handleLogin() {
      const username = document.getElementById('username').value.trim();
      const password = document.getElementById('password').value.trim();
      const userType = document.getElementById('userTypeSelect').value;
      if (users[userType][username] === password) {
        currentUser = username;
        currentRole = userType;
        document.getElementById('login-panel').classList.add('hidden');
        document.getElementById(`${userType}-panel`).classList.remove('hidden');
        if (userType === 'parent') showStudentInfo();
        if (userType === 'teacher') showTeacherRecords();
        if (userType === 'admin') showUserLists();
      } else {
        alert('اطلاعات ورود نادرست است.');
      }
    }

    function registerSpecificUser(role) {
      const username = document.getElementById(`${role}User`).value.trim();
      const password = document.getElementById(`${role}Pass`).value.trim();
      if (!username || !password) return alert('تمام فیلدها الزامی است.');
      users[role][username] = password;
      saveData();
      document.getElementById(`${role}User`).value = '';
      document.getElementById(`${role}Pass`).value = '';
      alert('کاربر با موفقیت ثبت شد.');
      showUserLists();
    }

    function showUserLists() {
      ['teacher', 'parent'].forEach((role) => {
        const div = document.getElementById(role + 'List');
        div.innerHTML = Object.entries(users[role])
          .map(
            ([user, pass]) => `
          <div class="user-item">
            <input value="${user}" data-role="${role}" data-field="user" />
            <input value="${pass}" data-role="${role}" data-user="${user}" data-field="pass" />
            <button onclick="updateUser(this)">ویرایش</button>
          </div>
        `
          )
          .join('');
      });
    }

    function updateUser(btn) {
      const container = btn.parentElement;
      const usernameInput = container.querySelector('input[data-field="user"]');
      const passwordInput = container.querySelector('input[data-field="pass"]');
      const role = usernameInput.dataset.role;
      const oldUsername = passwordInput.dataset.user;
      const newUsername = usernameInput.value.trim();
      const newPassword = passwordInput.value.trim();

      if (!newUsername || !newPassword) {
        alert('فیلدها نمی‌توانند خالی باشند.');
        return;
      }

      if (newUsername !== oldUsername) {
        delete users[role][oldUsername];
      }

      users[role][newUsername] = newPassword;
      saveData();
      showUserLists();
      alert('کاربر ویرایش شد.');
    }

    function submitStudentData() {
      const record = {
        name: document.getElementById('studentName').value.trim(),
        father: document.getElementById('studentFather').value.trim(),
        grade: document.getElementById('grade').value,
        subject: document.getElementById('subject').value.trim(),
        performance: document.getElementById('performance').value,
        note: document.getElementById('extraNote').value.trim(),
        date: document.getElementById('recordDate').value,
        parent: document.getElementById('studentFather').value.trim(),
      };

      if (!record.name || !record.father || !record.grade || !record.subject) {
        alert('تمام فیلدهای الزامی را پر کنید.');
        return;
      }

      // بررسی تطابق نام پدر با نام والدین ثبت شده
      if (!users.parent[record.father]) {
        alert('نام پدر شاگرد با نام کاربری والدین ثبت شده مطابقت ندارد.');
        return;
      }

      studentRecords.push(record);
      saveData();
      showTeacherRecords();
      clearTeacherInputs();
    }

    function clearTeacherInputs() {
      document.getElementById('studentName').value = '';
      document.getElementById('studentFather').value = '';
      document.getElementById('grade').selectedIndex = 0;
      document.getElementById('subject').value = '';
      document.getElementById('performance').selectedIndex = 0;
      document.getElementById('extraNote').value = '';
      document.getElementById('recordDate').value = '';
    }

    function showTeacherRecords() {
      const div = document.getElementById('teacherRecords');
      if (studentRecords.length === 0) {
        div.innerHTML = '<p>هیچ آمار ثبت شده‌ای وجود ندارد.</p>';
        return;
      }

      div.innerHTML = '<h3>آمار ثبت شده شاگردان:</h3>';

      studentRecords.forEach((rec, index) => {
        div.innerHTML += `
          <div class="record" data-index="${index}">
            <label>نام شاگرد:<input type="text" value="${rec.name}" class="edit-name" /></label><br/>
            <label>نام پدر:<input type="text" value="${rec.father}" class="edit-father" /></label><br/>
            <label>صنف:
              <select class="edit-grade">
                ${generateGradeOptions(rec.grade)}
              </select>
            </label><br/>
            <label>مضمون:<input type="text" value="${rec.subject}" class="edit-subject" /></label><br/>
            <label>وضعیت:
              <select class="edit-performance">
                <option value="عالی" ${rec.performance === 'عالی' ? 'selected' : ''}>عالی</option>
                <option value="متوسط" ${rec.performance === 'متوسط' ? 'selected' : ''}>متوسط</option>
                <option value="ضعیف" ${rec.performance === 'ضعیف' ? 'selected' : ''}>ضعیف</option>
              </select>
            </label><br/>
            <label>توضیحات اضافی:<textarea class="edit-note">${rec.note}</textarea></label><br/>
            <label>تاریخ:<input type="date" value="${rec.date}" class="edit-date" /></label>
            <div class="record-buttons">
              <button onclick="saveRecord(${index})">ذخیره</button>
              <button onclick="deleteRecord(${index})" style="background-color:#e74c3c;">حذف</button>
            </div>
          </div>
        `;
      });
    }

    function generateGradeOptions(selected) {
      let options = '';
      for (let i = 1; i <= 10; i++) {
        ['الف', 'ب'].forEach((suffix) => {
          const val = `${i}${suffix}`;
          options += `<option value="${val}" ${val === selected ? 'selected' : ''}>صنف ${val}</option>`;
        });
      }
      return options;
    }

    function saveRecord(index) {
      const recordDiv = document.querySelector(`.record[data-index="${index}"]`);
      const name = recordDiv.querySelector('.edit-name').value.trim();
      const father = recordDiv.querySelector('.edit-father').value.trim();
      const grade = recordDiv.querySelector('.edit-grade').value;
      const subject = recordDiv.querySelector('.edit-subject').value.trim();
      const performance = recordDiv.querySelector('.edit-performance').value;
      const note = recordDiv.querySelector('.edit-note').value.trim();
      const date = recordDiv.querySelector('.edit-date').value;

      if (!name || !father || !grade || !subject) {
        alert('لطفاً تمام فیلدهای الزامی را پر کنید.');
        return;
      }
      // بررسی تطابق نام پدر با والدین ثبت شده
      if (!users.parent[father]) {
        alert('نام پدر شاگرد با نام کاربری والدین ثبت شده مطابقت ندارد.');
        return;
      }

      studentRecords[index] = {
        name,
        father,
        grade,
        subject,
        performance,
        note,
        date,
        parent: father,
      };

      saveData();
      alert('رکورد با موفقیت ذخیره شد.');
      showTeacherRecords();
    }

    function deleteRecord(index) {
      if (confirm('آیا از حذف این رکورد اطمینان دارید؟')) {
        studentRecords.splice(index, 1);
        saveData();
        showTeacherRecords();
      }
    }

    function showStudentInfo() {
      const div = document.getElementById('studentInfo');
      const records = studentRecords.filter(r => r.parent === currentUser);
      if (records.length === 0) {
        div.innerHTML = '<p>هیچ آمار شاگرد ثبت نشده است.</p>';
        return;
      }
      div.innerHTML = '<h3>آمار شاگرد شما:</h3>';
      records.forEach(rec => {
        div.innerHTML += `
          <div class="record">
            <p><strong>نام شاگرد:</strong> ${rec.name}</p>
            <p><strong>صنف:</strong> ${rec.grade}</p>
            <p><strong>مضمون:</strong> ${rec.subject}</p>
            <p><strong>وضعیت:</strong> ${rec.performance}</p>
            <p><strong>توضیحات اضافی:</strong> ${rec.note}</p>
            <p><strong>تاریخ:</strong> ${rec.date}</p>
          </div>
        `;
      });
    }

    function logout() {
      currentUser = null;
      currentRole = null;
      document.getElementById('login-panel').classList.remove('hidden');
      ['admin', 'teacher', 'parent'].forEach(role => {
        document.getElementById(`${role}-panel`).classList.add('hidden');
      });
      clearInputs();
    }

    function clearInputs() {
      ['username', 'password', 'teacherUser', 'teacherPass', 'parentUser', 'parentPass',
        'studentName', 'studentFather', 'grade', 'subject', 'extraNote', 'recordDate'].forEach(id => {
        const el = document.getElementById(id);
        if (el) {
          if (el.tagName === 'SELECT') {
            el.selectedIndex = 0;
          } else {
            el.value = '';
          }
        }
      });
    }
  </script>
</body>
</html>
