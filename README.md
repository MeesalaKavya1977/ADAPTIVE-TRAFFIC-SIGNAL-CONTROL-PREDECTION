# ADAPTIVE-TRAFFIC-SIGNAL-CONTROL-PREDECTION
By using machine learning with state-of-the-art, real-time object detection based on a deep Convolutional Neural Networks called You Only Look Once (YOLO). We can make the characteristics of the competing traffic that allows  the signalized road intersection.  


Proposed System Overview
Our proposed system takes an image from the CCTV cameras at traffic junctions as input for realtime traffic density calculation using image processing and object detection. This system can be
broken down into 3 modules: Vehicle Detection module, Signal Switching Algorithm, and
Simulation module. As shown in the figure below, this image is passed on to the vehicle detection
algorithm, which uses YOLO. The number of vehicles of each class, such as car, bike, bus, and
truck, is detected, which is to calculate the density of traffic. The signal switching algorithm uses
this density, among some other factors, to set the green signal timer for each lane. The red signal
times are updated accordingly. The green signal time is restricted to a maximum and minimum
value in order to avoid starvation of a particular lane. A simulation is also developed to
demonstrate the system’s effectiveness and compare it with the existing static system.


Vehicle Detection Module


● The proposed system uses YOLO (You only look once) for vehicle detection, which
provides the desired accuracy and processing time. A custom YOLO model was trained for
vehicle detection, which can detect vehicles of different classes like cars, bikes, heavy
vehicles (buses and trucks), and rickshaws.

● The dataset for training the model was prepared by scraping images from google and
labelling them manually using LabelIMG, a graphical image annotation tool.

● Then the model was trained using the pre-trained weights downloaded from the YOLO
website. The configuration of the .cfg file used for training was changed in accordance with
the specifications of our model. The number of output neurons in the last layer was set
equal to the number of classes the model is supposed to detect by changing the 'classes'
variable. In our system, this was 4 viz. Car, Bike, Bus/Truck, and Rickshaw. The number
of filters also needs to be changed by the formula 5*(5+number of classes), i.e., 45 in our
case.

● After making these configuration changes, the model was trained until the loss was
significantly less and no longer seemed to reduce. This marked the end of the training, and
the weights were now updated according to our requirements.

● These weights were then imported in code and used for vehicle detection with the help of
OpenCV library. A threshold is set as the minimum confidence required for successful
detection. After the model is loaded and an image is fed to the model, it gives the result in
a JSON format i.e., in the form of key-value pairs, in which labels are keys, and their
confidence and coordinates are values. Again, OpenCV can be used to draw the bounding boxes on the images from the labels and coordinates received. 
