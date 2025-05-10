<sdf version='1.7'>
  <world name='default'>
    <spherical_coordinates>
      <surface_model>EARTH_WGS84</surface_model>
      <latitude_deg>47.3977</latitude_deg>
      <longitude_deg>8.54559</longitude_deg>
      <elevation>0</elevation>
      <heading_deg>0</heading_deg>
    </spherical_coordinates>
    <physics type='ode'>
      <ode>
        <solver>
          <type>quick</type>
          <iters>100</iters>
          <sor>1</sor>
          <use_dynamic_moi_rescaling>0</use_dynamic_moi_rescaling>
        </solver>
        <constraints>
          <cfm>0</cfm>
          <erp>0.2</erp>
          <contact_max_correcting_vel>0.1</contact_max_correcting_vel>
          <contact_surface_layer>0</contact_surface_layer>
        </constraints>
      </ode>
      <real_time_update_rate>400</real_time_update_rate>
      <max_step_size>0.0025</max_step_size>
      <real_time_factor>1</real_time_factor>
    </physics>
    <scene>
      <shadows>0</shadows>
      <ambient>0.4 0.4 0.4 1</ambient>
      <background>0.7 0.7 0.7 1</background>
    </scene>
    <light name='sun' type='directional'>
      <cast_shadows>1</cast_shadows>
      <pose>500 500 1200 0 -0 0</pose>
      <diffuse>0.8 0.8 0.8 1</diffuse>
      <specular>0.2 0.2 0.2 1</specular>
      <attenuation>
        <range>2000</range>
        <constant>0.9</constant>
        <linear>0.01</linear>
        <quadratic>0.001</quadratic>
      </attenuation>
      <direction>0 0 -1</direction>
      <spot>
        <inner_angle>0</inner_angle>
        <outer_angle>0</outer_angle>
        <falloff>0</falloff>
      </spot>
    </light>
    <model name='ground_plane'>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <pose>0 0 0 0 -0 0</pose>
          <geometry>
            <plane>
              <normal>0 0 1</normal>
              <size>500 500</size>
            </plane>
          </geometry>
          <surface>
            <friction>
              <ode>
                <mu>1</mu>
                <mu2>1</mu2>
              </ode>
              <torsional>
                <ode/>
              </torsional>
            </friction>
            <contact>
              <ode/>
            </contact>
            <bounce/>
          </surface>
          <max_contacts>10</max_contacts>
        </collision>
        <visual name='grass'>
          <pose>0 0 0 0 -0 0</pose>
          <cast_shadows>0</cast_shadows>
          <geometry>
            <plane>
              <normal>0 0 1</normal>
              <size>300 500</size>
            </plane>
          </geometry>
          <material>
            <script>
              <uri>file://media/materials/scripts/Gazebo.material</uri>
              <name>Gazebo/Grass</name>
            </script>
          </material>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <gravity>0 0 -9.8</gravity>
    <magnetic_field>6e-06 2.3e-05 -4.2e-05</magnetic_field>
    <atmosphere type='adiabatic'/>
    <wind/>
    <model name='edrn'>
      <link name='edrn/base_link'>
        <inertial>
          <pose>0 0 -0 0 -0 0</pose>
          <mass>9.00001</mass>
          <inertia>
            <ixx>0.303756</ixx>
            <ixy>0.000448492</ixy>
            <ixz>0.00101597</ixz>
            <iyy>0.277221</iyy>
            <iyz>-0.00180629</iyz>
            <izz>0.469164</izz>
          </inertia>
        </inertial>
        <collision name='edrn/base_link_inertia_collision'>
          <pose>0 0 0 0 -0 0</pose>
          <geometry>
            <box>
              <size>0.3 0.3 0.6</size>
            </box>
          </geometry>
          <surface>
            <contact>
              <collide_bitmask>4294967295</collide_bitmask>
              <ode/>
            </contact>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
            <bounce/>
          </surface>
          <max_contacts>10</max_contacts>
        </collision>
        <visual name='edrn/base_link_inertia_visual'>
          <pose>0 0 0 0 -0 0</pose>
          <geometry>
            <mesh>
              <scale>0.1 0.1 0.1</scale>
              <uri>/home/avant/catkin_ws/src/ardupilot_gazebo/models/kopterworx/meshes/kopterworx_model_simple.dae</uri>
            </mesh>
          </geometry>
        </visual>
        <visual name='edrn/base_link_fixed_joint_lump__edrn/camera_box_visual_1'>
          <pose>0 0.2 -0.3 -3.14159 0.000796 -1.5708</pose>
          <geometry>
            <mesh>
              <scale>1 1 1</scale>
              <uri>/home/avant/catkin_ws/src/ardupilot_gazebo/models/util/asus_xtion_pro_camera.dae</uri>
            </mesh>
          </geometry>
        </visual>
        <velocity_decay>
          <linear>0.001</linear>
          <angular>0.001</angular>
        </velocity_decay>
        <sensor name='camera' type='depth'>
          <update_rate>30</update_rate>
          <camera name='head'>
            <horizontal_fov>1.39626</horizontal_fov>
            <image>
              <width>640</width>
              <height>480</height>
              <format>B8G8R8</format>
            </image>
            <clip>
              <near>0.02</near>
              <far>300</far>
            </clip>
            <noise>
              <type>gaussian</type>
              <mean>0</mean>
              <stddev>0.007</stddev>
            </noise>
          </camera>
          <plugin name='camera_plugin' filename='libgazebo_ros_openni_kinect.so'>
            <baseline>0.2</baseline>
            <alwaysOn>1</alwaysOn>
            <updateRate>0.0</updateRate>
            <cameraName>edrn/camera_ir</cameraName>
            <imageTopicName>/edrn/camera/color/image_raw</imageTopicName>
            <cameraInfoTopicName>/edrn/camera/color/camera_info</cameraInfoTopicName>
            <depthImageTopicName>/edrn/camera/depth/image_raw</depthImageTopicName>
            <depthImageCameraInfoTopicName>/edrn/camera/depth/camera_info</depthImageCameraInfoTopicName>
            <pointCloudTopicName>/edrn/camera/depth_registered/points</pointCloudTopicName>
            <frameName>edrn/camera</frameName>
            <pointCloudCutoff>0.3</pointCloudCutoff>
            <pointCloudCutoffMax>10.0</pointCloudCutoffMax>
            <distortionK1>0</distortionK1>
            <distortionK2>0</distortionK2>
            <distortionK3>0</distortionK3>
            <distortionT1>0</distortionT1>
            <distortionT2>0</distortionT2>
            <CxPrime>0</CxPrime>
            <Cx>0</Cx>
            <Cy>0</Cy>
            <focalLength>0</focalLength>
            <hackBaseline>0</hackBaseline>
            <robotNamespace>/</robotNamespace>
          </plugin>
          <pose>0 0.2 -0.5 0 -0 0.032741</pose>
        </sensor>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
      <joint name='edrn/odometry_sensor_joint' type='revolute'>
        <pose relative_to='edrn/base_link'>0 0 0 0 -0 0</pose>
        <parent>edrn/base_link</parent>
        <child>edrn/odometry_sensor_link</child>
        <axis>
          <xyz>1 0 0</xyz>
          <limit>
            <lower>0</lower>
            <upper>0</upper>
            <effort>0</effort>
            <velocity>0</velocity>
          </limit>
          <dynamics>
            <spring_reference>0</spring_reference>
            <spring_stiffness>0</spring_stiffness>
          </dynamics>
        </axis>
      </joint>
      <link name='edrn/odometry_sensor_link'>
        <pose relative_to='edrn/odometry_sensor_joint'>0 0 0 0 -0 0</pose>
        <inertial>
          <pose>0 0 0 0 -0 0</pose>
          <mass>0.01</mass>
          <inertia>
            <ixx>1e-05</ixx>
            <ixy>0</ixy>
            <ixz>0</ixz>
            <iyy>1e-05</iyy>
            <iyz>0</iyz>
            <izz>1e-05</izz>
          </inertia>
        </inertial>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
      <joint name='edrn/rotor_0_joint' type='revolute'>
        <pose relative_to='edrn/base_link'>0.367696 -0.367696 0.115 0 -0 0</pose>
        <parent>edrn/base_link</parent>
        <child>edrn/rotor_0</child>
        <axis>
          <xyz>0 0 1</xyz>
          <limit>
            <lower>-1e+16</lower>
            <upper>1e+16</upper>
          </limit>
          <dynamics>
            <spring_reference>0</spring_reference>
            <spring_stiffness>0</spring_stiffness>
          </dynamics>
        </axis>
      </joint>
      <link name='edrn/rotor_0'>
        <pose relative_to='edrn/rotor_0_joint'>0 0 0 0 -0 0</pose>
        <inertial>
          <pose>0 0 0 0 -0 0</pose>
          <mass>0.01</mass>
          <inertia>
            <ixx>2.925e-06</ixx>
            <ixy>0</ixy>
            <ixz>0</ixz>
            <iyy>0.00101542</iyy>
            <iyz>0</iyz>
            <izz>0.00101812</izz>
          </inertia>
        </inertial>
        <collision name='edrn/rotor_0_collision'>
          <pose>0 0 0 0 -0 0</pose>
          <geometry>
            <cylinder>
              <length>0.005</length>
              <radius>0.285</radius>
            </cylinder>
          </geometry>
          <surface>
            <contact>
              <collide_bitmask>4294967295</collide_bitmask>
              <ode/>
            </contact>
            <friction>
              <ode/>
              <torsional>
                <ode/>
              </torsional>
            </friction>
            <bounce/>
          </surface>
          <max_contacts>10</max_contacts>
        </collision>
        <visual name='edrn/rotor_0_visual'>
          <pose>0 0 0 0 -0 0</pose>
          <geometry>
            <mesh>
              <scale>0.003 0.003 0.003</scale>
              <uri>/home/avant/catkin_ws/src/ardupilot_gazebo/models/util/propeller_ccw.dae</uri>
            </mesh>
          </geometry>
          <material>
            <script>
              <name>Gazebo/Blue</name>
              <uri>file://media/materials/scripts/gazebo.material</uri>
            </script>
          </material>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
      <joint name='edrn/rotor_1_joint' type='revolute'>
        <pose relative_to='edrn/base_link'>0.367696 0.367696 0.115 0 -0 0</pose>
        <parent>edrn/base_link</parent>
        <child>edrn/rotor_1</child>
        <axis>
          <xyz>0 0 1</xyz>
          <limit>
            <lower>-1e+16</lower>
            <upper>1e+16</upper>
          </limit>
          <dynamics>
            <spring_reference>0</spring_reference>
            <spring_stiffness>0</spring_stiffness>
          </dynamics>
        </axis>
      </joint>
      <link name='edrn/rotor_1'>
        <pose relative_to='edrn/rotor_1_joint'>0 0 0 0 -0 0</pose>
        <inertial>
          <pose>0 0 0 0 -0 0</pose>
          <mass>0.01</mass>
          <inertia>
            <ixx>2.925e-06</ixx>
            <ixy>0</ixy>
            <ixz>0</ixz>
            <iyy>0.00101542</iyy>
            <iyz>0</iyz>
            <izz>0.00101812</izz>
          </inertia>
        </inertial>
        <collision name='edrn/rotor_1_collision'>
          <pose>0 0 0 0 -0 0</pose>
          <geometry>
            <cylinder>
              <length>0.005</length>
              <radius>0.285</radius>
            </cylinder>
          </geometry>
          <surface>
            <contact>
              <collide_bitmask>4294967295</collide_bitmask>
              <ode/>
            </contact>
            <friction>
              <ode/>
              <torsional>
                <ode/>
              </torsional>
            </friction>
            <bounce/>
          </surface>
          <max_contacts>10</max_contacts>
        </collision>
        <visual name='edrn/rotor_1_visual'>
          <pose>0 0 0 0 -0 0</pose>
          <geometry>
            <mesh>
              <scale>0.003 0.003 0.003</scale>
              <uri>/home/avant/catkin_ws/src/ardupilot_gazebo/models/util/propeller_cw.dae</uri>
            </mesh>
          </geometry>
          <material>
            <script>
              <name>Gazebo/Red</name>
              <uri>file://media/materials/scripts/gazebo.material</uri>
            </script>
          </material>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
      <joint name='edrn/rotor_2_joint' type='revolute'>
        <pose relative_to='edrn/base_link'>-0.367696 0.367696 0.115 0 -0 0</pose>
        <parent>edrn/base_link</parent>
        <child>edrn/rotor_2</child>
        <axis>
          <xyz>0 0 1</xyz>
          <limit>
            <lower>-1e+16</lower>
            <upper>1e+16</upper>
          </limit>
          <dynamics>
            <spring_reference>0</spring_reference>
            <spring_stiffness>0</spring_stiffness>
          </dynamics>
        </axis>
      </joint>
      <link name='edrn/rotor_2'>
        <pose relative_to='edrn/rotor_2_joint'>0 0 0 0 -0 0</pose>
        <inertial>
          <pose>0 0 0 0 -0 0</pose>
          <mass>0.01</mass>
          <inertia>
            <ixx>2.925e-06</ixx>
            <ixy>0</ixy>
            <ixz>0</ixz>
            <iyy>0.00101542</iyy>
            <iyz>0</iyz>
            <izz>0.00101812</izz>
          </inertia>
        </inertial>
        <collision name='edrn/rotor_2_collision'>
          <pose>0 0 0 0 -0 0</pose>
          <geometry>
            <cylinder>
              <length>0.005</length>
              <radius>0.285</radius>
            </cylinder>
          </geometry>
          <surface>
            <contact>
              <collide_bitmask>4294967295</collide_bitmask>
              <ode/>
            </contact>
            <friction>
              <ode/>
              <torsional>
                <ode/>
              </torsional>
            </friction>
            <bounce/>
          </surface>
          <max_contacts>10</max_contacts>
        </collision>
        <visual name='edrn/rotor_2_visual'>
          <pose>0 0 0 0 -0 0</pose>
          <geometry>
            <mesh>
              <scale>0.003 0.003 0.003</scale>
              <uri>/home/avant/catkin_ws/src/ardupilot_gazebo/models/util/propeller_ccw.dae</uri>
            </mesh>
          </geometry>
          <material>
            <script>
              <name>Gazebo/Blue</name>
              <uri>file://media/materials/scripts/gazebo.material</uri>
            </script>
          </material>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
      <joint name='edrn/rotor_3_joint' type='revolute'>
        <pose relative_to='edrn/base_link'>-0.367696 -0.367696 0.115 0 -0 0</pose>
        <parent>edrn/base_link</parent>
        <child>edrn/rotor_3</child>
        <axis>
          <xyz>0 0 1</xyz>
          <limit>
            <lower>-1e+16</lower>
            <upper>1e+16</upper>
          </limit>
          <dynamics>
            <spring_reference>0</spring_reference>
            <spring_stiffness>0</spring_stiffness>
          </dynamics>
        </axis>
      </joint>
      <link name='edrn/rotor_3'>
        <pose relative_to='edrn/rotor_3_joint'>0 0 0 0 -0 0</pose>
        <inertial>
          <pose>0 0 0 0 -0 0</pose>
          <mass>0.01</mass>
          <inertia>
            <ixx>2.925e-06</ixx>
            <ixy>0</ixy>
            <ixz>0</ixz>
            <iyy>0.00101542</iyy>
            <iyz>0</iyz>
            <izz>0.00101812</izz>
          </inertia>
        </inertial>
        <collision name='edrn/rotor_3_collision'>
          <pose>0 0 0 0 -0 0</pose>
          <geometry>
            <cylinder>
              <length>0.005</length>
              <radius>0.285</radius>
            </cylinder>
          </geometry>
          <surface>
            <contact>
              <collide_bitmask>4294967295</collide_bitmask>
              <ode/>
            </contact>
            <friction>
              <ode/>
              <torsional>
                <ode/>
              </torsional>
            </friction>
            <bounce/>
          </surface>
          <max_contacts>10</max_contacts>
        </collision>
        <visual name='edrn/rotor_3_visual'>
          <pose>0 0 0 0 -0 0</pose>
          <geometry>
            <mesh>
              <scale>0.003 0.003 0.003</scale>
              <uri>/home/avant/catkin_ws/src/ardupilot_gazebo/models/util/propeller_cw.dae</uri>
            </mesh>
          </geometry>
          <material>
            <script>
              <name>Gazebo/Red</name>
              <uri>file://media/materials/scripts/gazebo.material</uri>
            </script>
          </material>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
      <joint name='imu_joint' type='revolute'>
        <pose relative_to='edrn/base_link'>0 0 0 0 -0 0</pose>
        <parent>edrn/base_link</parent>
        <child>imu_link</child>
        <axis>
          <xyz>1 0 0</xyz>
          <limit>
            <lower>0</lower>
            <upper>0</upper>
            <effort>0</effort>
            <velocity>0</velocity>
          </limit>
          <dynamics>
            <spring_reference>0</spring_reference>
            <spring_stiffness>0</spring_stiffness>
          </dynamics>
        </axis>
      </joint>
      <link name='imu_link'>
        <pose relative_to='imu_joint'>0 0 0 0 -0 0</pose>
        <inertial>
          <pose>0 0 0 0 -0 0</pose>
          <mass>0.01</mass>
          <inertia>
            <ixx>0.001</ixx>
            <ixy>0</ixy>
            <ixz>0</ixz>
            <iyy>0.001</iyy>
            <iyz>0</iyz>
            <izz>0.001</izz>
          </inertia>
        </inertial>
        <sensor name='imu_sensor' type='imu'>
          <always_on>1</always_on>
          <update_rate>50</update_rate>
          <visualize>1</visualize>
          <topic>/edrn/imu</topic>
          <pose>0 0 0 -3.14159 -0 0</pose>
          <plugin name='imu_plugin' filename='libgazebo_ros_imu_sensor.so'>
            <topicName>/edrn/imu</topicName>
            <bodyName>imu_link</bodyName>
            <updateRateHZ>50.0</updateRateHZ>
            <gaussianNoise>0.0</gaussianNoise>
            <xyzOffset>0 0 0</xyzOffset>
            <rpyOffset>0 0 0</rpyOffset>
            <frameName>edrn/imu</frameName>
            <robotNamespace>/</robotNamespace>
          </plugin>
          <imu/>
        </sensor>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
      <plugin name='gazebo_ros_control' filename='libgazebo_ros_control.so'>
        <robotNamespace>/edrn/</robotNamespace>
        <robotParam>/edrn/robot_description</robotParam>
        <robotSimType>gazebo_ros_control/DefaultRobotHWSim</robotSimType>
      </plugin>
      <plugin name='rosbag' filename='librotors_gazebo_multirotor_base_plugin.so'>
        <robotNamespace>edrn</robotNamespace>
        <linkName>edrn/base_link</linkName>
        <rotorVelocitySlowdownSim>15</rotorVelocitySlowdownSim>
      </plugin>
      <plugin name='front_left_motor_model' filename='librotors_gazebo_motor_model.so'>
        <jointName>edrn/rotor_1_joint</jointName>
        <linkName>edrn/rotor_1</linkName>
        <turningDirection>cw</turningDirection>
        <timeConstantUp>0.0125</timeConstantUp>
        <timeConstantDown>0.0125</timeConstantDown>
        <maxRotVelocity>667</maxRotVelocity>
        <motorConstant>0.0002440724623743665</motorConstant>
        <momentConstant>0.044148079282817</momentConstant>
        <commandSubTopic>edrn/gazebo/command/motor_speed</commandSubTopic>
        <motorNumber>1</motorNumber>
        <rotorDragCoefficient>8.06428e-05</rotorDragCoefficient>
        <rollingMomentCoefficient>1e-06</rollingMomentCoefficient>
        <motorVelocityTopic>edrn/motor_vel/1</motorVelocityTopic>
        <rotorVelocitySlowdownSim>15</rotorVelocitySlowdownSim>
        <robotNamespace>/</robotNamespace>
      </plugin>
      <plugin name='front_right_motor_model' filename='librotors_gazebo_motor_model.so'>
        <jointName>edrn/rotor_0_joint</jointName>
        <linkName>edrn/rotor_0</linkName>
        <turningDirection>ccw</turningDirection>
        <timeConstantUp>0.0125</timeConstantUp>
        <timeConstantDown>0.0125</timeConstantDown>
        <maxRotVelocity>667</maxRotVelocity>
        <motorConstant>0.0002440724623743665</motorConstant>
        <momentConstant>0.044148079282817</momentConstant>
        <commandSubTopic>edrn/gazebo/command/motor_speed</commandSubTopic>
        <motorNumber>0</motorNumber>
        <rotorDragCoefficient>8.06428e-05</rotorDragCoefficient>
        <rollingMomentCoefficient>1e-06</rollingMomentCoefficient>
        <motorVelocityTopic>edrn/motor_vel/0</motorVelocityTopic>
        <rotorVelocitySlowdownSim>15</rotorVelocitySlowdownSim>
        <robotNamespace>/</robotNamespace>
      </plugin>
      <plugin name='back_left_motor_model' filename='librotors_gazebo_motor_model.so'>
        <jointName>edrn/rotor_2_joint</jointName>
        <linkName>edrn/rotor_2</linkName>
        <turningDirection>ccw</turningDirection>
        <timeConstantUp>0.0125</timeConstantUp>
        <timeConstantDown>0.0125</timeConstantDown>
        <maxRotVelocity>667</maxRotVelocity>
        <motorConstant>0.0002440724623743665</motorConstant>
        <momentConstant>0.044148079282817</momentConstant>
        <commandSubTopic>edrn/gazebo/command/motor_speed</commandSubTopic>
        <motorNumber>2</motorNumber>
        <rotorDragCoefficient>8.06428e-05</rotorDragCoefficient>
        <rollingMomentCoefficient>1e-06</rollingMomentCoefficient>
        <motorVelocityTopic>edrn/motor_vel/2</motorVelocityTopic>
        <rotorVelocitySlowdownSim>15</rotorVelocitySlowdownSim>
        <robotNamespace>/</robotNamespace>
      </plugin>
      <plugin name='back_right_motor_model' filename='librotors_gazebo_motor_model.so'>
        <jointName>edrn/rotor_3_joint</jointName>
        <linkName>edrn/rotor_3</linkName>
        <turningDirection>cw</turningDirection>
        <timeConstantUp>0.0125</timeConstantUp>
        <timeConstantDown>0.0125</timeConstantDown>
        <maxRotVelocity>667</maxRotVelocity>
        <motorConstant>0.0002440724623743665</motorConstant>
        <momentConstant>0.044148079282817</momentConstant>
        <commandSubTopic>edrn/gazebo/command/motor_speed</commandSubTopic>
        <motorNumber>3</motorNumber>
        <rotorDragCoefficient>8.06428e-05</rotorDragCoefficient>
        <rollingMomentCoefficient>1e-06</rollingMomentCoefficient>
        <motorVelocityTopic>edrn/motor_vel/3</motorVelocityTopic>
        <rotorVelocitySlowdownSim>15</rotorVelocitySlowdownSim>
        <robotNamespace>/</robotNamespace>
      </plugin>
      <plugin name='arducopter_plugin' filename='libArduPilotPlugin.so'>
        <imuTopicName>/edrn/imu</imuTopicName>
        <controlTopicName>/edrn/gazebo/command/motor_speed</controlTopicName>
        <fdm_addr>127.0.0.1</fdm_addr>
        <fdm_port_in>9002</fdm_port_in>
        <fdm_port_out>9003</fdm_port_out>
        <modelXYZToAirplaneXForwardZDown>0 0 0 3.141593 0 0</modelXYZToAirplaneXForwardZDown>
        <gazeboXYZToNED>0 0 0 3.141593 0 0</gazeboXYZToNED>
        <imuName>edrn::imu_link::imu_sensor</imuName>
        <connectionTimeoutMaxCount>5</connectionTimeoutMaxCount>
        <control channel='0'>
          <type>VELOCITY</type>
          <offset>0</offset>
          <jointName>edrn::edrn/rotor_1_joint</jointName>
          <multiplier>667</multiplier>
          <controlVelocitySlowdownSim>15</controlVelocitySlowdownSim>
        </control>
        <control channel='1'>
          <type>VELOCITY</type>
          <offset>0</offset>
          <jointName>edrn::edrn/rotor_3_joint</jointName>
          <multiplier>667</multiplier>
          <controlVelocitySlowdownSim>15</controlVelocitySlowdownSim>
        </control>
        <control channel='2'>
          <type>VELOCITY</type>
          <offset>0</offset>
          <jointName>edrn::edrn/rotor_0_joint</jointName>
          <multiplier>667</multiplier>
          <controlVelocitySlowdownSim>15</controlVelocitySlowdownSim>
        </control>
        <control channel='3'>
          <type>VELOCITY</type>
          <offset>0</offset>
          <jointName>edrn::edrn/rotor_2_joint</jointName>
          <multiplier>667</multiplier>
          <controlVelocitySlowdownSim>15</controlVelocitySlowdownSim>
        </control>
        <robotNamespace>/</robotNamespace>
      </plugin>
      <static>0</static>
      <plugin name='odometry_sensor' filename='librotors_gazebo_odometry_plugin.so'>
        <linkName>edrn/odometry_sensor_link</linkName>
        <robotNamespace>edrn</robotNamespace>
        <poseTopic>pose</poseTopic>
        <velocityRelativeTopic>velocity_relative</velocityRelativeTopic>
        <poseWithCovarianceTopic>pose_with_covariance</poseWithCovarianceTopic>
        <positionTopic>position</positionTopic>
        <transformTopic>transform</transformTopic>
        <odometryTopic>odometry</odometryTopic>
        <parentFrameId>world</parentFrameId>
        <childFrameId>edrn/base_link</childFrameId>
        <measurementDivisor>20</measurementDivisor>
        <measurementDelay>0</measurementDelay>
        <unknownDelay>0.0</unknownDelay>
        <noiseNormalPosition>0.0 0.0 0.0</noiseNormalPosition>
        <noiseNormalQuaternion>0.0 0.0 0.0</noiseNormalQuaternion>
        <noiseNormalLinearVelocity>0.0 0.0 0.0</noiseNormalLinearVelocity>
        <noiseNormalAngularVelocity>0.0 0.0 0.0</noiseNormalAngularVelocity>
        <noiseUniformPosition>0.0 0.0 0.0</noiseUniformPosition>
        <noiseUniformQuaternion>0.0 0.0 0.0</noiseUniformQuaternion>
        <noiseUniformLinearVelocity>0.0 0.0 0.0</noiseUniformLinearVelocity>
        <noiseUniformAngularVelocity>0.0 0.0 0.0</noiseUniformAngularVelocity>
      </plugin>
      <pose>0 0 2 0 -0 0</pose>
    </model>
    <state world_name='default'>
      <sim_time>4546 85000000</sim_time>
      <real_time>2628 509318856</real_time>
      <wall_time>1745245919 148543586</wall_time>
      <iterations>1048497</iterations>
      <model name='OFICIAL_CIR'>
        <pose>39.3639 38.7432 0.69458 1.5708 -0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>39.3639 38.7432 0.69458 1.5708 -0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_CIR_0'>
        <pose>-20.8462 28.2488 0.707666 1.58703 -0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>-20.8462 28.2488 0.707666 1.58703 -0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_CIR_clone_0'>
        <pose>39.1424 -6.83791 0.69458 1.5708 -0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>39.1424 -6.83791 0.69458 1.5708 -0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_CORDAS'>
        <pose>22.7488 23.9037 -2.35352 1.56803 0.062397 -1.61512</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>22.7488 23.9037 -2.35352 1.56803 0.062397 -1.61512</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_CRUZ'>
        <pose>-31.3581 10.4814 0.5 1.56485 -0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>-31.3581 10.4814 0.5 1.56485 -0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_GRADE'>
        <pose>35.1912 -42.2171 0.5 1.59401 -0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>35.1912 -42.2171 0.5 1.59401 -0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_GRADE_0'>
        <pose>46.3465 -31.1323 0.5 1.56801 -0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>46.3465 -31.1323 0.5 1.56801 -0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_HEX'>
        <pose>-12.5042 46.8529 0.5 1.62289 -0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>-12.5042 46.8529 0.5 1.62289 -0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_3'>
        <pose>25.8053 40.5749 0.031951 1.58691 7.3e-05 -0.004529</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>25.8053 40.5749 0.031951 1.58691 7.3e-05 -0.004529</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_3_clone'>
        <pose>27.769 40.5651 0.031951 1.58691 7.3e-05 -0.004529</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>27.769 40.5651 0.031951 1.58691 7.3e-05 -0.004529</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_3_clone_0'>
        <pose>29.7164 40.566 0.031951 1.58691 7.3e-05 -0.004529</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>29.7164 40.566 0.031951 1.58691 7.3e-05 -0.004529</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_3_clone_1'>
        <pose>31.6937 40.5544 0.031951 1.58691 7.3e-05 -0.004529</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>31.6937 40.5544 0.031951 1.58691 7.3e-05 -0.004529</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_3_clone_2'>
        <pose>33.6531 40.5482 0.031951 1.58691 7.3e-05 -0.004529</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>33.6531 40.5482 0.031951 1.58691 7.3e-05 -0.004529</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_3_clone_3'>
        <pose>35.6106 40.534 0.031951 1.58691 7.3e-05 -0.004529</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>35.6106 40.534 0.031951 1.58691 7.3e-05 -0.004529</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_3_clone_4'>
        <pose>37.5802 40.5319 0.031951 1.58691 7.3e-05 -0.004529</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>37.5802 40.5319 0.031951 1.58691 7.3e-05 -0.004529</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2'>
        <pose>24.7567 23.4277 0.031951 1.5711 -0.016111 1.55207</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>24.7567 23.4277 0.031951 1.5711 -0.016111 1.55207</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone'>
        <pose>24.7972 25.4582 0.031951 1.5711 -0.016111 1.55207</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>24.7972 25.4582 0.031951 1.5711 -0.016111 1.55207</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone_0'>
        <pose>24.8375 27.4521 0.031951 1.5711 -0.016111 1.55207</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>24.8375 27.4521 0.031951 1.5711 -0.016111 1.55207</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone_1'>
        <pose>24.8763 29.4465 0.031951 1.5711 -0.016111 1.55207</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>24.8763 29.4465 0.031951 1.5711 -0.016111 1.55207</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone_2'>
        <pose>24.9125 31.411 0.031951 1.5711 -0.016111 1.55207</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>24.9125 31.411 0.031951 1.5711 -0.016111 1.55207</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone_3'>
        <pose>24.9407 33.4015 0.031951 1.5711 -0.016111 1.55207</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>24.9407 33.4015 0.031951 1.5711 -0.016111 1.55207</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone_4'>
        <pose>24.9804 35.3841 0.031951 1.5711 -0.016111 1.55207</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>24.9804 35.3841 0.031951 1.5711 -0.016111 1.55207</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone_5'>
        <pose>25.0105 37.3643 0.031951 1.5711 -0.016111 1.55207</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>25.0105 37.3643 0.031951 1.5711 -0.016111 1.55207</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone_6'>
        <pose>25.0404 39.366 0.162748 1.5711 -0.016111 1.55207</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>25.0404 39.366 0.162748 1.5711 -0.016111 1.55207</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_PAN_IR'>
        <pose>-36.9069 26.9183 0.5 -1.60958 -0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>-36.9069 26.9183 0.5 -1.60958 -0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_PENT'>
        <pose>-34.5033 48.7269 0.5 1.59538 -0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>-34.5033 48.7269 0.5 1.59538 -0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_QUA'>
        <pose>-5.35211 25.1348 0.715229 1.58333 -0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>-5.35211 25.1348 0.715229 1.58333 -0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_TR'>
        <pose>-8.29569 15.7628 0.5 1.51884 -0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>-8.29569 15.7628 0.5 1.51884 -0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_TRAVE_AZU'>
        <pose>7.55816 -9.96262 3.75754 -1.5708 0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>7.55816 -9.96262 3.75754 -1.5708 0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_TRAVE_PRT'>
        <pose>-29.8071 -15.1422 3.71953 -1.5708 0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>-29.8071 -15.1422 3.71953 -1.5708 0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_TRAVE_RS'>
        <pose>0.593746 -21.4448 3.64521 -1.5708 0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>0.593746 -21.4448 3.64521 -1.5708 0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='OFICIAL_TRAVE_VER'>
        <pose>38.357 -18.1989 3.66186 -1.5708 0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>38.357 -18.1989 3.66186 -1.5708 0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='QQUADRADO'>
        <pose>-35.4481 40.038 0.5 0 -0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>-35.4481 40.038 0.5 0 -0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='QQUADRADO_0'>
        <pose>16.3144 26.194 0.5 0 -0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>16.3144 26.194 0.5 0 -0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <model name='edrn'>
        <pose>39.6249 40.423 0.348992 2e-06 3e-06 -0.964836</pose>
        <scale>1 1 1</scale>
        <link name='edrn/base_link'>
          <pose>39.6249 40.423 0.348992 2e-06 3e-06 -0.964836</pose>
          <velocity>-0.001958 0.000572 0.000228 -0.001907 -0.006527 1e-06</velocity>
          <acceleration>-1.52932 0.426716 0.182155 -1.85056 1.28735 -0.520256</acceleration>
          <wrench>-13.7639 3.84044 1.63939 0 -0 0</wrench>
        </link>
        <link name='edrn/odometry_sensor_link'>
          <pose>39.6249 40.423 0.348992 2e-06 2e-06 -0.964835</pose>
          <velocity>-0.001964 0.000578 0.00023 -0.001902 -0.006402 -5.9e-05</velocity>
          <acceleration>-1.52593 0.422317 0.182013 -1.61201 1.09709 -0.669626</acceleration>
          <wrench>-0.015259 0.004223 0.00182 0 -0 0</wrench>
        </link>
        <link name='edrn/rotor_0'>
          <pose>39.5321 39.9114 0.463991 3e-06 -1e-06 0.117986</pose>
          <velocity>-0.002739 0.000797 0.000577 -0.001852 -0.006459 0.001285</velocity>
          <acceleration>-2.40511 0.651969 0.469723 1.84124 1.11445 -0.000256</acceleration>
          <wrench>-0.024051 0.00652 0.004697 0 -0 0</wrench>
        </link>
        <link name='edrn/rotor_1'>
          <pose>40.1365 40.3302 0.463992 3e-06 -0 -0.208247</pose>
          <velocity>-0.002714 0.000761 0.003715 -0.001852 -0.006508 0.001285</velocity>
          <acceleration>-2.17999 0.327119 2.98541 -0.566395 -0.423578 -0.000121</acceleration>
          <wrench>-0.0218 0.003271 0.029854 0 -0 0</wrench>
        </link>
        <link name='edrn/rotor_2'>
          <pose>39.7177 40.9347 0.463994 -5e-06 -2e-06 -2.58264</pose>
          <velocity>-0.002679 0.000786 -0.000116 -0.001852 -0.003866 0.001285</velocity>
          <acceleration>-1.85518 0.552213 -0.103263 -1.402 -1.42904 0.001614</acceleration>
          <wrench>-0.018552 0.005522 -0.001033 0 -0 0</wrench>
        </link>
        <link name='edrn/rotor_3'>
          <pose>39.1132 40.5158 0.463992 -2e-06 4e-06 -1.20009</pose>
          <velocity>-0.002703 0.000821 -0.003254 -0.001852 -0.004265 0.001285</velocity>
          <acceleration>-2.08029 0.877047 -2.619 -1.0617 -0.819359 3.13598</acceleration>
          <wrench>-0.020803 0.00877 -0.02619 0 -0 0</wrench>
        </link>
        <link name='imu_link'>
          <pose>39.6249 40.423 0.348992 2e-06 2e-06 -0.964835</pose>
          <velocity>-0.001964 0.000578 0.00023 -0.001902 -0.006403 -5.8e-05</velocity>
          <acceleration>-1.52593 0.422321 0.182014 -1.61183 1.09691 -0.669278</acceleration>
          <wrench>-0.015259 0.004223 0.00182 0 -0 0</wrench>
        </link>
      </model>
      <model name='ground_plane'>
        <pose>0 0 0 0 -0 0</pose>
        <scale>1 1 1</scale>
        <link name='link'>
          <pose>0 0 0 0 -0 0</pose>
          <velocity>0 0 0 0 -0 0</velocity>
          <acceleration>0 0 0 0 -0 0</acceleration>
          <wrench>0 0 0 0 -0 0</wrench>
        </link>
      </model>
      <light name='sun'>
        <pose>500 500 1200 0 -0 0</pose>
      </light>
      <light name='user_directional_light_0'>
        <pose>0.877343 -8.47973 1 0 -0 0</pose>
      </light>
      <light name='user_point_light_0'>
        <pose>-0.741213 -38.84 1 0 -0 0</pose>
      </light>
    </state>
    <model name='OFICIAL_CIR'>
      <pose>3.93029 0.899419 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_CIR/meshes/CIR.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_CIR/meshes/CIR.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_TRAVE_AZU'>
      <pose>12.5516 -1.63324 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_TRAVE_AZU/meshes/AZU.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_TRAVE_AZU/meshes/AZU.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_TRAVE_PRT'>
      <pose>10.3007 -1.34387 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_TRAVE_PRT/meshes/PRT.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_TRAVE_PRT/meshes/PRT.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_TRAVE_RS'>
      <pose>17.7603 -0.203752 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_TRAVE_RS/meshes/RS.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_TRAVE_RS/meshes/RS.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_TRAVE_VER'>
      <pose>24.9059 -1.66545 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_TRAVE_VER/meshes/VER.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_TRAVE_VER/meshes/VER.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <light name='user_directional_light_0' type='directional'>
      <pose>0.877343 -8.47973 1 0 -0 0</pose>
      <diffuse>0.5 0.5 0.5 1</diffuse>
      <specular>0.1 0.1 0.1 1</specular>
      <direction>0.1 0.1 -0.9</direction>
      <attenuation>
        <range>20</range>
        <constant>0.5</constant>
        <linear>0.01</linear>
        <quadratic>0.001</quadratic>
      </attenuation>
      <cast_shadows>1</cast_shadows>
      <spot>
        <inner_angle>0</inner_angle>
        <outer_angle>0</outer_angle>
        <falloff>0</falloff>
      </spot>
    </light>
    <model name='OFICIAL_GRADE'>
      <pose>15.7652 7.18518 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_GRADE/meshes/prova_SAE.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_GRADE/meshes/prova_SAE.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_GRADE_0'>
      <pose>68.8525 -30.5286 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_GRADE/meshes/grades_SAE.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_GRADE/meshes/grades_SAE.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_CIR_0'>
      <pose>-34.4477 38.4185 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_CIR/meshes/CIR.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_CIR/meshes/CIR.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='QQUADRADO'>
      <pose>-35.4481 40.038 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://NOVO_QUA/meshes/QUAA.dae</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://NOVO_QUA/meshes/QUAA.dae</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_CRUZ'>
      <pose>-29.7319 43.5594 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_CRUZ/meshes/cruz.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_CRUZ/meshes/cruz.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_HEX'>
      <pose>-35.8162 50.1259 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_HEXAGON/meshes/HEX.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_HEXAGON/meshes/HEX.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_PENT'>
      <pose>-39.3991 48.2891 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_PENT/meshes/PENT.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_PENT/meshes/PENT.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_QUA'>
      <pose>-37.5476 43.5183 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_QUA/meshes/QUA.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_QUA/meshes/QUA.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_TR'>
      <pose>-24.8257 41.2847 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_TR/meshes/TR.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_TR/meshes/TR.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_CIR_clone_0'>
      <pose>38.7752 -27.2215 0.69458 1.5708 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_CIR/meshes/CIR.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_CIR/meshes/CIR.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_PAN_IR'>
      <pose>-34.7128 36.1078 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_PAN_IR/meshes/PAN_IR.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_PAN_IR/meshes/PAN_IR.obj</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_LINHA_RETA_clone_clone_3'>
      <pose>26.8942 43.1291 0.031951 1.58691 7.3e-05 -0.004529</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2'>
      <pose>25.4892 34.4094 0.031951 1.5711 -0.016111 1.55207</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='QQUADRADO_0'>
      <pose>16.3144 26.194 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://NOVO_QUA/meshes/QUAA.dae</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://NOVO_QUA/meshes/QUAA.dae</uri>
              <scale>3 3 3</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_CORDAS'>
      <pose>37.3305 8.47905 0.5 0 -0 0</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_CORDAS/meshes/2TRAVE.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_CORDAS/meshes/2TRAVE.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <light name='user_point_light_0' type='point'>
      <pose>-0.741213 -38.84 1 0 -0 0</pose>
      <diffuse>0.5 0.5 0.5 1</diffuse>
      <specular>0.1 0.1 0.1 1</specular>
      <attenuation>
        <range>20</range>
        <constant>0.5</constant>
        <linear>0.01</linear>
        <quadratic>0.001</quadratic>
      </attenuation>
      <cast_shadows>0</cast_shadows>
      <direction>0 0 -1</direction>
    </light>
    <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone'>
      <pose>24.7972 25.4582 0.031951 1.5711 -0.016111 1.55207</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone_0'>
      <pose>24.8375 27.4521 0.031951 1.5711 -0.016111 1.55207</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone_1'>
      <pose>24.8763 29.4465 0.031951 1.5711 -0.016111 1.55207</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone_2'>
      <pose>24.9125 31.411 0.031951 1.5711 -0.016111 1.55207</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone_3'>
      <pose>24.9407 33.4015 0.031951 1.5711 -0.016111 1.55207</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone_4'>
      <pose>24.9804 35.3841 0.031951 1.5711 -0.016111 1.55207</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone_5'>
      <pose>25.0105 37.3643 0.031951 1.5711 -0.016111 1.55207</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_LINHA_RETA_clone_clone_4_clone_2_clone_6'>
      <pose>25.0404 39.3681 0.031951 1.5711 -0.016111 1.55207</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_LINHA_RETA_clone_clone_3_clone'>
      <pose>27.7917 40.5648 0.031951 1.58691 7.3e-05 -0.004529</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_LINHA_RETA_clone_clone_3_clone_0'>
      <pose>29.7164 40.566 0.031951 1.58691 7.3e-05 -0.004529</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_LINHA_RETA_clone_clone_3_clone_1'>
      <pose>31.6937 40.5544 0.031951 1.58691 7.3e-05 -0.004529</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_LINHA_RETA_clone_clone_3_clone_2'>
      <pose>33.6531 40.5482 0.031951 1.58691 7.3e-05 -0.004529</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_LINHA_RETA_clone_clone_3_clone_3'>
      <pose>35.6106 40.534 0.031951 1.58691 7.3e-05 -0.004529</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
    <model name='OFICIAL_LINHA_RETA_clone_clone_3_clone_4'>
      <pose>37.532 40.5248 0.031951 1.58691 7.3e-05 -0.004529</pose>
      <static>1</static>
      <link name='link'>
        <collision name='collision'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
          <max_contacts>10</max_contacts>
          <surface>
            <contact>
              <ode/>
            </contact>
            <bounce/>
            <friction>
              <torsional>
                <ode/>
              </torsional>
              <ode/>
            </friction>
          </surface>
        </collision>
        <visual name='visual'>
          <geometry>
            <mesh>
              <uri>model://OFICIAL_LINHA_RETA/meshes/RETO.obj</uri>
              <scale>1 1 1</scale>
            </mesh>
          </geometry>
        </visual>
        <self_collide>0</self_collide>
        <enable_wind>0</enable_wind>
        <kinematic>0</kinematic>
      </link>
    </model>
  </world>
</sdf>
