# E-Ink Display Project

This project provides a system for controlling an E-Ink display using an ESP32 chip. It includes both the firmware for the ESP32 and a CLI tool for sending images to the display over a network connection.

## Features

- ESP32 firmware for controlling an E-Ink display
- CLI tool for rendering and sending images to the display
- Various image processing options including resizing, cropping, and dithering
- Nix-based development environment

## Prerequisites

- Nix package manager
- ESP32 development board
- E-Ink display compatible with the provided firmware

## Setup

1. Clone this repository
2. Ensure you have Nix installed on your system

## Firmware Setup

1. Modify the WiFi SSID, password, and static IP in `src/srvr.h`
2. Use the provided Nix shell commands to compile and upload the firmware:

```
nix develop
init # only needed once
compile
upload
```

You can monitor the ESP32 for errors using:

```
monitor
```

## CLI Usage

The main command for interacting with the E-Ink display is `eink`. Here are the available subcommands:

### Display an Image

```
eink <image_file>
```

This will automatically render the image and send it to the display.

### Render an Image

```
eink render [options] -i <input_image>
```

Options:
- `-s, --style=num`: Specify a dithering style (1-49)
- `--no-resize`: Don't resize, only crop
- `--no-center`: Don't crop to the center

The rendered image is saved to `/tmp/eink.png` by default.

### Send a Rendered Image to the Display

```
eink draw [image_location]
```

This sends the specified image to the display. If no image location is provided, it defaults to `/tmp/eink.png`.

### Explore Rendering Styles

```
eink styles [image_file]
```

This generates examples of different rendering styles in `/tmp/didder_tests`.

## Development

This project uses a Nix flake for dependency management and development environment setup. To enter the development environment:

```
nix develop
```

This will provide you with all necessary tools including `arduino-cli`, `node2nix`, and required Python packages.

## Project Structure

- `src/`: Contains C and Arduino code for the ESP32 firmware
- `bin/`: Contains the main `eink` script
- `libexec/`: Contains scripts for image rendering and display communication
- `didders`: A file containing dithering options
- `nix/`: Nix-related files for dependency management

## Temporary Files

The project creates temporary files in the `/tmp` directory, such as `/tmp/eink.png` for the rendered image. These files are used for intermediate processing steps and communication with the E-Ink display.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License:

MIT License

Copyright (c) 2024 Denis

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
