# How to integrate Cypress WiFi producs into ST Micro devices
## Summmary
These instructions can work for almost any STM32 device. We will use the `STM32H747I-DISCO` board as an example. We are going to assume you are using git, a Murata Cypress WiFi module, the SDIO interface and STM32CubeMX for creating and configuring the device. Once configured, you can export to an IDE of your choice

## Design & Architecture

TODO: Insert Picture Here or point to another markdown file

## Details

These are step by step instructions on how to create your own project with your own board/MCU. Hopefully, it provides a general overview of what to for your MCU or board

* Create a git-repo or use an existing one
* Create a submodule -- we use the name of the board for project directory STM32H747I-DISCO. This directory name can be anything you want including the root of the repo. At the root of the repo, do the following

    `git submodule add --force https://github.com/cypresssemiconductorco/wifi-host-driver.git STM32H747I-DISCO/Middlewares/Third_Party/Cypress-WIFI/WHD`

* Start the STM32CubeMX application
  * Create a project for said board (or MCU)
  * When asked to initiliazed all peripherals, answer yes (this may take a while if you have not used this board before)
  * In "Pinout & Configuration" make sure SDMMC1 is enabled
  * From Middleware section, you depending on the MCU, you may have one or more processors. Select which processor you want to host the WiFi communications
    * Enable and configure FreeRTOS for the processor. We used the latest version (CMSIS_V2) as of this writing
    * Enable and configure LwIP for the processor (optional but you will need some IP stack)
      * TODO: **Under "Platform Settings" LWIP asks for a BSP Component driver. This can be a problem**
  * Enable/Disable any other peripherals, middleware you need
  * Save the project in the `STM32H747I-DISCO` directory. If asked if it is okay to overrite, please answer YES. The project (ioc) file should be alongside the `Middlewares`
  * In STM32CubeMX switch to `Project Manager` tab and select your IDE/Makefile project of choice
    * TODO: If you see warning wrt. LWIP or FreeRTOS, please continue
  * 
