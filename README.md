# Affordable mobile robot for SMEs (OpenAMR)

## Introduction

Small and Medium Enterprises (SMEs) across various sectors can greatly benefit from Autonomous Mobile Robots (AMRs). In warehouses and distribution centers, AMRs automate goods movement and order fulfillment, optimizing logistics with a goods-to-person approach. Manufacturing plants enhance their production workflow through efficient material transport and logistics. Small family farms and greenhouses utilize AMRs for moving crops, feed, and equipment, improving operational efficiency.

Our project empowers you to build your own AMR using open-source designs and accessible manufacturing methods. This guide provides detailed drawings, 3D models, Bill of Materials (BOM), hardware architecture, navigation software, and user interface packages. Utilize straightforward manufacturing technologies to integrate advanced automation seamlessly into your business operations.

## Key features

- **Navigation**: LIDAR/SLAM
- **Drive type**: Differential drive
- **Weight**: ~60 kg
- **Camera view**: 120 degrees
- **Speed**: 1500-2000 mm/s (unloaded), 1200-1500 mm/s (loaded)
- **Positioning accuracy**: ±20 mm
- **Dimensions**: 600x800 mm
- **Battery**: 24/48 V, 48-56 Ah, 8 hours life
- **Communication**: Wi-Fi (2.4/5 GHz)
- **Load capacity**: up to 150 kg
- **Operating temperature**: -10°C to +50°C
- **Charging**: Contact/wireless

## Design and manufacturing

Our design is optimized for manufacturability, requiring only basic technologies such as laser cutting, bending, turning (optional), and 3D printing (optional). Using mostly 2mm thick metal sheets, the design is robust yet simple to produce, allowing one person to build the robot in just one day if every part is ready.

Here is how the chassis design looks like:

![Mobile Robot General View](https://github.com/openAMRobot/OpenAMR/blob/main/docs/hardware/pictures/AMR_views.jpg)

### Mechanical design and assembly

1. **Downloadable resources**:
    - Production drawings, 3D models, STEP, and DXF files
    - Specification sheet, including all parts and assemblies, sensors, and fasteners
2. **Fabrication process**:
    - Discuss the drawings with a contractor for cutting and bending metal.
    - Assemble the chassis following the provided sequence.
3. **Assembly steps**:
    - The chassis design and the recommended assembly sequence are illustrated in the provided images.
    - Detailed steps for assembling the drive wheels and other components are included.

### Hardware and software integration

1. **Electronics block diagram**:
    - Main single-board computer (SBC)
    - Safety sensors (US, IR, bumper), RPI camera, and LiDAR
    - Controller Teensy board and firmware
    - BLDC motors, drivers, and encoders
    - Batteries, BMS, and wireless charger
    - On/Off switch and Emergency button

2. **Main components**:
    - **Raspberry Pi 5**: For main computing tasks.
    - **LIDAR**: For mapping and navigation.
    - **Sensors**: For obstacle detection and safety.
    - **BLDC motors and drivers**: For movement control.
    - **Battery system**: For power supply.
    - **Wireless charging**: For autonomous charging.

3. **Software setup**:
    - **Linorobot**: Open-source software package for navigation and control.
    - **UI**: Built with Flask and Java for user interaction.
   
To get all files you should do the next commands:

        git clone https://github.com/openAMRobot/OpenAMR.git
  
        cd openAMR

        git submodule update --init --recursive

The **whole tutorial** about software installation is sectioned into different topics. Click [here](https://github.com/openAMRobot/OpenAMR/wiki/Getting-started) here to get started.
      
Here’s how the hardware architecture of the robot looks like:

![Mobile Robot General View](https://github.com/openAMRobot/OpenAMR/blob/main/docs/hardware/pictures/HW_schema_article.jpg)

### Practical applications and future enhancements

This versatile design can be adapted to create different types of robots for various logistics tasks. It can also be modified to carry tools or a roller cage, increasing its usefulness in various scenarios. Examples of practical applications include:

- Automating goods movement in warehouses
- Enhancing production workflows in manufacturing plants
- Improving operational efficiency in small farms and greenhouses

## Conclusion

This project provides a low-cost DIY autonomous mobile robot suitable for industrial automation or warehouse logistics. By open-sourcing our technology, we offer SMEs an opportunity to leverage advanced robotics without the high costs associated with research and development.

For any questions, please refer to the documentation or the open-source project Linorobot. Basic knowledge of electronics, software, and mechanics is required.

## Community management and moderation

Effective community management and moderation are essential to maintain a healthy and productive environment for collaboration. Our project welcomes contributions and feedback from the community to improve and evolve.

## Community profiles for public repositories

We are working on rules and suggestions to manage contributions and interactions within our repository. They include features like issue templates, pull request templates, and guidelines for contributors and will be published soon.

### A project's community profile

You can access the community profile of this repository by clicking on the "Community" tab on the repository's main page. This section provides all the necessary information and resources for contributors.

### A code of conduct 

We are preparing standards for behavior within the community. Information about Code of Conduct will be added soon to a `CODE_OF_CONDUCT.md` file in the root directory. Where we will outline the expected behavior and the process for reporting violations.

### Guidelines for repository contributors

We are working on information about the workflow, coding standards, and submission process to help contributors understand the best practices and expectations. This information will be outlined in a `CONTRIBUTING.md` file.

### License

This project is licensed under the MIT License. For more info please check `LICENSE` file in the root directory.

### Support Our Project
Help us bring innovative AI & robotics project to the next level!

[![Donate via PayPal](https://img.shields.io/badge/Donate-PayPal-blue.svg)](https://www.paypal.com/paypalme/BotshareAI)

Every contribution, big or small, helps us grow. Thank you for your support!

