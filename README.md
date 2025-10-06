## 📋 Prerequisites

Bago nyo mapa run ung system gawin nyo muna to:

Need i-download:

1. Node.js (v16 higher)
   - Download 

2. **XAMPP** (for MySQL and phpMyAdmin)
   - Download
   - Make sure na MySQL is included sa installation

3. VS Code
   - Download 

---

Installation Steps

Step 1: Download Project

1. Download project folder to your computer
2. Extract to a location like: `C:\canteen-pos` NOTE: GAWA KAYO FOLDER ETO PANGALAN WAG NYO PAPTUNGAN PA NG ISA PANG FOLDER LIKE C:\COSC 75\canteen-pos

Step 2: Open Project in VS Code

1. Open VS Code
2. open ung folder sa vscode-------

### Step 3: Install Node Modules

1. In VS Code, open Terminal (press Ctrl + ~)
2. Run the following command:
   
   npm install

4. Wait download

   
#Step 4: Start XAMPP MySQL

1. Open XAMPP Control Panel
2. Click Start next to Apache
3. Click Start next to MySQL
4. Both should show green highlighting when running

 Troubleshooting: (PAG AYAW LANG MAG START):
- Check port 3306 is already in use (CHAT GPT NYO NALANG HOW)
- Stop any Windows MySQL service in `services.msc`
- See the "Common Issues" section below

Step 5: Create Database

1. Open  web browser
2. Go: `http://localhost/phpmyadmin`
3. Click the SQL tab at the top
4. Open the file: `database/schema.sql` from the project folder
5. Copy ALL the content from that file
6. Paste it into the SQL box in phpMyAdmin
7. Click the Go button
8. You should see success messages

**Verify:**
- Check the left sidebar - you should see `canteen_pos` database
- Click on it - you should see 5 tables: users, products, sales, sale_items, inventory_logs

Step 6: Configure Database Connection (IF NEEDED)

1. Open `server.js` in VS Code
2. Find lines 43-48 (the database configuration)
3. Update if your MySQL has a password:
   ```javascript
   const pool = mysql.createPool({
       host: 'localhost',
       port: 3306,              // Change if using different port
       user: 'root',            // Change if using different user
       password: '',            // Add your MySQL password here if you have one
       database: 'canteen_pos',
       waitForConnections: true,
       connectionLimit: 10,
       queueLimit: 0
   });
   ```

### Step 7: Start the Server

1. In VS Code Terminal, run:
   ```bash
   npm start
   ```
   
   **OR**
   
   ```bash
   node server.js
   ```

2. ETO DAPAT LALABAS (pag nakalagay di naka connect sa database troubleshoot nalang , nasa baba instructions):
   ```
   ✅ Database connected successfully
   🚀 Canteen POS Server Started Successfully!
   📍 Local Access:     http://localhost:3000
   📡 Network Access:   http://[YOUR_IP]:3000
   ```

3. WAG I EEXIT UNG TERMINAL (pag walang cursor or di nakaka type sa terminal naka run na yun)

Step 8: Access System

1. Open web browser
2. Go: `http://localhost:3000`
3. You should see the login page

 Step 9: Login



Accessing from Other Devices (WiFi)

To use the system on tablets, phones, or other computers on the same WiFi:

### Step 1: Find Your Computer's IP Address

on Windows:

1. Open Command Prompt
2. Type: `ipconfig`
3. Look for **IPv4 Address** under your WiFi adapter
4. Example: `192.168.1.100`


### Step 2: Connect from Other Devices

1. Make sure the device is on the **same WiFi network**
2. Open a web browser on that device
3. Go to: `http://YOUR_IP:3000`
   - Example: `http://192.168.1.100:3000`
4. You should see the login page

Note: dapat naka run sa computer ung system ung npm start

---

## 📁 Project Structure

```
canteen-pos/
├── database/
│   └── schema.sql          # Database structure and sample data
├── public/
│   ├── login.html         # Login page
│   ├── dashboard.html     # Dashboard with stats and alerts
│   ├── sales.html         # POS interface for making sales
│   ├── inventory.html     # Inventory management
│   └── reports.html       # Sales reports and transactions
├── node_modules/          # Dependencies (auto-generated)
├── server.js              # Backend server (Node.js/Express)
├── package.json           # Project configuration
└── README.md              # This file
```

---

 Common Issues & Solutions

Issue 1: "MySQL shutdown unexpectedly" in XAMPP

**Solution:**
1. Open Task Manager (Ctrl + Shift + Esc)
2. Go Details tab
3. Find and end any `mysqld.exe` processes
4. Stop Windows MySQL service:
   - Press Win + R
   - Type `services.msc`
   - Find "MySQL" or "MySQL80"
   - Right-click → Stop
   - Right-click → Properties → Startup type: Disabled
5. Restart MySQL in XAMPP

### Issue 2: "Cannot find module 'express'"

**Solution:**
```bash
npm install
```

### Issue 3: "Database connection failed"

**Solutions:**
1. Make sure MySQL is running in XAMPP (green status)
2. Verify database `canteen_pos` exists in phpMyAdmin
3. Check if MySQL password is correct in `server.js`
4. Try restarting MySQL in XAMPP

### Issue 4: "Port 3000 already in use"

**Solution:**
1. In `server.js`, change line 8:
   ```javascript
   const PORT = 3001; // Changed from 3000
   ```
2. Access using `http://localhost:3001`

### Issue 5: "Site cannot be reached"

**Solutions:**
1. Make sure the server is running (`npm start`)
2. Check if the terminal shows "Server Started Successfully"
3. Verify `public` folder exists with all HTML files
4. Try `http://127.0.0.1:3000` instead

---

## 🛑 Stopping the Server

To stop the server:
1. Go to VS Code Terminal where server is running
2. Press `Ctrl + C`
3. Type `Y` if asked to confirm

---

## 📝 User Roles & Permissions

### Owner
- Full access to all features
- Can manage users
- Can change product prices
- View all reports and dashboards

### Manager
- View dashboards and reports
- Manage inventory
- Monitor expiration dates
- Cannot manage users

### Cashier
- Enter sales and print receipts
- View product list
- Limited inventory view
- No access to reports or price changes

---



**Group 5 - 2025**
