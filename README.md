# Development of an artificial intelligence-based heat production control process


## Summary
| Company Name | [Mindreks Metall OÜ](https://mindreksmetall.ee/) |
| :--- | :--- |
| Development Team Lead Name | Tauri Tätte |
| Development Team Lead E-mail | [tauri.tatte@ut.ee](mailto:tauri.tatte@ut.ee) |
| Duration of the Demonstration Project | 09/2024-05/2025 |
| Final Report | [Final_report_r2.pdf](https://github.com/ai-robotics-estonia/2024_Experimenting_of_AI_based_heat_production_management_process/blob/main/assets/Final_report_r2.pdf) |

# Description
## Objectives of the Demonstration Project
The aim of the project was to develop an intelligent heat storage system designed for private homes and small consumers, which would allow the building owner to use several methods for heating (electric heating, heat pump, solid fuel boiler) by choosing the appropriate method and time. These functions can also be used alternately and in combination. The given solution can later be scaled for small-scale production along with imported heat pumps. The goal was to create an energy-efficient integrated heat storage system. Currently, a similar solution is completely absent from our market.

## Activities and Results of the Demonstration Project
### Challenge
During the project, several issues were addressed that enable home consumers to use energy in the most cost-effective way.
- Heating with electricity can often be more cost-effective than using a solid fuel boiler.
- The energy used for heating should be produced at the cheapest times (Nord Pool).
- Heating needs must be forecasted in advance and planned accordingly.
- The system must learn the building’s behavior based on climate changes.
- The solution must allow for the use of supplementary heating and account for this addition.
- The system must take solar radiation into account and its effects on the building.
- The system must consider wind speed and its cooling effect on the building.
- The system must account for the outside temperature and its cooling effect on the building.
- The device must operate autonomously (without connectivity).
- The device could utilize the thermal inertia of the building.


### Data Sources
We are adding a few low-cost auxiliary devices (a flow meter for the heating system and return flow temperature sensors) that will enable real-time feedback from the heating inputs in the future application. Additionally, we integrated weather forecast data (from weather.com) and Nord Pool energy prices into the device. From the weather forecast, we included cloud cover data (%), temperature (°C), and wind speed (m/s) at three-hour intervals.


### AI Technologies
Since the device must take into account the specific characteristics of the building in relation to wind, radiation, and temperature, we addressed this using continuously updated three-dimensional data tables (axes: temperature, wind speed, cloudiness). As there is a linear correlation between the heat transfer (heat loss) and the temperature, we replaced the third dimension of the table (temperature) with a linear function. The table was divided into ranges to ensure that the real-time learning period would not become excessively long (a maximum of 1 year).
Data written to the learning table is based on calculations per square meter, derived from total daily energy consumption (Figure 1), and is recorded in the table considering radiation and wind speed data. The values in the table are continuously adjusted to reflect the building’s changes over time (the expected device lifespan is up to 30 years).
During forecasting (at 3:00 PM), data is read from the table (based on the known temperature, cloud cover, and wind for the next day), and the energy consumption for the following day (kWh) is predicted. Based on this, the energy production cycle is scheduled, starting from 3:00 PM the previous day (Figure 2, Figure 3).
To ensure the most optimal approach, the operator is provided with three options, allowing the user to define which device is the primary preferred energy source in the system (electric heating, solid fuel heating, or heat pump). Each option was given separate functionality, with the system automatically considering the possibility that the user may also use other devices in the system as auxiliary heating sources.

![Figure 1. Training method](https://github.com/ai-robotics-estonia/2024_Experimenting_of_AI_based_heat_production_management_process/blob/main/assets/training_method.jpg)
*Figure 1. Training method*

![Figure 2. Timing of energy production and consumption](https://github.com/ai-robotics-estonia/2024_Experimenting_of_AI_based_heat_production_management_process/blob/main/assets/energy_production_consumption_timing.png)
*Figure 2. Timing of energy production and consumption*

![Figure 3. Target temperature request](https://github.com/ai-robotics-estonia/2024_Experimenting_of_AI_based_heat_production_management_process/blob/main/assets/target_temp_request.jpg)
*Figure 3. Target temperature request*

![Figure 4. Example of heat pump control](https://github.com/ai-robotics-estonia/2024_Experimenting_of_AI_based_heat_production_management_process/blob/main/assets/heat_pump_control.png)
*Figure 4. Example of heat pump control*

### Technological Results
During the project, various methods for solving the task were examined. According to the initial plan, the device was to be controlled by learning from the user’s usage patterns. However, this solution relied heavily on immeasurable parameters (sauna usage, randomness of additional heating, variability in the boiler operator's/heating objectives). Since we had previously developed an automation solution for this system based on an industrial controller (FX3U + integrated 7" HMI), we decided to continue using a similar approach for further control, ensuring high reliability and easy debugging for the company's employees. As a result, we achieved an good outcome based on algorithms that forecast energy consumption and take into account the behavior of all users.

During prototype testing, the solution is functioning, but it still requires refinement regarding the initial configuration of the data table, which we are currently working on. For the control system to operate accurately, the data table must be pre-configured with values based on square meters, but the differences between buildings are quite significant. However, these differences can be addressed by copying from the initial learning data of similar devices.


### Technical Architecture
The technical architecture of the solution is shown on Figure 5 below. 

![Figure 5. Technical architecture](https://github.com/ai-robotics-estonia/2024_Experimenting_of_AI_based_heat_production_management_process/blob/main/assets/heat_pump_control.png)
*Figure 5. Technical architecture*

### User Interface 
The end user sees the heating demand (the result of the prediction) directly on the screen (HMI). No other intermediate data is displayed to the user.

### Future Potential of the Technical Solution
The sample solution is educational in many ways across different fields, as similar approaches can be used to control various heating systems and energy production solutions, as well as to utilize surplus energy (which may not be practical to sell) or to use electric heating alongside conventional heating (when it is more cost-effective at a given time). The software solution can be reused in multiple scenarios, as the entire heating technology sector is moving toward increasingly optimized solutions. This presents a great opportunity to create cost-effective energy storage systems (using thermal storage) and to develop control solutions based on industrial controllers.

### Lessons Learned
Ongoing collaboration with the company in developing and refining the algorithms significantly improved the outcome. Throughout the project, the team gained a much deeper understanding of the physics behind building energy usage, which in turn revealed new opportunities for achieving greater energy savings. This enhanced insight allowed for more informed decision-making and the development of a more efficient and intelligent control solution.
