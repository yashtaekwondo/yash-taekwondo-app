<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Yash Taekwondo Academy - Management System</title>
    <style>
        * { box-sizing: border-box; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; margin: 0; padding: 0; }
        body { background-color: #f4f6f9; padding: 20px; color: #333; }
        .container { max-width: 1100px; margin: auto; }
        header { background: #d9534f; color: white; padding: 20px; text-align: center; border-radius: 8px; margin-bottom: 20px; }
        header h1 { margin-bottom: 5px; }
        
        .dashboard { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px; margin-bottom: 20px; }
        .card { background: white; padding: 20px; border-radius: 8px; text-align: center; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
        .card h3 { font-size: 14px; color: #666; margin-bottom: 5px; }
        .card p { font-size: 24px; font-weight: bold; color: #d9534f; }

        .section { background: white; padding: 20px; border-radius: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); margin-bottom: 20px; }
        .section h2 { border-bottom: 2px solid #f4f6f9; padding-bottom: 10px; margin-bottom: 15px; color: #444; }

        form { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 10px; margin-bottom: 15px; }
        input, select, button { padding: 10px; border: 1px solid #ccc; border-radius: 5px; font-size: 14px; }
        button { background: #d9534f; color: white; border: none; cursor: pointer; font-weight: bold; }
        button:hover { background: #c9302c; }

        table { width: 100%; border-collapse: collapse; margin-top: 10px; }
        th, td { padding: 12px; border: 1px solid #ddd; text-align: left; font-size: 14px; }
        th { background-color: #f8f9fa; }

        .badge { padding: 4px 8px; border-radius: 4px; font-size: 12px; color: white; display: inline-block; }
        .badge-present { background-color: #5cb85c; }
        .badge-absent { background-color: #d9534f; }
        .badge-paid { background-color: #0275d8; }
        .badge-pending { background-color: #f0ad4e; }
        
        .btn-sm { padding: 5px 10px; font-size: 12px; margin-right: 2px; }
        .btn-green { background-color: #5cb85c; }
        .btn-orange { background-color: #f0ad4e; }
        .btn-blue { background-color: #0275d8; }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>🥋 Yash Taekwondo Academy</h1>
        <p>Fee & Attendance Management System</p>
    </header>

    <!-- Dashboard Summary -->
    <div class="dashboard">
        <div class="card">
            <h3>Total Students</h3>
            <p id="totalStudents">0</p>
        </div>
        <div class="card">
            <h3>Today Present</h3>
            <p id="totalPresent">0</p>
        </div>
        <div class="card">
            <h3>Fee Pending</h3>
            <p id="totalPending">0</p>
        </div>
        <div class="card">
            <h3>Fee Paid</h3>
            <p id="totalPaid">0</p>
        </div>
    </div>

    <!-- Add New Student -->
    <div class="section">
        <h2>1. Naya Student Add Karein</h2>
        <form id="studentForm">
            <input type="text" id="name" placeholder="Student Ka Naam" required>
            <input type="tel" id="mobile" placeholder="Mobile Number" required>
            <select id="belt" required>
                <option value="">Belt Rank Chunein</option>
                <option value="White">White Belt</option>
                <option value="Yellow">Yellow Belt</option>
                <option value="Green">Green Belt</option>
                <option value="Blue">Blue Belt</option>
                <option value="Red">Red Belt</option>
                <option value="Black">Black Belt</option>
            </select>
            <select id="batch" required>
                <option value="">Batch Timing</option>
                <option value="Morning">Morning Batch</option>
                <option value="Evening">Evening Batch</option>
            </select>
            <button type="submit">Student Add Karein</button>
        </form>
    </div>

    <!-- Attendance & Fee List -->
    <div class="section">
        <h2>2. Student Record, Attendance & Fee</h2>
        <div style="overflow-x:auto;">
            <table>
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Mobile</th>
                        <th>Belt</th>
                        <th>Batch</th>
                        <th>Today's Attendance</th>
                        <th>Fee Status</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody id="studentTableBody">
                    <!-- Dynamic Data Here -->
                </tbody>
            </table>
        </div>
    </div>
</div>

<script>
    let students = JSON.parse(localStorage.getItem('yash_taekwondo_students')) || [];

    function saveData() {
        localStorage.setItem('yash_taekwondo_students', JSON.stringify(students));
        renderTable();
    }

    document.getElementById('studentForm').addEventListener('submit', function(e) {
        e.preventDefault();
        const newStudent = {
            id: Date.now(),
            name: document.getElementById('name').value,
            mobile: document.getElementById('mobile').value,
            belt: document.getElementById('belt').value,
            batch: document.getElementById('batch').value,
            attendance: 'Not Marked',
            feeStatus: 'Pending'
        };
        students.push(newStudent);
        saveData();
        this.reset();
    });

    function toggleAttendance(id, status) {
        const student = students.find(s => s.id === id);
        if(student) {
            student.attendance = status;
            saveData();
        }
    }

    function toggleFee(id, status) {
        const student = students.find(s => s.id === id);
        if(student) {
            student.feeStatus = status;
            saveData();
        }
    }

    function deleteStudent(id) {
        if(confirm("Kya aap is student ko delete karna chahte hain?")) {
            students = students.filter(s => s.id !== id);
            saveData();
        }
    }

    function renderTable() {
        const tbody = document.getElementById('studentTableBody');
        tbody.innerHTML = '';

        let presentCount = 0;
        let pendingCount = 0;
        let paidCount = 0;

        students.forEach(student => {
            if(student.attendance === 'Present') presentCount++;
            if(student.feeStatus === 'Pending') pendingCount++;
            if(student.feeStatus === 'Paid') paidCount++;

            const tr = document.createElement('tr');
            tr.innerHTML = `
                <td><strong>${student.name}</strong></td>
                <td>${student.mobile}</td>
                <td>${student.belt}</td>
                <td>${student.batch}</td>
                <td>
                    <span class="badge ${student.attendance === 'Present' ? 'badge-present' : 'badge-absent'}">
                        ${student.attendance}
                    </span>
                </td>
                <td>
                    <span class="badge ${student.feeStatus === 'Paid' ? 'badge-paid' : 'badge-pending'}">
                        ${student.feeStatus}
                    </span>
                </td>
                <td>
                    <button class="btn-sm btn-green" onclick="toggleAttendance(${student.id}, 'Present')">Present</button>
                    <button class="btn-sm btn-orange" onclick="toggleAttendance(${student.id}, 'Absent')">Absent</button>
                    <button class="btn-sm btn-blue" onclick="toggleFee(${student.id}, '${student.feeStatus === 'Paid' ? 'Pending' : 'Paid'}')">
                        Fee: ${student.feeStatus === 'Paid' ? 'Mark Pending' : 'Mark Paid'}
                    </button>
                    <button class="btn-sm" style="background:#333;" onclick="deleteStudent(${student.id})">Delete</button>
                </td>
            `;
            tbody.appendChild(tr);
        });

        // Update Dashboard Stats
        document.getElementById('totalStudents').innerText = students.length;
        document.getElementById('totalPresent').innerText = presentCount;
        document.getElementById('totalPending').innerText = pendingCount;
        document.getElementById('totalPaid').innerText = paidCount;
    }

    // Initial Load
    renderTable();
</script>

</body>
</html>
