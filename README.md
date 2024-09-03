<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Commission Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-image: url('https://1539841570.rsc.cdn77.org/storage/app/media/Hotel%20Photos/Pools/IMG_20200820_145341_1920x1280.jpg.webp');
            background-size: cover;
            background-position: center;
            color: #fff;
        }
        .container {
            max-width: 400px;
            margin: auto;
            padding: 20px;
            background-color: rgba(0, 0, 0, 0.7); /* Semi-transparent background */
            border-radius: 10px;
        }
        input, select {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border-radius: 5px;
            border: 1px solid #ccc;
            background-color: #fff; /* White background for inputs */
            color: #000; /* Black text color for inputs */
        }
        button {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            width: 100%;
            margin-bottom: 10px;
        }
        button:hover {
            background-color: #45a049;
        }
        .delete-button {
            background-color: #f44336;
        }
        .delete-button:hover {
            background-color: #e53935;
        }
        .result {
            margin-top: 20px;
        }
        .result p {
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Commission Calculator</h2>
        <label for="month">Commission for the Month (€):</label>
        <input type="number" id="month" placeholder="Enter Commission for the Month">

        <label for="extraPax">Include Extra Person for Day Shift:</label>
        <select id="extraPax">
            <option value="0">No</option>
            <option value="1">Yes</option>
        </select>

        <button onclick="calculateCommission()">Calculate</button>
        <button class="delete-button" onclick="clearAll()">Delete All</button>

        <div class="result" id="result"></div>
    </div>

    <script>
        function calculateCommission() {
            const month = parseFloat(document.getElementById('month').value) || 0;
            const extraPax = parseInt(document.getElementById('extraPax').value) || 0;

            // Calculation
            let afterHotel = month / 2;
            let afterVAT = afterHotel - (afterHotel * 0.20);

            // Total After Deductions
            let total = afterVAT;

            // Default Numbers
            let nightShiftCount = 4;
            let dayShiftCount = 5 + extraPax;  // Add extra person to day shift if selected

            // Distribution
            let nightShiftTotal = total * 0.33;
            let dayShiftTotal = total * 0.67;

            let nightShiftPerPerson = nightShiftTotal / nightShiftCount;
            let dayShiftPerPerson = dayShiftTotal / dayShiftCount;

            let resultHTML = `
                <p>Total Amount After Deductions: €${total.toFixed(2)}</p>
                <p>Night Shift (33%):</p>
                <ul>
                    <li>Marko: €${nightShiftPerPerson.toFixed(2)}</li>
                    <li>Wassem: €${nightShiftPerPerson.toFixed(2)}</li>
                    <li>Ivan: €${nightShiftPerPerson.toFixed(2)}</li>
                    <li>Stevan: €${nightShiftPerPerson.toFixed(2)}</li>
                </ul>
                <p>Day Shift (67%):</p>
                <ul>
                    <li>Jana: €${dayShiftPerPerson.toFixed(2)}</li>
                    <li>Elizabeth: €${dayShiftPerPerson.toFixed(2)}</li>
                    <li>Julie: €${dayShiftPerPerson.toFixed(2)}</li>
                    <li>Mario: €${dayShiftPerPerson.toFixed(2)}</li>
                    <li>Joanne: €${dayShiftPerPerson.toFixed(2)}</li>
            `;

            if (extraPax === 1) {
                resultHTML += `<li>Extra Person (Day Shift): €${dayShiftPerPerson.toFixed(2)}</li>`;
            }

            resultHTML += `</ul>`;

            document.getElementById('result').innerHTML = resultHTML;
        }

        function clearAll() {
            document.getElementById('month').value = '';
            document.getElementById('extraPax').selectedIndex = 0;
            document.getElementById('result').innerHTML = '';
        }
    </script>
</body>
</html>
