# Dragons_Lair

## Only for Unix and Linux based architecture due to commands executed by scripts or alter for windows.
## Works particularly well with wordpress based projects. Hence the comment as it was submitted to wordfence.

Organize Your Project StructureEnsure your project structure looks like this:
project-directory/
│

├── public/

│   ├── index.html

│   └── app.js

│
├── node_modules/

├── package.json

└── server.js

Step 1: Install Dependencies and Run the Server Ensure you have Node.js and npm installed. 
Then, install Express:

```bash
npm init -y
```
```bash
npm install express
```
Finally, start your server:node server.js Navigate to http://localhost:3000 in your web browser to interact with your GUI.
This setup provides a basic web interface for the security monitoring and user management functions. 
You can expand the GUI and backend functionalities as needed.

STEP BY STEP GUIDE GUI

Step 1: Install Node.js and npmDownload and install Node.js from nodejs.org. 
This will also install npm (Node Package Manager).
Verify the installation: 
```bash
node -v
```
```bash
npm -v
```
Step 2: Set Up the Project and Initialize the project:
```bash
mkdir project-directory
```
```bash
cd project-directory
```
```bash
npm init -y
```
Install Express:
```bash
npm install express
```
Create project files and structure:
```bash
mkdir public
```
```bash
touch public/index.html
```
```bash
touch public/app.js
```
```bash
touch server.js
```
Step 3: Add HTML and JavaScript Code
public/
index.html:

```bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Security Monitoring Dashboard</title>
    <style>
        body { font-family: Arial, sans-serif; }
        .container { width: 50%; margin: 0 auto; }
        header, footer { text-align: center; margin: 20px 0; }
        .section { margin: 20px 0; }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>The Dragon's Lair</h1>
            <h2>The reason you should stay behind the fence</h2>
        </header>

        <div class="section">
            <h3>Add User</h3>
            <form id="addUserForm">
                <label for="username">Username:</label>
                <input type="text" id="username" name="username" required>
                <label for="role">Role:</label>
                <input type="text" id="role" name="role" required>
                <button type="submit">Add User</button>
            </form>
        </div>

        <div class="section">
            <h3>Add Super Root Account</h3>
            <form id="addSuperRootForm">
                <label for="superUsername">Username:</label>
                <input type="text" id="superUsername" name="superUsername" required>
                <label for="superPassword">Password:</label>
                <input type="password" id="superPassword" name="superPassword" required>
                <button type="submit">Add Super Root</button>
            </form>
        </div>

        <footer>
            <p>Created by Blu Corbel</p>
        </footer>
    </div>

    <script src="app.js"></script>
</body>
</html>public/app.js:// Encode/Decode functionality
const Base64 = {
    encode: (str) => btoa(str),
    decode: (str) => atob(str),
};

// Function to add user (mocked for demonstration)
const addUser = (username, role) => {
    console.log(`User '${username}' added with role '${role}'`);
};

// Function to add super root account (mocked for demonstration)
const addSuperRootAccount = (username, password) => {
    console.log(`Super root account '${username}' added with password '${Base64.encode(password)}'`);
};

// Event listener for Add User form
document.getElementById('addUserForm').addEventListener('submit', (event) => {
    event.preventDefault();
    const username = event.target.username.value;
    const role = event.target.role.value;
    addUser(username, role);
    alert(`User '${username}' added with role '${role}'`);
});

// Event listener for Add Super Root form
document.getElementById('addSuperRootForm').addEventListener('submit', (event) => {
    event.preventDefault();
    const username = event.target.superUsername.value;
    const password = event.target.superPassword.value;
    addSuperRootAccount(username, password);
    alert(`Super root account '${username}' added`);
});server.js:const express = require('express');
const path = require('path');
const app = express();

app.use(express.static(path.join(__dirname, 'public')));

// Middleware to log IP address of incoming requests
app.use((req, res, next) => {
    const attackerIP = req.headers['x-forwarded-for'] || req.socket.remoteAddress;
    req.attackerIP = attackerIP;
    next();
});

// Endpoint to trigger breach detection
app.get('/breach', (req, res) => {
    const attackerIP = req.attackerIP;
    console.log(`Breach detected from IP: ${attackerIP}`);
    // Call breach detection functions here
    res.send('Breach detected!');
});

// Start server
const PORT = 3000;
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});
```

Step 4: Run the Server:
Navigate to your project directory and start the server: 
```bash
node server.js
``` 
Accessing the GUI Open your web browser and navigate to http://localhost:3000 to interact with the security monitoring dashboard.

Step 5

if that doesn't work do this.

Create a file named server.js in your project directory and paste the provided code:
```bash
nano server.js
```
```bash
// Base64 encoded functions
const Base64 = {
  // Encode string to Base64
  encode: (str) => Buffer.from(str).toString('base64'),
  // Decode Base64 to string
  decode: (str) => Buffer.from(str, 'base64').toString('ascii'),
};

// Function to send email alert
const sendEmailAlert = (subject, body) => {
  // Send email alert (replace with your email sending code)
  console.log(`Email Alert: Subject - ${subject}, Body - ${body}`);
};

// Function to calculate the hash of a file
const calculateFileHash = (fileContent) => {
  // Mock hash calculation for demonstration
  return 'mocked_hash';
};

// Function to monitor file integrity
const monitorFileIntegrity = (directory) => {
  // Simulate file changes
  const fileChanges = ['index.php', 'wp-config.php'];

  fileChanges.forEach((file) => {
    const fileContent = getFileContent(file);
    const fileHash = calculateFileHash(fileContent);
    if (fileHash !== knownHashes[file]) {
      const subject = `File Change Detected: ${file}`;
      const body = `The file ${file} has been modified.`;
      sendEmailAlert(subject, body);
      knownHashes[file] = fileHash;
    }
  });
};

// Function to check for breaches and pull attacker's IP address
const checkForBreaches = (attackerIP) => {
  // Simulate breach detection
  const breachDetected = true;

  if (breachDetected) {
    // Quarantine site
    quarantineSite();
    // Optionally, take further action such as blocking network access
    blockNetworkAccess(attackerIP);
  }
};

// Function to quarantine site
const quarantineSite = () => {
  // Simulate quarantine
  console.log('Site Quarantined');
};

// Function to block network access
const blockNetworkAccess = (attackerIP) => {
  // Simulate blocking network access
  console.log(`Network Access Blocked for attacker IP: ${attackerIP}`);
};

// Function to add a new user with specified role
const addUser = (username, role) => {
  // Add user logic (mocked for demonstration)
  console.log(`User '${username}' added with role '${role}'`);
};

// Function to add super root account with password storage and encryption
const addSuperRootAccount = (username, password) => {
  // Encrypt password
  const encryptedPassword = encryptPassword(password);
  // Store encrypted password (mocked for demonstration)
  console.log(`Super root account '${username}' added with encrypted password '${encryptedPassword}'`);
};

// Function to encrypt password using a real-world encryption algorithm (e.g., bcrypt)
const encryptPassword = (password) => {
  // Example: Use bcrypt for password hashing and encryption
  const bcrypt = require('bcrypt');
  const saltRounds = 10;
  const hashedPassword = bcrypt.hashSync(password, saltRounds);
  return hashedPassword;
};

// Function to retrieve file content from a real-world source
const getFileContent = (fileName) => {
  // Example: Read file content from a database or external API
  return `File content of ${fileName}`;
};

// Function to add header
const addHeader = () => {
  return `
    <header>
      <h1>The Dragon's Lair</h1>
      <h2>The reason you should stay behind the fence</h2>
    </header>
  `;
};

// Function to add footer
const addFooter = () => {
  return `
    <footer>
      <p>Created by Blu Corbel</p>
    </footer>
  `;
};

// Function to start Node.js server with Express to retrieve attacker's IP address
const startServer = () => {
  const express = require('express');
  const app = express();

  // Middleware to log IP address of incoming requests
  app.use((req, res, next) => {
    const attackerIP = req.headers['x-forwarded-for'] || req.socket.remoteAddress;
    req.attackerIP = attackerIP;
    next();
  });

  // Endpoint to trigger breach detection
  app.get('/breach', (req, res) => {
    // Get attacker's IP address
    const attackerIP = req.attackerIP;
    // Process breach detection and take necessary actions
    console.log(`Breach detected from IP: ${attackerIP}`);
    checkForBreaches(attackerIP);
    res.send('Breach detected!');
  });

  // Start server
  const PORT = 3000;
  app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
  });
};

// Directory to monitor
const wordpressDirectory = '/path/to/wordpress';

// Dictionary to store known file hashes
const knownHashes = {};

// Populate known hashes initially (mocked for demonstration)
knownHashes['index.php'] = 'mocked_hash';
knownHashes['wp-config.php'] = 'mocked_hash';

// Monitor file integrity continuously
setInterval(() => {
  monitorFileIntegrity(wordpressDirectory);
}, 3600000); // Adjust the interval as needed (e.g., every hour)

// Example usage:
// Add a new user
addUser('newuser', 'admin');

// Add super root account
addSuperRootAccount('superroot', 'supersecretpassword');

// Start Node.js server to retrieve attacker's IP address
startServer();

// Add header and footer to the content
const header = addHeader();
const footer = addFooter();

// Example: Combine header, content, and footer
const content = "<p>Main content goes here</p>"; // Replace with actual content
const contentWithHeaderAndFooter = header + content + footer;
console.log(contentWithHeaderAndFooter);
```

Step 5: Running the Application
Run the application:
```bash
node server.js
```
Monitor File Integrity and Breach Detection:
The script will monitor file integrity every hour and check for breaches. 
It will simulate alerts and actions like quarantining the site and blocking the network access of an attacker. 
You can adjust the paths and logic to fit your actual use case.

Step 6: Testing the Application
Access the breach detection endpoint:Open a web browser and navigate to http://localhost:3000/breach. 
This should log an attacker’s IP address and simulate a breach detection scenario.

Verify User Management: The script includes functions to add users and a super root account with password encryption. 

These can be tested by examining the console output or by expanding the functionality to interact with a real user database.

Check the Logs: Monitor the console output for log messages related to file changes, breach detections, and other simulated actions.
