# TL50 Light Controller

A Python-based controller for Banner Engineering TL50 indicator lights using serial communication. This project allows you to control various aspects of TL50 lights including colors, animations, and intensity through a simple command interface.

## Features

- Multiple animation modes (steady, flash, chase, intensity sweep, etc.)
- 14 different color options
- 4 intensity levels
- Support for dual-color animations
- Checksum validation for reliable communication
- USB serial interface support
- Debug mode for testing

## Requirements

- Python 3.x
- PySerial library
- Banner Engineering TL50 light(s)

## Installation

1. Clone this repository
2. Install required dependencies:
   ```bash
   pip install pyserial
   ```

## Usage

The script can be run with various parameters to control the light behavior. Here's a basic example:

```python
ser.write(set_segment(
    intensity="high",
    color_num_one="rose",
    color_num_two="blue",
    animation="two_color_flash"
))
```

### Available Parameters

#### Colors
- green
- red
- orange
- amber
- yellow
- lime_green
- spring_green
- cyan
- sky_blue
- blue
- violet
- magenta
- rose
- white

#### Intensity Levels
- high
- medium
- low
- off

#### Animation Modes
- off
- steady
- flash
- two_color_flash
- half_half
- half_half_rot
- chase
- intens_sweep

### Debug Mode

Run the script with the `--debug` flag to enable debug output:

```bash
python script.py --debug
```

## Serial Configuration

The script uses the following serial settings:
- Baudrate: 19200
- Default port: '/dev/tty.usbserial-FT791OX9' (can be modified as needed)

## Protocol Details

The controller uses Banner Engineering's serial protocol with checksum validation. Each command consists of a 30-byte hex string plus a 2-byte checksum. The command structure is:

```
[0xF4, 0x41, 0xC1, 0x1F, ...] + [checksum_byte1, checksum_byte2]
```

### Checksum Calculation

The checksum is calculated using the following method:
1. Sum all command bytes
2. Perform ones complement (XOR with 0xFFFF)
3. Split into two bytes
4. Append to command string

## Notes

- For chase animations, color_num_two serves as the background color, while color_num_one is the moving color
- Commands require a small delay (0.09s) between transmissions for reliable operation
- Multiple lights can be controlled by initializing additional serial ports

## Contributing

Feel free to submit issues, fork the repository, and create pull requests for any improvements.

## License

MIT License

Copyright (c) 2023

## Resources
https://www.youtube.com/watch?v=crRyCEbCWO8&ab_channel=BannerEngineering
https://www.bannerengineering.com/th/en/products/lighting-and-indicators/tower-lights/50mm-tower-lights-tl50-series.html
