# Introduction to Camera Kit

Developers can create camera applications by invoking the interfaces provided by Camera Kit (camera service). These applications access and operate camera hardware to perform basic functions such as preview, photo capture, and video recording. Additionally, more advanced operations can be achieved by combining interfaces, such as controlling the flash, adjusting exposure time, focusing or zooming, etc.

## Development Model

The camera captures and processes image and video data by accessing the camera hardware, precisely controlling the corresponding hardware components, and flexibly outputting image and video content. This meets the requirements for multi-lens hardware adaptation (e.g., wide-angle, telephoto, TOF) and multi-scenario adaptation (e.g., different resolutions, formats, and effects).

The workflow of the camera is illustrated in the figure below and can be summarized into three parts: camera input device management, session management, and camera output management.

- The camera device accesses the camera hardware to capture data, serving as the camera input stream.

- Session management configures the input stream, such as selecting which lenses to use for shooting. It also allows configuration of parameters like flash, exposure time, focus, and zoom to achieve different shooting effects, thereby adapting to various business scenarios. Applications can switch sessions to meet different shooting requirements.

- The camera's output stream is configured to deliver content as a preview stream, photo capture stream, or video stream.

Camera applications control the camera to perform basic operations such as image display (preview), photo saving (capture), and video recording. During these operations, the camera service manages the camera device to capture and output data. The captured image data is processed at the camera's underlying hardware device interface (HDI, Hardware Device Interfaces) and directly transmitted to specific functional modules via BufferQueue for further processing. BufferQueue, which does not require developer attention, ensures timely delivery of processed data from the underlying layer to the upper layer for image display.  

Taking video recording as an example: during the recording process, the media recording service first creates a video Surface for data transmission and provides it to the camera service. The camera service then controls the camera device to capture video data and generate a video stream. The captured data is processed by the underlying camera HDI and transmitted to the media recording service via the Surface. After processing the video data, the media recording service saves it as a video file, completing the recording process.