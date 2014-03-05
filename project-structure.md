# Project Structure

* Application: each application = one repository
  * PHP-Extensions
  * C-Lib
  * PHP-Apps
  * HTTP-Webserver
* Kernel: each block in architecture = one repository
  * File-System
  * Event-Manager
  * Scheduler + Process Management
  * ...
  * Driver: each driver as folder
    * GPIO
    * ...
* HAL: one repository -> components as folder

![Projectstructure](https://raw.github.com/BRO-FHV/docs/master/images/projectstructure.png)
