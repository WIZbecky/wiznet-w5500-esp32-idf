# ESP32 Module로 W5500을 이용한 개발 시작하기 

## 목차

-   [소개](#Introduction)
-   [Step 1: Componetnt](#Step-1)
-   [Step 2: Hardware Configuration](#Step-2)
-   [Step 3: ESP-IDF Tool Configureation](#Step-3)
-   [더 보기](#ReadMore)

<a name="Introduction"></a>
## Introduction

**문서의 주요 내용**

이 문서는 ESP-IDF Tool을 이용하여 ESP32 Module에 W5500을 연동하기 위한 개발 환경 구축 및 예제 코드 실행 과정에 대해 설명합니다.
이 문서는 ESP32-DevKitC Module, WIZ850io Module, Windows 기반으로 작성되었으며, 그 외의 환경에서도 구현 가능합니다.

각 과정에는 다음 내용들이 포함되어 있습니다:
- ESP32-IDF Tool 설치
- ESP32-IDF Tool 설정
- ESP32 Module과 W5500 Module의 하드웨어 연결

<a name="Step-1"></a>
## Step 1: Componetnt
- Hardware
  - **ESP32 Module**
    - [ESP32-DevKitC](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/hw-reference/esp32/get-started-devkitc.html)
    - [ESP-WROVER-KIT](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/hw-reference/esp32/get-started-wrover-kit.html)
    - [ESP32-PICO-KIT](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/hw-reference/esp32/get-started-pico-kit.html)
    - [ESP32-Ethernet-Kit](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/hw-reference/esp32/get-started-ethernet-kit.html)
    - [ESP32-DevKit-S(-R)](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/hw-reference/esp32/user-guide-devkits-r-v1.1.html)
  - **W5500 Module**
    - [WIZ850io](http://wiznetshop.co.kr/product/detail.html?product_no=742)
  - **USB cable**
  - **Windows, Linux, Mac OS 기반의 PC**

- Software
  - **ESP-IDF Tool 설치**
    - Windows - [https://dl.espressif.com/dl/esp-idf-tools-setup-2.3.exe](https://dl.espressif.com/dl/esp-idf-tools-setup-2.3.exe)
    - Linux, mac OS
      ```
      cd ~/esp
      git clone -b v4.2 --recursive https://github.com/espressif/esp-idf.git
      cd ~/esp/esp-idf
      ./install.sh
      ```

<a name="Step-2"></a>
## Step 2: Hardware Configuration
ESP32 Module과 W5500 Module의 SPI interface Pin들과 RST, 3.3V, GND, INT Pin을 연결합니다. 
ESP32-DevKitC Module과 WIZ850io Module을 사용하여 결한한 예시로 Pinmap에 맞춰 Example Confirgure를 설정합니다.
다른 모듈, 다른 Pinmap 일 경우 환경에 맞춰 Example Configuration 설정이 필요합니다.
ESP-32 Module의 경우 모든 GPIO PIN 들이 SPI Interface PIN으로 살용될 수 있습니다. 

| ESP-32 | W5500     |
| ------ | --------- |
| GPIO23 | SPI_CLK   |
| GPIO19 | SPI_MOSI  |
| GPIO18 | SPI_MISO  |
| GPIO21 | SPI_CS    |
| GPIO4  | Interrupt |
| GPIO5  | Reset     |
| GND    | GND       |
| 3.3V   | 3.3V      |

![](pinmap.PNG)

<a name="Step-3"></a>
## Step 3: ESP-IDF Tool Configuration

  - **export script** 를 실행합니다.
    - Windows
	`%userprofile%\esp\esp-idf\export.bat`
	- Linux, mac OS
	`.$HOME/esp/esp-idf/export.ps1`
	
  - **Target chip**을 설정합니다.
    ```
	cd esp-idf/example/ethernet/basic
    idf.py set-target esp32
    ```
	
  - Project configuration 을 위한 **menuconfig**를 실행합니다.
    `idf.py menuconfig`
	![](menuconfig.PNG)
  - `Example Configureation` 을 통해 SPI Interface 등의 **Hardware 연결**을 설정합니다.
    ![](menuconfig-ExampleConfiguration.PNG)

<a name="ReadMore"></a>	
## 더 보기
* [Ethernet-Basic Example][ESP32-Example-Ethernet-Basic]	
[ESP32-Example-Ethernet-Basic]: ./ethernet-basic.md