---
title: DeepSkyDad FP1
categories: ["dustcaps", "lightboxes"]
description: DeepSkyDad FP1 Flat Field Panel
thumbnail: ./deep-sky-dad-fp1.webp
---

## Introduction

The DeepSkyDad FP1 is a flat field illumination panel designed for astrophotography. It provides uniform, adjustable lighting for capturing flat field calibration frames, which are essential for correcting optical vignetting, dust shadows, and pixel-to-pixel sensitivity variations in astronomical imaging.

## What is Flat Field Correction?

Flat field correction is a critical calibration technique in astrophotography that compensates for:

- **Vignetting**: Darkening at the edges of images due to optical design
- **Dust shadows**: Dark spots caused by dust on the sensor, filters, or optical elements
- **Pixel sensitivity variations**: Differences in how individual pixels respond to light
- **Optical path distortions**: Non-uniformities in the optical system

By capturing flat frames with uniform illumination, these systematic errors can be mathematically removed from your light frames during image processing.

## Features

The DeepSkyDad FP1 flat panel offers:

- **Adjustable Brightness**: Variable intensity control to match different optical setups and exposure requirements
- **Uniform Illumination**: Even light distribution across the panel surface for accurate flat field frames
- **Compact Design**: Lightweight and portable for use in the field or observatory
- **USB Connectivity**: Powered and controlled via USB connection
- **INDI Driver Support**: Full integration with INDI-based astronomy software platforms

## Connection

The FP1 connects to your imaging computer via USB cable. The INDI driver provides software control over the panel's brightness and on/off state.

### Requirements

- USB port on the control computer
- INDI library with DeepSkyDad FP1 driver support
- Compatible astronomy software (KStars/Ekos, etc.)

## Operation

### Basic Workflow

1. **Connect the Panel**: Plug the FP1 into a USB port and start the INDI driver
2. **Position the Panel**: Place the panel over your telescope's aperture, ensuring it covers the full light path
3. **Set Brightness**: Adjust the panel brightness so flat frame exposures reach 40-70% of your camera's dynamic range (check the histogram)
4. **Capture Flat Frames**: Take 15-20 flat field frames using the same camera settings (gain, offset) as your light frames
5. **Capture Dark Flats**: With the panel turned off or covered, capture 15-20 dark frames with the same exposure time as your flat frames

### Tips for Best Results

- Match your flat frame binning, gain, and offset to your light frames
- Aim for flat frame histograms that peak around 50% of your camera's maximum value
- Take fresh flat frames whenever you change filters, rotate the camera, or adjust focus
- Store flats organized by date, filter, and camera settings for easy reuse
- Consider taking flats at the beginning and end of your imaging session to account for any dust that may have settled

## Integration with KStars/Ekos

When used with KStars/Ekos, the FP1 can be integrated into automated calibration frame capture routines. The Capture module can control the panel brightness and coordinate flat frame acquisition with your camera and filter wheel.

## Troubleshooting

### Panel Not Detected

- Verify USB connection is secure
- Check that the INDI DeepSkyDad FP1 driver is installed and running
- Try a different USB port or cable
- Check USB device permissions on Linux systems

### Uneven Illumination

- Ensure the panel is properly centered over the telescope aperture
- Check that the panel surface is clean and free from obstruction
- Verify the panel is positioned close enough to the aperture for even coverage

### Brightness Issues

- If flat frames are too dim or too bright, adjust the panel brightness setting in the INDI driver
- Ensure your camera exposure time is appropriate (typically 1-3 seconds for flat frames)
- Check that your camera gain and offset match your light frame settings
