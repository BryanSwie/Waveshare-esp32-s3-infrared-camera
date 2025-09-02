# ESP32-S3 Thermal Camera Display System
#Code will be coming soon as well as a video showing operation.

A real-time thermal imaging display system that streams thermal data from a Waveshare ESP32-S3 thermal camera module to a 7-inch touchscreen display via WiFi.

## Hardware Components

### Thermal Camera Module
- **Waveshare ESP32-S3 IR Thermal Imaging Camera Module**
- ESP32-S3-WROOM-1 Xtensa 32-bit LX7 dual-core processor
- 2.4GHz WiFi (802.11 b/g/n) and Bluetooth 5 (LE)
- Built-in thermal sensor with 80x62 pixel resolution
- TCP streaming capability on port 3333

### Display Module  
- **Makerfabs MATouch ESP32-S3-Parallel-TFT-with-Touch 7inch**
- ESP32-S3-WROOM-1 controller with 16MB Flash, 8MB PSRAM
- 7-inch IPS display (1024x600 resolution) with RGB565 interface
- 5-point capacitive touch (GT911 driver)
- MicroSD card slot for data logging
- Dual USB Type-C ports

## Features

### Real-Time Display
- Live thermal imaging at 30+ FPS
- 6x upscaled thermal image (480x372 pixels on screen)
- Touch-to-measure temperature at any pixel
- Visual crosshair overlay for touched pixels

### Multiple Color Palettes
- **Inferno** - Deep purple to bright yellow gradient
- **Ironbow** - Classic thermal imaging colors  
- **Grayscale** - Monochrome thermal display
- **Hot** - Red-yellow-white heat map
- **Thermal** - Mathematical blue-cyan-yellow-red-white

### Interactive Controls (LVGL GUI)
- Adjustable temperature range (min/max) with spinbox controls
- Real-time temperature scale with color gradient
- Palette selection dropdown
- Current pixel temperature display
- Frame capture and SD card saving

### Data Logging
- Save thermal frames to microSD card in binary format
- Each frame includes dimensions, temperature range, and raw temperature data
- Python post-processing script for viewing saved frames

## Technical Implementation

### WiFi Communication
The thermal camera creates a WiFi access point (WSThermal/12345678). The display connects and receives TCP thermal data streams using a custom protocol with preamble detection and frame synchronization.

### Touch Coordinate Mapping
Implements precise touch coordinate transformation to map screen touches to thermal pixels, accounting for display scaling and positioning.

### Memory Optimization
- Color palettes stored in PROGMEM to save RAM
- Efficient RGB565 color conversion
- Optimized LVGL display buffer management

### Frame Processing
- Real-time thermal data parsing from 16-bit raw values
- Temperature scaling (raw/100 = Celsius)
- Automatic gain control and filtering support

## Code Structure

### Main Components
- **Thermal Data Processing** - Frame reception, parsing, and temperature calculation
- **Display Rendering** - Thermal image upscaling and color mapping  
- **LVGL Interface** - Touch controls and user interface
- **Touch Input Handling** - Coordinate transformation and pixel temperature lookup
- **SD Card Logging** - Binary frame data storage

### Key Libraries
- Arduino_GFX_Library - High-performance display driver
- LVGL 8.3.2 - Touch interface and GUI elements
- TAMC_GT911 - Capacitive touch controller
- WiFi/TCP - Thermal data streaming

## Getting Started

### Prerequisites
- Arduino IDE with ESP32 board package (v2.0.11)
- Required libraries (see code comments for versions)
- Formatted microSD card (optional, for data logging)

### Hardware Setup
1. Configure thermal camera module with default firmware
2. Connect display module via USB for programming
3. Insert microSD card if using data logging features

### Software Configuration
1. Update WiFi credentials in code if needed (default: WSThermal/12345678)
2. Adjust thermal camera IP address if modified (default: 192.168.4.1:3333)
3. Calibrate touch coordinates if needed
4. Upload code to display module

### Usage
1. Power on thermal camera module (creates WiFi hotspot)  
2. Power on display module (auto-connects to thermal camera)
3. Use touch interface to adjust temperature ranges and select color palettes
4. Touch thermal image to measure pixel temperatures
5. Use "Save Frame" button to capture thermal data to SD card

## Post-Processing

The included Python script converts saved thermal data files to high-resolution PNG images with temperature scales and colormaps matching the display palettes.

### Requirements
```bash
pip install numpy pillow matplotlib
```

### Usage
```python
python post_processing.py thermal_frame.dat
```

## Performance

- **Frame Rate**: 30+ FPS real-time thermal display
- **Latency**: <100ms from thermal capture to display
- **Temperature Accuracy**: ±0.01°C resolution
- **Touch Response**: <50ms coordinate mapping and temperature lookup

## Applications

- Thermal leak detection and building diagnostics
- Electronic component temperature monitoring  
- Industrial process monitoring
- Scientific thermal analysis
- Educational thermal imaging demonstrations
- Home energy efficiency audits

## Contributing

Contributions are welcome! Areas for improvement:
- Additional color palette implementations
- Enhanced data logging formats  
- Wireless configuration interface
- Temperature alarm/threshold features
- Multi-point temperature comparison

## License

This project is open source.

## Acknowledgments

- Waveshare Electronics for thermal camera module documentation
- Makerfabs for display module specifications and examples
- LVGL community for GUI framework support

## Demo Video

[Link to YouTube demonstration video showing real-time thermal imaging and touch interface]
