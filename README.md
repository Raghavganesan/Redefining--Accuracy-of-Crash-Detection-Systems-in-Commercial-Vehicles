<h1>Redefining Accuracy of Crash Detection Systems in Commercial Vehicles</h1>
  <p><em>Arduino-based, low-cost crash detection with automated GPS/GSM emergency alerts</em></p>
<h2>Overview</h2>
<p>
This project designs and prototypes a <strong>real-time crash detection system</strong> for commercial (and personal) vehicles
using an <strong>Arduino Uno R3</strong>, an <strong>accelerometer</strong> for impact detection, and a <strong>GSM</strong> module that
automatically dispatches an <strong>SMS with GPS coordinates</strong> to emergency contacts when a collision is detected.
Auxiliary <strong>ultrasonic</strong> and <strong>sound</strong> sensors help validate true crash events and reduce false positives.
The solution is <strong>low-cost, modular, and power-aware</strong>, aiming to shorten emergency response times and improve survival outcomes.
</p>


<h3>Key Features</h3>
<ul>
  <li><strong>Impact detection:</strong> Accelerometer-driven crash identification with tunable thresholds.</li>
  <li><strong>Location &amp; alerting:</strong> GPS fix captured and <em>SMS alert</em> sent via GSM (auto-dial optional).</li>
  <li><strong>Multi-sensor validation:</strong> Ultrasonic proximity + sound level cues to curb false alarms.</li>
  <li><strong>Modular &amp; scalable:</strong> Easy to extend for fleets, add sensors, or swap comms (LoRa/Wi-Fi).</li>
  <li><strong>Open hardware/software:</strong> Arduino IDE + widely available libraries/components.</li>
</ul>

<h2>System Architecture</h2>
<p>
The Arduino collects signals from an <em>accelerometer</em>, <em>ultrasonic</em>, and <em>sound</em> sensor.
On confirmed impact, it reads <em>GPS</em> location and triggers the <em>GSM</em> module to notify predefined contacts.
</p>
<p><img width="608" height="460" alt="image" src="https://github.com/user-attachments/assets/2e2f0f7d-718c-49bd-b7cf-7a0376faa242" />
</p>

<h2>Hardware &amp; Software</h2>

<h3>Bill of Materials</h3>
<table>
  <thead>
    <tr><th>Component</th><th>Qty</th><th>Purpose</th></tr>
  </thead>
  <tbody>
    <tr><td>Arduino Uno R3</td><td>1</td><td>Core MCU: sensor fusion &amp; alert orchestration</td></tr>
    <tr><td>Accelerometer (e.g., ADXL355)</td><td>1</td><td>Impact/crash detection</td></tr>
    <tr><td>Ultrasonic Sensor</td><td>1</td><td>Proximity context to reduce false positives</td></tr>
    <tr><td>Sound Sensor</td><td>1</td><td>Loud-event corroboration (crash acoustics)</td></tr>
    <tr><td>GPS Module</td><td>1</td><td>Accurate latitude/longitude</td></tr>
    <tr><td>GSM Module (e.g., SIM800A)</td><td>1</td><td>SMS/call dispatch to emergency contacts</td></tr>
    <tr><td>Power Supply</td><td>1</td><td>Stable power to MCU and modules</td></tr>
  </tbody>
</table>
<h3>Toolchain &amp; Libraries</h3>
<ul>
  <li><strong>Arduino IDE</strong> (coding, compile, upload)</li>
  <li><strong>SoftwareSerial</strong> / <strong>AltSoftSerial</strong> (multi-UART comms)</li>
  <li><strong>TinyGPS++</strong> (GPS parsing)</li>
  <li><strong>Wire.h</strong> (I²C sensor comms)</li>
  <li><strong>Math.h</strong> (filters/thresholding)</li>
  <li>Optional: <em>Freeform/other EDA</em> for circuit visualization</li>
</ul>

<h2>How It Works</h2>
<ol>
  <li>MCU continuously samples accelerometer (impact), ultrasonic (distance), and sound level.</li>
  <li>When thresholds indicate a probable crash (e.g., 2 of 3 sensors concur), the event is latched.</li>
  <li>GPS coordinates are read; a formatted <strong>SMS alert</strong> (and/or phone call) is sent via GSM.</li>
  <li>Alert includes <strong>latitude, longitude</strong> and optional metadata (time, vehicle ID).</li>
</ol>


<h2>Results Snapshot</h2>
<img width="640" height="409" alt="image" src="https://github.com/user-attachments/assets/ea3b38c1-dc96-4a81-b0c1-684bd8183896" />

<ul>
  <li><strong>Alert Latency:</strong> Mean ≈ <strong>36.83 s</strong> from crash detection to GSM alert across 10 trials.</li>
  <li><strong>Range:</strong> ~<strong>35.57–37.35 s</strong> (stable with low variation, network-dependent).</li>
</ul>
<p style="font-size: 0.9em; opacity: 0.8;">
Note: GPS cold starts and GSM network quality are the main contributors to latency; maintaining backup power for GPS greatly reduces time-to-first-fix.
</p>

<h2>Setup</h2>
<details>
  <summary><strong>Wiring (quick guide)</strong></summary>
  <ul>
    <li>Connect accelerometer via I²C/SPI as per module pinout.</li>
    <li>Ultrasonic: TRIG/ECHO to Arduino digital pins (with level shifting if needed).</li>
    <li>Sound sensor: analog out to Arduino analog pin.</li>
    <li>GPS: UART to hardware/AltSoftSerial pins.</li>
    <li>GSM: UART to SoftwareSerial/AltSoftSerial; ensure dedicated 5V/4A capable supply.</li>
    <li>Common ground across all modules; decouple power rails.</li>
  </ul>
</details>
<h2>Roadmap / Future Work</h2>
<ul>
  <li>Add <strong>gyroscope/pressure</strong> sensing for better discrimination of crash vs. non-crash.</li>
  <li>Improve <strong>power strategy</strong> (backup battery, GPS hot-start, energy harvesting/solar).</li>
  <li>Alternate comms: <strong>LoRa, Wi-Fi, satellite</strong> for low-coverage regions.</li>
  <li>Higher-precision positioning (multi-band GNSS; hybrid GPS+Wi-Fi/BLE).</li>
  <li>Stronger processing (e.g., Cortex-M/RPi Pico) for <strong>on-device filtering</strong>.</li>
  <li>Vehicle <strong>CAN bus</strong> integration for richer telemetry.</li>
</ul>

<h2>Social &amp; Environmental Impact</h2>
<ul>
  <li><strong>SDG 3 (Health):</strong> Faster alerts can reduce fatalities/serious injuries.</li>
  <li><strong>SDG 11 (Cities):</strong> Safer, more responsive transport systems.</li>
  <li><strong>SDG 9 (Innovation):</strong> Accessible safety tech for broader adoption.</li>
</ul>
