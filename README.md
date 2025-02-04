<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GPA Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        table, th, td {
            border: 1px solid #ddd;
            text-align: center;
        }
        th, td {
            padding: 10px;
               }
    </style>
</head>
<body>
    <h1>GPA Calculator</h1>
    <form id="gpaForm">
        <div id="subjectsContainer">
            <div class="input-row">
                <label for="subject1">Subject 1 Name:</label>
                <input type="text" id="subject1" name="subject1" required>
                <label for="credit1">Credit Hours:</label>
                <input type="number" id="credit1" name="credit1" min="1" max="4" required>
                <label for="score1">Score:</label>
                <input type="number" id="score1" name="score1" min="0" max="100" required>
            </div>
        </div>
        <button type="button" onclick="addSubject()">Add Another Subject</button>
        <button type="submit">Calculate GPA</button>
    </form>

 <h2>Results</h2>
    <table id="resultsTable">
        <thead>
            <tr>
                <th>Subject</th>
                <th>Credit Hours</th>
                <th>Score</th>
                <th>Grade</th>
                <th>Point</th>
            </tr>
        </thead>
        <tbody>
        </tbody>
    </table>
    <h3 id="gpaResult"></h3>

    <script>
        let subjectCount = 1;

        function addSubject() {
            subjectCount++;
 const container = document.getElementById('subjectsContainer');
            const div = document.createElement('div');
            div.className = 'input-row';
            div.innerHTML = `
                <label for="subject${subjectCount}">Subject ${subjectCount} Name:</label>
                <input type="text" id="subject${subjectCount}" name="subject${subjectCount}" required>
                <label for="credit${subjectCount}">Credit Hours:</label>
                <input type="number" id="credit${subjectCount}" name="credit${subjectCount}" min="1" max="4" required>
                <label for="score${subjectCount}">Score:</label>
                <input type="number" id="score${subjectCount}" name="score${subjectCount}" min="0" max="100" required>
            `;
            container.appendChild(div);
        }
 function calculateGrade(score) {
            if (score >= 80) return { grade: "A", point: 4.0 };
            if (score >= 75) return { grade: "A-", point: 3.7 };
            if (score >= 70) return { grade: "B+", point: 3.3 };
            if (score >= 65) return { grade: "B", point: 3.0 };
            if (score >= 60) return { grade: "B-", point: 2.7 };
            if (score >= 55) return { grade: "C+", point: 2.3 };
            if (score >= 50) return { grade: "C", point: 2.0 };
            if (score >= 45) return { grade: "C-", point: 1.7 };
            if (score >= 40) return { grade: "D", point: 1.0 };
            return { grade: "F", point: 0.0 };
        }

        document.getElementById('gpaForm').addEventListener('submit', function (e) {
            e.preventDefault();

            const resultsTable = document.getElementById('resultsTable').querySelector('tbody');
            resultsTable.innerHTML = '';

            let totalQualityPoints = 0;
            let totalCredits = 0;
  for (let i = 1; i <= subjectCount; i++) {
                const subject = document.getElementById(subject${i}).value;
                const credit = parseInt(document.getElementById(credit${i}).value);
                const score = parseFloat(document.getElementById(score${i}).value);

                if (!subject || isNaN(credit) || isNaN(score)) {
                    alert(Please fill out all fields for Subject ${i});
                    return;
                }

                const { grade, point } = calculateGrade(score);

                totalQualityPoints += point * credit;
                totalCredits += credit;

                const row = `<tr>
                    <td>${subject}</td>
                    <td>${credit}</td>
                    <td>${score}</td>
                    <td>${grade}</td>
                    <td>${point.toFixed(2)}</td>
                </tr>`;
                resultsTable.innerHTML += row;
            }
 const gpa = totalQualityPoints / totalCredits;
            document.getElementById('gpaResult').innerText = Your GPA is: ${gpa.toFixed(2)};
        });
    </script>
</body>
</html>

