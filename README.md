Exhaust Sound System for Electric Motor
📋 Required Components
Main Components:

    Wemos D1 Mini (ESP8266)
    MicroSD Card Module
    MAX98357A I2S Amplifier
    4-8Ω Speaker (3-5W)
    MicroSD Card (8GB+)
    Breadboard/PCB
    Jumper Wires

Optional:

    Potentiometer (volume control)
    LED indicator
    Case/enclosure


Wiring Connections:

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
                

📊 Pin Assignment Table
Wemos Pin 	GPIO 	Component 	Function
D1	GPIO5	MAX98357A	I2S Data (DIN)
D2	GPIO4	MAX98357A	Bit Clock (BCLK)
D3	GPIO0	MAX98357A	Word Clock (LRC)
D4	GPIO2	LED	Status Indicator
D5	GPIO14	SD Module	SPI Clock
D6	GPIO12	SD Module	SPI MISO
D7	GPIO13	SD Module	SPI MOSI
D8	GPIO15	SD Module	Chip Select
A0	ADC0	Motor Controller	RPM Input
⚠️ Important Notes:

    MAX98357A operates at 3.3V - perfect for D1 Mini
    SD card module should be 3.3V compatible
    RPM input should not exceed 3.3V (use voltage divider if needed)
    Speaker impedance should be 4-8Ω, power rating 3-5W

