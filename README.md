<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Exhaust Sound System - Wemos D1 Mini</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 20px;
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: #fff;
            min-height: 100vh;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.1);
            padding: 30px;
            border-radius: 15px;
            backdrop-filter: blur(10px);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
        }
        h1 {
            text-align: center;
            color: #fff;
            margin-bottom: 30px;
            font-size: 2.5em;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }
        h2 {
            color: #ffd700;
            border-bottom: 2px solid #ffd700;
            padding-bottom: 10px;
            margin-top: 30px;
        }
        .wiring-section {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin: 20px 0;
        }
        .component-list {
            background: rgba(255, 255, 255, 0.1);
            padding: 20px;
            border-radius: 10px;
            border-left: 4px solid #ffd700;
        }
        .wiring-diagram {
            background: rgba(255, 255, 255, 0.95);
            padding: 20px;
            border-radius: 10px;
            color: #333;
            font-family: monospace;
            font-size: 14px;
            overflow-x: auto;
        }
        .code-section {
            background: rgba(0, 0, 0, 0.3);
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
            border-left: 4px solid #00ff88;
        }
        pre {
            background: rgba(0, 0, 0, 0.5);
            padding: 15px;
            border-radius: 8px;
            overflow-x: auto;
            font-size: 14px;
            line-height: 1.4;
        }
        code {
            color: #00ff88;
        }
        .pin-table {
            width: 100%;
            border-collapse: collapse;
            margin: 15px 0;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 8px;
            overflow: hidden;
        }
        .pin-table th, .pin-table td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        }
        .pin-table th {
            background: rgba(255, 215, 0, 0.2);
            font-weight: bold;
        }
        .note {
            background: rgba(255, 193, 7, 0.2);
            border: 1px solid #ffc107;
            padding: 15px;
            border-radius: 8px;
            margin: 15px 0;
        }
        .warning {
            background: rgba(220, 53, 69, 0.2);
            border: 1px solid #dc3545;
            padding: 15px;
            border-radius: 8px;
            margin: 15px 0;
        }
        @media (max-width: 768px) {
            .wiring-section {
                grid-template-columns: 1fr;
            }
            .container {
                padding: 20px;
            }
            h1 {
                font-size: 2em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🔧 Exhaust Sound System for Electric Motor</h1>
        
        <h2>📋 Required Components</h2>
        <div class="wiring-section">
            <div class="component-list">
                <h3>Main Components:</h3>
                <ul>
                    <li><strong>Wemos D1 Mini</strong> (ESP8266)</li>
                    <li><strong>MicroSD Card Module</strong></li>
                    <li><strong>MAX98357A I2S Amplifier</strong></li>
                    <li><strong>4-8Ω Speaker</strong> (3-5W)</li>
                    <li><strong>MicroSD Card</strong> (8GB+)</li>
                    <li><strong>Breadboard/PCB</strong></li>
                    <li><strong>Jumper Wires</strong></li>
                </ul>
                
                <h3>Optional:</h3>
                <ul>
                    <li>Potentiometer (volume control)</li>
                    <li>LED indicator</li>
                    <li>Case/enclosure</li>
                </ul>
            </div>
            
            <div class="wiring-diagram">
                <h3>Wiring Connections:</h3>
                <pre>
Wemos D1 Mini    →    Components
=====================================

SD Card Module:
D5 (GPIO14)      →    CLK (SCLK)
D6 (GPIO12)      →    MISO
D7 (GPIO13)      →    MOSI (CMD)
D8 (GPIO15)      →    CS
3.3V             →    VCC
GND              →    GND

MAX98357A I2S Amplifier:
D1 (GPIO5)       →    DIN (Data)
D2 (GPIO4)       →    BCLK (Bit Clock)
D3 (GPIO0)       →    LRC (Word Clock)
3.3V             →    VIN
GND              →    GND

Speaker:
MAX98357A +      →    Speaker +
MAX98357A -      →    Speaker -

RPM Input (from motor controller):
A0 (Analog)      →    RPM Signal (0-3.3V)

Optional LED:
D4 (GPIO2)       →    LED + (with resistor)
GND              →    LED -
                </pre>
            </div>
        </div>

        <h2>📊 Pin Assignment Table</h2>
        <table class="pin-table">
            <thead>
                <tr>
                    <th>Wemos Pin</th>
                    <th>GPIO</th>
                    <th>Component</th>
                    <th>Function</th>
                </tr>
            </thead>
            <tbody>
                <tr><td>D1</td><td>GPIO5</td><td>MAX98357A</td><td>I2S Data (DIN)</td></tr>
                <tr><td>D2</td><td>GPIO4</td><td>MAX98357A</td><td>Bit Clock (BCLK)</td></tr>
                <tr><td>D3</td><td>GPIO0</td><td>MAX98357A</td><td>Word Clock (LRC)</td></tr>
                <tr><td>D4</td><td>GPIO2</td><td>LED</td><td>Status Indicator</td></tr>
                <tr><td>D5</td><td>GPIO14</td><td>SD Module</td><td>SPI Clock</td></tr>
                <tr><td>D6</td><td>GPIO12</td><td>SD Module</td><td>SPI MISO</td></tr>
                <tr><td>D7</td><td>GPIO13</td><td>SD Module</td><td>SPI MOSI</td></tr>
                <tr><td>D8</td><td>GPIO15</td><td>SD Module</td><td>Chip Select</td></tr>
                <tr><td>A0</td><td>ADC0</td><td>Motor Controller</td><td>RPM Input</td></tr>
            </tbody>
        </table>

        <div class="warning">
            <strong>⚠️ Important Notes:</strong>
            <ul>
                <li>MAX98357A operates at 3.3V - perfect for D1 Mini</li>
                <li>SD card module should be 3.3V compatible</li>
                <li>RPM input should not exceed 3.3V (use voltage divider if needed)</li>
                <li>Speaker impedance should be 4-8Ω, power rating 3-5W</li>
            </ul>
        </div>

        <h2>💻 Arduino Code</h2>
        <div class="code-section">
            <h3>Main Arduino Sketch (exhaust_sound.ino):</h3>
            <pre><code>
#include "AudioFileSourceSD.h"
#include "AudioGeneratorWAV.h"
#include "AudioOutputI2S.h"
#include &lt;SPI.h&gt;
#include &lt;SD.h&gt;

// Pin definitions
#define SD_CS_PIN    15  // D8
#define RPM_PIN      A0  // Analog input for RPM
#define LED_PIN      2   // D4
#define I2S_DOUT     5   // D1
#define I2S_BCLK     4   // D2  
#define I2S_LRC      0   // D3

// Audio objects
AudioGeneratorWAV *wav;
AudioFileSourceSD *file;
AudioOutputI2S *out;

// Engine sound parameters
int currentRPM = 0;
int lastRPM = 0;
String currentSoundFile = "";
unsigned long lastRPMCheck = 0;
unsigned long soundChangeDelay = 100; // ms

// RPM ranges and corresponding sound files
struct RPMRange {
  int minRPM;
  int maxRPM;
  String soundFile;
};

RPMRange rpmRanges[] = {
  {0, 800, "/idle.wav"},
  {800, 1500, "/low_rpm.wav"},
  {1500, 2500, "/mid_rpm.wav"},
  {2500, 3500, "/high_rpm.wav"},
  {3500, 5000, "/redline.wav"}
};

int numRanges = sizeof(rpmRanges) / sizeof(RPMRange);

void setup() {
  Serial.begin(115200);
  delay(1000);
  
  // Initialize pins
  pinMode(LED_PIN, OUTPUT);
  pinMode(RPM_PIN, INPUT);
  
  // Blink LED during startup
  for(int i = 0; i < 3; i++) {
    digitalWrite(LED_PIN, HIGH);
    delay(200);
    digitalWrite(LED_PIN, LOW);
    delay(200);
  }
  
  Serial.println("Initializing Exhaust Sound System...");
  
  // Initialize SD card
  if (!SD.begin(SD_CS_PIN)) {
    Serial.println("SD Card initialization failed!");
    while(1) {
      digitalWrite(LED_PIN, HIGH);
      delay(100);
      digitalWrite(LED_PIN, LOW);
      delay(100);
    }
  }
  Serial.println("SD Card initialized successfully");
  
  // List files on SD card
  listSDFiles();
  
  // Initialize audio output
  out = new AudioOutputI2S();
  out->SetPinout(I2S_BCLK, I2S_LRC, I2S_DOUT);
  out->SetGain(0.8); // Adjust volume (0.0 to 1.0)
  
  Serial.println("System ready!");
  digitalWrite(LED_PIN, HIGH);
}

void loop() {
  // Check if current audio is still playing
  if (wav && wav->isRunning()) {
    if (!wav->loop()) {
      // Current sound finished, restart it for looping
      wav->stop();
      file->close();
      delete wav;
      delete file;
      startCurrentSound();
    }
  }
  
  // Check RPM periodically
  if (millis() - lastRPMCheck > soundChangeDelay) {
    updateRPM();
    lastRPMCheck = millis();
  }
  
  delay(10);
}

void updateRPM() {
  // Read analog input (0-1023) and convert to RPM (0-5000)
  int analogValue = analogRead(RPM_PIN);
  currentRPM = map(analogValue, 0, 1023, 0, 5000);
  
  // Add some smoothing
  currentRPM = (currentRPM + lastRPM) / 2;
  
  // Check if we need to change sound file
  String newSoundFile = getSoundFileForRPM(currentRPM);
  
  if (newSoundFile != currentSoundFile) {
    Serial.print("RPM: ");
    Serial.print(currentRPM);
    Serial.print(" - Switching to: ");
    Serial.println(newSoundFile);
    
    // Stop current sound
    if (wav && wav->isRunning()) {
      wav->stop();
      file->close();
      delete wav;
      delete file;
    }
    
    currentSoundFile = newSoundFile;
    startCurrentSound();
  }
  
  lastRPM = currentRPM;
}

String getSoundFileForRPM(int rpm) {
  for (int i = 0; i < numRanges; i++) {
    if (rpm >= rpmRanges[i].minRPM && rpm < rpmRanges[i].maxRPM) {
      return rpmRanges[i].soundFile;
    }
  }
  return "/idle.wav"; // Default fallback
}

void startCurrentSound() {
  if (currentSoundFile.length() > 0) {
    file = new AudioFileSourceSD(currentSoundFile.c_str());
    wav = new AudioGeneratorWAV();
    
    if (wav->begin(file, out)) {
      Serial.print("Playing: ");
      Serial.println(currentSoundFile);
      digitalWrite(LED_PIN, HIGH);
    } else {
      Serial.print("Failed to start: ");
      Serial.println(currentSoundFile);
      digitalWrite(LED_PIN, LOW);
    }
  }
}

void listSDFiles() {
  Serial.println("Files on SD card:");
  File root = SD.open("/");
  while (true) {
    File entry = root.openNextFile();
    if (!entry) break;
    
    Serial.print("  ");
    Serial.print(entry.name());
    Serial.print(" (");
    Serial.print(entry.size());
    Serial.println(" bytes)");
    
    entry.close();
  }
  root.close();
}
            </code></pre>
        </div>

        <h2>📦 Required Libraries</h2>
        <div class="code-section">
            <p>Install these libraries through Arduino IDE Library Manager:</p>
            <pre><code>
1. ESP8266Audio by Earle Philhower
   - Search for: "ESP8266Audio"
   - This includes AudioFileSourceSD, AudioGeneratorWAV, AudioOutputI2S

2. SD (usually pre-installed with Arduino IDE)

3. SPI (usually pre-installed with Arduino IDE)
            </code></pre>
        </div>

        <h2>🎵 Sound File Preparation</h2>
        <div class="note">
            <h3>Audio File Requirements:</h3>
            <ul>
                <li><strong>Format:</strong> WAV files (16-bit, mono or stereo)</li>
                <li><strong>Sample Rate:</strong> 22kHz or 44.1kHz</li>
                <li><strong>File Names:</strong> idle.wav, low_rpm.wav, mid_rpm.wav, high_rpm.wav, redline.wav</li>
                <li><strong>Length:</strong> 2-5 seconds each (will loop automatically)</li>
                <li><strong>Size:</strong> Keep files under 1MB each for smooth playback</li>
            </ul>
            
            <h3>Sound File Sources:</h3>
            <ul>
                <li>Record real exhaust sounds with smartphone</li>
                <li>Use free sound libraries (freesound.org)</li>
                <li>Generate synthetic engine sounds with audio software</li>
                <li>Extract from YouTube videos (convert to WAV)</li>
            </ul>
        </div>

        <h2>🔧 Calibration & Testing</h2>
        <div class="code-section">
            <h3>RPM Calibration:</h3>
            <ol>
                <li>Connect RPM signal from your motor controller</li>
                <li>Open Serial Monitor (115200 baud)</li>
                <li>Observe RPM readings vs actual motor speed</li>
                <li>Adjust the <code>map(analogValue, 0, 1023, 0, 5000)</code> values</li>
                <li>Modify RPM ranges in the array to match your motor</li>
            </ol>
            
            <h3>Volume Control:</h3>
            <p>Adjust <code>out->SetGain(0.8)</code> value between 0.0-1.0</p>
            
            <h3>Response Speed:</h3>
            <p>Change <code>soundChangeDelay</code> for faster/slower sound transitions</p>
        </div>

        <div class="warning">
            <h3>🔋 Power Considerations:</h3>
            <ul>
                <li>D1 Mini: ~80mA</li>
                <li>SD Module: ~20mA</li>
                <li>MAX98357A + Speaker: 100-500mA (depending on volume)</li>
                <li><strong>Total:</strong> Plan for 1A power supply minimum</li>
                <li>Use 5V supply with 3.3V regulator for best results</li>
            </ul>
        </div>

        <h2>🎯 Next Steps</h2>
        <div class="note">
            <ol>
                <li>Wire components according to diagram</li>
                <li>Install required libraries in Arduino IDE</li>
                <li>Upload the code to Wemos D1 Mini</li>
                <li>Prepare WAV files and copy to SD card root directory</li>
                <li>Connect RPM signal from your motor controller</li>
                <li>Test and calibrate RPM ranges</li>
                <li>Fine-tune volume and response timing</li>
            </ol>
        </div>
    </div>
</body>
</html>
