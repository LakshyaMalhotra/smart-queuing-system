# Smart Queuing System
This is the second project for Intel Edge AI for IoT developers nanodegree. In this project we are given three scenarios-
- Manufacturing
- Retail
- Transportation

These scenarios come from three different industry sectors which try to mimic the requirements of a real client. Our job will be to analyze the constraints, propose the hardware solution and build out and test the application on the [Intel DEVCloud](https://devcloud.intel.com/edge/). Specifically the goal is to build an application which reduces congestion and queuing systems, situations where the queues are not managed efficiently - one queue may be overloaded while another is empty. Along with the scenarios, sample video footage from the client is provided which can be used to test our applications' performance.

## Goal of the project
Reduce the congestion in the queues using [Intel's OpenVINO API](https://docs.openvinotoolkit.org/) and the person detection model from the [Open Model Zoo](https://docs.openvinotoolkit.org/2020.4/omz_models_intel_index.html) to count the number of people in each queue, so that people can be directed to the least congested queue. We need to build an application that finds the optimized solution for each scenario which satisfy the client's requirements like the limitations on the budgets they can spend on the hardware and the power consumption requirements for the hardware.

## Main Tasks
- Propose a possible hardware solution
- Build out the application and test its performance on the DevCloud using multiple hardware types
- Compare the performance to see which hardware performed best
- Validate the proposal based on the test results

## Project set-up
The model used for all the scenarios is `person-detection-retail-0013` which can be found in [Open Model Zoo](https://docs.openvinotoolkit.org/2020.4/omz_models_intel_index.html). The details of the model used for this project can be found [here](https://docs.openvinotoolkit.org/2020.4/omz_models_intel_person_detection_retail_0013_description_person_detection_retail_0013.html). All the code in the project ran on [Intel DEVCloud](https://devcloud.intel.com/edge/), so we don't need to set up anything locally.

## Benchmarks
All the scenarios are benchmarked for three metrics across different hardware - Model load time, Inference time and Frames per second.

## Scenario 1: Manufacturing line of Semiconductor Chips
> __Which hardware might be most appropriate for this scenario? (CPU/IGPU/VPU/FPGA)__
>
> __Proposed Hardware:__ FPGA

### Client's Requirements
| Requirements observed | How does the chosen hardware meet this requirement? |
| --- | --- |
| Client requirement is to do image processing 5 times per second on a video feed of 30-35 FPS | FPGA provides low latency as compared to other devices |
| It can be easily reprogrammed and optimized for other tasks like finding flaws in the semiconductor chips | FPGAs are ideal for this scenario because they are very flexible in the sense that they are field programmable |
| It should at least last for 5-10 years | FPGAs that use devices from Intel’s IoT group have a guaranteed availability of 10 years, from start to production | 
| Budget is not a constraint since the revenue is good | FPGAs are at least $1000 |

### Queue Monitoring Requirements
| Maximum number of people in the queue | 5 |
| --- | --- |
| __Model precision chosen (FP32, FP16, or INT8)__ | __FP16__ |

### Test Results

All the scenarios are benchmarked for three metrics across different hardware - Model load time, Inference time and Frames per second.
- __Model load time__

![model_load_time_manufacturing](images/model_load_time_manufacturing.png)

- __Inference time__

![inference_time_manufacturing](images/inference_time_manufacturing.png)

- __Frames per second__

![fps_manufacturing](images/fps_manufacturing.png)

### Final Hardware Recommendation
> As per the requirements listed above, __FPGA__ indeed proves out to be the best hardware for this scenario since it offers the highest frame rate and lowest inference time.

## Scenario 2: Retail Store
> __Which hardware might be most appropriate for this scenario? (CPU/IGPU/VPU/FPGA)__
>
> __Proposed Hardware:__ Integrated GPU that comes with core i7 systems of the client

### Client's Requirement
| Requirements observed | How does the chosen hardware meet this requirement? |
| --- | --- |
| Limited Budget | No need to buy new hardware, use the IGPU in the systems at the checkout counters |
| Latency should not be an issue since even on weekdays the average wait time for customers is around 230 seconds | IGPU offers comparatively higher latency as compared to devices like VPUs |
| Client also wants to save as much as possible on electric bill | IGPUs are pretty customizable as they have configurable power consumption option |

### Queue Monitoring Requirements
| Maximum number of people in the queue | 5 (during peak hours) |
| --- | --- |
| __Model precision chosen (FP32, FP16, or INT8)__ | __IGPU EUs are only optimized for FP16__ |

### Test Results

- __Model load time__

![model_load_time_retail](images/model_load_time_retail.png)

- __Inference time__

![inference_time_retail](images/inference_time_retail.png)

- __Frames per second__

![fps_retail](images/fps_retail.png)

### Final Hardware Recommendation
> The main requirements of the client were a limited budget and saving as much on electric bills as possible. The client already has modern systems equipped with core-i7. Although the model loading time for an __Integrated GPU__ is the highest but still it is the perfect hardware for this current scenario as it offers low latency and high frames per second with no additional cost.

## Scenario 3: City Metro Transportation Services
> __Which hardware might be most appropriate for this scenario? (CPU/IGPU/VPU/FPGA)__
>
> __Proposed Hardware:__ VPU (Intel Neural Compute Stick-2)

### Client's Requirements
| Requirements observed | How does the chosen hardware meet this requirement? |
| --- | --- |
| Client has a maximum budget of $300 per system and she would like to save as much as possible | VPUs are small, low-cost devices which can accelerate the performance of pre-existing CPUs |
| Save as much as on power requirements | VPUs are very low power devices |

### Queue Monitoring Requirements
| Maximum number of people in the queue | 15 (during rush hours) |
| --- | --- |
| __Model precision chosen (FP32, FP16, or INT8)__ | __FP16__ |

### Test Results

- __Model load time__

![model_load_time_transportation](images/model_load_time_transportation.png)

- __Inference time__

![inference_time_transportation](images/inference_time_transportation.png)

- __Frames per second__

![fps_transportation](images/fps_transportation.png)

### Final Hardware Recommendation
> Although VPUs have the slowest inference time, the qualities that make them very attractive are low-budget, low-power and very fast model loading time. These are the things that matter a lot to the client so our hardware recommendations are __Intel Neural Compute Stick-2__.

