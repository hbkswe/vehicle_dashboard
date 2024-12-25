# Vehicle Dashboard

## Overview
This project is a vehicle dashboard simulation built using Node-RED and MongoDB. The application displays real-time data such as motor RPM, battery percentage, and power consumption, and includes interactive controls for motor speed and charging. It fulfills the requirements outlined in the Epiroc challenge document.

## Stack Used

### Node-RED
- **Frontend**: Built using Node-RED Dashboard for UI components.
- **Backend**: Managed through Node-RED with JavaScript function nodes for logic.
- **Data Access**: Implemented using Node-RED nodes to connect with MongoDB.

### MongoDB
- Chosen for its reliability, ease of use, and compatibility with Node-RED.
- Data structure is kept simple for efficient storage and retrieval.
- All dashboard information is retrieved from the database, while controls (like sliders and buttons) trigger backend updates.

## Adjustments
- **Battery Cooling**: Added a natural cooling mechanism for the battery when the motor is not active.
- **Charging Indicator**: The charging button changes to green when the battery is charging.

## Installation and Setup
Follow the steps below to set up and run the project.

### Prerequisites
1. Install Node.js and npm from [Node.js](https://nodejs.org/).
2. Install MongoDB. See the "Setting Up MongoDB" section below for detailed instructions.
3. Install Node-RED. Use the following command:
   ```bash
   npm install -g --unsafe-perm node-red
   ```
4. Install necessary npm packages for the project:
   ```bash
   npm install mongodb node-red-dashboard
   ```

### Setting Up MongoDB

#### 1. Add MongoDB Repository and Install MongoDB
Run the following commands to add the official MongoDB repository and install MongoDB:

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu $(lsb_release -cs)/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
sudo apt update
sudo apt install -y mongodb-org
```

#### 2. Start and Enable MongoDB Service
Start the MongoDB service and enable it to start on boot:

```bash
sudo systemctl start mongod
sudo systemctl enable mongod
```

#### 3. Verify MongoDB Installation
Check if MongoDB is running:

```bash
sudo systemctl status mongod
```
You should see "active (running)" in the output.

#### 4. Install MongoDB Shell (Optional)
If you need the `mongosh` shell:

```bash
sudo apt install -y mongodb-mongosh
```

#### 5. Configure the Database
1. Launch the MongoDB shell:
   ```bash
   mongosh
   ```
2. Create a new database:
   ```javascript
   use vehicle_dashboard;
   ```
3. Create a collection and insert initial data:
   ```javascript
   db.dashboard_data.insertOne({
     "_id": "vehicle_001",
     "top_indicator_parking_brake": true,
     "top_indicator_check_engine": false,
     "top_indicator_motor_status": true,
     "top_indicator_battery_low": false,
     "gauge_power": 0,
     "gauge_motor_rpm": 0,
     "middle_gear_ratio": 3,
     "middle_battery_percentage": 100,
     "middle_battery_temperature": 47.51,
     "middle_motor_rpm": 2000,
     "middle_motor_speed_setting": 0,
     "bottom_button_gear": true,
     "bottom_button_motor": false,
     "bottom_button_battery_temperature": true,
     "bottom_button_view_menu": false,
     "bottom_button_charging": true
   });
   ```
4. Verify the data:
   ```javascript
   db.dashboard_data.find();
   ```

### Setting Up Node-RED
1. Start Node-RED:
   ```bash
   node-red
   ```
2. Open the Node-RED editor in your browser at `http://localhost:1880`.
3. Import the provided `flows.json` file:
   - Click the menu button in the top right corner of the Node-RED editor.
   - Select **Import > Clipboard**.
   - Paste the contents of `flows.json`.
   - Click **Import**.

### Hosting on AWS
This project is hosted on AWS using the instructions provided by Node-RED. Follow the steps below to set up your AWS instance:
1. Launch an EC2 instance on AWS:
   - Choose an Amazon Linux 2 AMI.
   - Select an instance type (e.g., t2.micro for free-tier eligibility).
   - Configure the instance details, including security groups to allow inbound traffic on port 1880.
2. SSH into the instance:
   ```bash
   ssh -i your-key.pem ec2-user@your-ec2-public-ip
   ```
3. Install Node.js and npm:
   ```bash
   curl -sL https://rpm.nodesource.com/setup_14.x | sudo bash -
   sudo yum install -y nodejs
   ```
4. Install Node-RED:
   ```bash
   sudo npm install -g --unsafe-perm node-red
   ```
5. Install necessary npm packages:
   ```bash
   npm install mongodb node-red-dashboard
   ```
6. Start Node-RED:
   ```bash
   node-red
   ```
7. Access Node-RED from your browser using the public IP of your EC2 instance: `http://your-ec2-public-ip:1880`.
8. Deploy your `flows.json` and configure MongoDB connections as needed.

### Running the Application
1. Ensure MongoDB is running and populated with initial data.
2. Start Node-RED and deploy the flows.
3. Open the dashboard in your browser at `http://your-ec2-public-ip:1880/ui` (or locally at `http://localhost:1880/ui`).
4. Interact with the dashboard:
   - Adjust motor speed using the slider.
   - Toggle the charging button.

## Project Features
- **Real-Time Data**: Updates dashboard elements with live data fetched from MongoDB.
- **Dynamic Indicators**: Reflect the state of parking brake, check engine, motor, and battery levels.
- **Interactive Controls**:
  - Motor speed slider adjusts RPM.
  - Charging button enables/disables charging mode.
- **Battery Behavior**:
  - Discharges when motor is active.
  - Charges when in charging mode.
  - Naturally cools when inactive.

## Submission Details
- Hosted Application: [[Static URL Placeholder]](http://35.183.40.111:1880/ui) static IP may change after EC2 restarts
- GitHub Repository: [[GitHub Repository Placeholder]](https://github.com/hbkswe/vehicle_dashboard)
- Public Database: MongoDB read-only access link [Database URL Placeholder]

## Additional Notes
- Documented code with meaningful comments.
- For any issues, refer to the GitHub repository or contact [Your Email Placeholder].

