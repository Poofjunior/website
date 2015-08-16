---
layout: bootstrap
years: [2014, 2013, 2012, 2011]
---
<div class="container">
  <div class="row">
    <div class="col-md-2">
      <div class="well sidebar-nav fixed">
{% for year in page.years %}
<center>
<h3><a href="#{{ year }}"><i class="icon-chevron-right"></i>{{ year }}</a></h3>
</center>
{% endfor %}
    </div> <!-- well sidebar-nav fixed -->
  </div> <!-- col-md-2 -->
  <div class="col-md-10 offset2">
    <div class="jumbotron">

<h1>Research</h1>
<h2>Publications and Development for Hardware, Software, and Undergraduate Courses</h2>
<section id="2014">

<h2>2014</h2>
<h3>Raspberry Pi Peripherals Library</h3>
<img src="/img/research_pics/pi_library.png" width="180" align="left" Hspace="10">
I co-developed a minimalistic Raspberry Pi Peripherals library with <a href="http://sarahlichtman.wordpress.com/">Sarah Lichtman</a></li>.
This library provides a memory-mapped alternative to the traditional Wiring
library, enabling PIC-like programming with direct access to bitfields.
This library serves as the back bone behind a number of textbook examples in the
third edition of <a href="http://www.elsevier.com/books/digital-design-and-computer-architecture/harris/978-0-12-370497-9#description">Digital Design and Computer Architecture</a></li>
by Harris and Harris.

<section id="2013">
<h2>2013</h2>
<h3>Underwater Field Robotics: The Malta Cistern Mapping Project</h3>
<img src="/img/research_pics/rovScans2.jpg" width="220" align="left" Hspace="10">
<b>Towards Three-Dimensional Underwater Mapping Without Odometry</b>
<br>Dobke, A., Vasquez, J., Lieu, L., Chasnov, B., Clark, C., Dunn, I., Wood, Z.
<a href="http://newwww.hmc.edu/lair/publications/2013/dobke_UUST_2013.pdf">PDF</a></li>

Received by the Unmanned Untethered Submersible Technology Conference (UUST 2013).
<br>
This paper details the LatticeMap Algorithm, an algorithm developed for fitting sequential ROV
sonar scans using a iterative least-squares fitting technique.  Scans were taken from ancient
Cisterns in Malta during the Spring of 2013.


The International Computer Engineering Experience (ICEX) Program is a multi-disciplinary, 
multi-year project focused on the three-dimensional mapping of submerged archaeological sites.
Within this program, students build upon sensor-based map-making techniques, such as 
particle filtering and SLAM, to construct 3D maps of underwater cisterns. The task itself 
combines both field robot deployments and data analysis. 


Ths past summer, the ICEX team collected scans from numerous cisterns in Malta to construct
maps using a new scan-matching algorithm.

<h3>Underwater Field Robotics: ROV hardware additions through the CAN Bus interface</h3>
<IMG SRC="/img/research_pics/arduinoCAN_Mod.jpg" width="180" align="left" Hspace="10">
Following the most recent data-collection deployment in Malta in the Spring
of 2013, I have been developing a rotating mount for performing underwater sonar
scans at various angles. This mount is an independent embedded system attached to 
the robot underwater and driven by a software link over the ROV's CAN Bus interface. 
<br>

<h3>The Combat Robotics Experimental Learning Project</h3>
Beginning in fall 2012 and concluding the following spring, the HMC combat 
robotics club designed and fabricated a competitve combat robot with the final 
goal of participating in Robogames, 2013 in San Mateo, California. From this 
experience, our team designed and built Robespierre, a 220 [lb]. combat robot 
featuring novel competitive techniques. Robespierre features several 
hundred components, most of which were machined by a handful of students over
three months during the spring semester.

Chiefly, Robespierre's fabrication represents one of the student body's 
proudest achievements as an entirely student-driven design project. 
Through a combination of research, design, fabrication, testing, and management,
we have augmented motivation for pursuing a deep understanding of the process 
in what most of us consider to be a "side-project" apart from our school work.


<center>
<iframe  height="240" src="//www.youtube.com/embed/RHK80IQjZ_4" frameborder="0" allowfullscreen></iframe>
<br> A brief video demoing a spinner weapon field test
</center>

At the competition, Robespierre stood out as one of the first new competitors in years in Robogames' 220 [lb.] weight category.

This project is featured in <a href='http://www.hmc.edu/files/communications/magazines-hmc-bulletin/HMC_Bulletin_SU13-903.pdf'> HMC's Bulletin of Experimental Learning</a>, and progess pictures are documented on the <a href='https://www.facebook.com/pages/Harvey-Mudd-Combat-Robot-Club/134567813384420'>Robespierre Webpage</a>.
</section>

<section id="2012">
<h2>2012</h2>
<h3>Open Source MEMs Sensor Driver Development under a ROS Framework</h3>
<h6> Developed at the Bosch Research and Technology Center</h6>
<IMG SRC="/img/research_pics/memsBot.svg" width="400" align="left" Hspace="10">
MEMs sensors offer the robotics community the benefit of their small form-factor 
and fairly high-precision measurements for state-estimation algorithms. 
Nevertheless, the protocols necessary to retrieve the data are often 
chip-specific, necessitating a software driver to communicate in the correct 
manner. Furthermore, these MEMs sensors cannot be directly connected to the 
computer operating the robot. Rather, they must first be connected to an 
embedded development board that serves as the hardware interface between raw 
sensor and computer. However, software drivers must also be written to interface
with these boards as well. 

To simplify the hassle of retreiving data from these sensors and bringing it 
cleanly into a high-level algorithm, I developed a software framework that
formed a hardware abstraction layer for these sensors under Robot Operating 
System (ROS).  Thus, a roboticist could simply setup the physical cables to the
chip, enter the hardware configuration as parameters, and retrieve fresh 
sensor data from the chips without needing to understand the 
specific protocol details needed to extract the data from these chips.
The current set of C++ drivers supports two development boards, an Arduino Uno
and a Sub-20, as well as three of Bosch's MEMs sensors:
the 
<a href='http://wiki.ros.org/bmp085_driver?distro=groovy'>BMP085 pressure sensor</a>, the 
<a href='http://wiki.ros.org/bma180_driver?distro=groovy'>BMA180 accelerometer</a>, and the
<a href='http://wiki.ros.org/bmc050_driver?distro=groovy'>BMC050 accelerometer/magnetometer</a>. 
Maximum throughput of sensor data is limited by the latency of the computer's USB connection and currently tested at speeds up to 500 [Hz].
The entire software package can be downloaded from the <a href='http://wiki.ros.org/bosch_drivers?distro=groovy'>bosch-ros-pkg</a> and is currently maintained
by my project advisor, Philip Roan.
</section>

<section id="2011">
<h2>2011</h2>
<h3>Development of the framework for the Robotics Choice Lab Course</h3>

The Robotics Choice Lab course at Harvey Mudd College began in the Spring of 2012.
During the prior summer, I co-developed the hardware platform and setup the first implementation of the Robot drivers in ROS.
Furthermore, I developed the layout for the initial layout for the first few Lab assignments listed on the class <a href='https://www.cs.hmc.edu/twiki/bin/view/Robotics/RoboticsChoiceLabSpring2012'>homepage</a>.

In the following spring, I was given the chance to actually take this class.
For the team final project, Jake Low and I developed a control system for the Parrot AR Drone using the angular displacements of a flat board as seen by a Kinect Depth Sensor.
The final results of this project are documented in the video below and a brief writeup about the preliminary development is documented <a href='https://www.cs.hmc.edu/twiki/bin/view/Robotics/JoshuaVasquez_JakeLow_Lab5_Spring2012'>here</a>
<center>
<iframe width="420" height="315" src="//www.youtube.com/embed/rX-yrE1iTMU" frameborder="0" allowfullscreen></iframe>
</center>

<h3>Redesign of the Autonomous Vehicles Course</h3>
<img src="/img/research_pics/mudduino.png" width="150" align="left" Hspace="10">
<a href='http://newwww.hmc.edu/lair/E11/'>E11: Autonomous Vehicles</a>, is a freshmen introductory course to circuits, programming, and controls.
The course features a broad introduction to software tools, such as Solidworks; embedded programming tools, such as the Arduino; and machine shop experience.
Students build a robot base from a starter kit and develop software to interpret binary sequences, known as <a href='http://en.wikipedia.org/wiki/Gold_code'>gold codes</a>, emitted from IR emitting beacons.
Following this stage, they then develop algorithms to compete in an autonomous game of capture-the-flag by programming their robots to read specific gold codes and respond by tagging beacons for points.

Following the course's first run in Fall 2010, I joined a team of students under Professor Harris to redesign the course for the following year.
Within this semester, we produced several revisions to streamline the course in its coming years.
Namely, we redeveloped the robot starter kit, produced a second revision of the robot's printed circuit board to eliminate hardware bugs discovered in the first year, and redesigned the lab exercises to promote a better understanding of the material.

Since this relaunching of the course, I  have served as a member of the student teaching team for the three following years.
Within this time, I have served as head tutor for two years and currently act as a lab proctor.
I have written the example solutions to the programming assignments written in Arduino, and I have also independently revised the robot pcb for the course's fourth year, further reducing the number of design errors.
</section>

        </div>  <!-- col-md-10 offset2 -->
      </div> <!-- jumbotron -->
   </div> <!-- row -->
</div> <!-- container -->
