`�������ǧ��ȯã��ܥƥ��������漼 <http://www.tamagawa.ac.jp/engineering/ims/t_h_okada.html>`_ (RoboCup@Home ���å�����) �ǳ�ȯ����Ƥ����ư�ޥ˥ԥ�졼�� "SPUR" �� ROS �ѥå������Ǥ���

�ᥤ��Υɥ�����Ȥ� `������ <./README.rst>`_ �򻲾Ȳ������������ܸ�ɥ�����Ȥϥ��󥹥ȡ�����ˡ�Τߵ��ܤ��ޤ���

.. contents:: Table of Contents
   :depth: 3

Install
===========

���󥹥ȡ����׷�
--------------------------------

���������󥹥ȡ���ѤǤ���Ȳ��ꤷ�ޤ���

* `Ubuntu 14.04 Trusty Tahr <https://wiki.ubuntu.com/TrustyTahr/ReleaseNotes>`_ 64bit
* `ROS Indigo Igloo <http://wiki.ros.org/indigo>`_

apt �ǤΥ��󥹥ȡ��� (�侩)
--------------------------------

*__(May 9, 2015) apt �ǤΥ��󥹥ȡ���Ͽ侩�˰㤤�ʤ��ΤǤ�������������, ���������󥹥ȡ����ԤäƲ����� (omni �� joystick �Ρ��ɤ��ޤ������Τ��ᡥ���Υ����å� (https://github.com/tork-a/spur/issues/16) �����������줿�顤���������󥹥ȡ�������פˤʤ�ޤ�)��__*

�ʲ������ؤΤ���� `ROS Indigo` �� `SPUR` ROS �ѥå�����ξ���򥤥󥹥ȡ��뤹�륳�ޥ�ɤ򵭺ܤ��ޤ���
`ROS` �Υ��󥹥ȡ���ܺ٤�, `wiki <http://wiki.ros.org/indigo/Installation/Ubuntu>`_ ������������

.. code-block::

 Ubuntu$ sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu trusty main" > /etc/apt/sources.list.d/ros-latest.list'
 Ubuntu$ wget https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -O - | sudo apt-key add -
 Ubuntu$ sudo apt-get update && sudo apt-get install ros-indigo-desktop-full ros-indigo-spur
 Ubuntu$ sudo rosdep init && rosdep update
 
 Ubuntu$ echo "### For ROS setting"
 Ubuntu$ echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc
 Ubuntu$ source ~/.bashrc

���������饤�󥹥ȡ���
------------------------

���������󥹥ȡ���ϳ�ȯ��Ū�ǤΤ߿侩����ޤ���
`~/catkin_ws/` �ǥ��쥯�ȥ�˥��󥹥ȡ��뤹�뤳�Ȥ����ꤷ�Ƥ��ޤ���

1. catkin workspace �����ꤷ `SPUR` ROS �ѥå���������������.

.. code-block::

 $ mkdir -p ~/catkin_ws/src && cd ~/catkin_ws/src && catkin_init_workspace
 $ git clone https://github.com/tork-a/spur.git                             

1-1. joy stick ������ (����).

�����̰�ư��ܥå��Ѥ� ROS �� joystick �ɥ饤�ФϤޤ���ȯ���ʤ�Ǥ������ʤΤǡ��������ǥ��󥹥ȡ��뤷�ޤ� (April, 2015��`��Ϣ��������å� <https://github.com/ros-teleop/teleop_twist_joy/pull/6>`_).

.. code-block::

 $ cd ~/catkin_ws/src
 $ git clone https://github.com/130s/teleop_twist_joy.git && cd teleop_twist_joy && git checkout add/omnidir

1-2. scan_tools ������ (����).

.. code-block::

 $ cd ~/catkin_ws/src
 $ git clone https://github.com/ccny-ros-pkg/scan_tools.git && cd scan_tools && git checkout b5efb32268911cada4bf5144af3578a5561dcfef -b 20150711

2. ��¸����饤�֥��Υ��󥹥ȡ��롥����ѥ��롥

.. code-block::

 $ cd ~/catkin_ws                                                           
 $ rosdep install --from-paths src --ignore-src -r -y                       
 $ catkin_make install && source install/setup.bash                         

Usage
===========

���������ä����١�ɬ���µ���ư��������˥��ߥ�졼�����ǳ�ǧ����褦�ˤ��Ʋ�������

��֤�ư (simulation & �µ�)
------------------------------------------------

.. code-block::

 $ roslaunch spur_gazebo spur_world.launch    # Simulation
 $ roslaunch spur_bringup minimal.launch      # �µ�

�ƥ쥪�ڥ졼�����
------------------------------------------------

�ƥ쥪�ڥ졼�����joystick (Elecom PS3 ����)
###############################################################

�ʲ��� `PS3-Elecom <http://www.amazon.co.jp/ELECOM-USB%E3%82%B2%E3%83%BC%E3%83%A0%E3%83%91%E3%83%83%E3%83%89-12%E3%83%9C%E3%82%BF%E3%83%B3-%E3%83%96%E3%83%A9%E3%83%83%E3%82%AF-JC-GMU3312SPBK/dp/B003UIRIHC>`_ �ǳ�ǧ�Ѥߤμ��Ǥ���

1. joystick ��ڥ���󥰡�

* `For bluetooth-based joystick <http://wiki.ros.org/ps3joy/Tutorials/PairingJoystickAndBluetoothDongle>`_

2. joystick ROS �Ρ��ɵ�ư��

.. code-block::

 $ roslaunch spur_bringup joy_teleop.launch
 $ roslaunch spur_bringup joy_teleop.launch joy_port:=/dev/input/js1  # If joy is found on a different port

3. PS3-Elecom ��Ȥ�����ˤ�, "Mode" �ܥ������󲡤��ơ����ʥ����Ϥ�ͭ�������롥ư���Ԥ��ݤϥܥ��� 9 �򲡤�����³���롥

�����ܡ��ɤ�Ȥä��ƥ쥪�ڥ졼�����
###########################################

.. code-block::

 $ roslaunch spur_bringup kb_teleop.launch

2D ��Χ��ư
-------------------------

2D �Ͽ޺���
##############

��֤ȶ��˼��Υ����ӥ��򡤲��˼������ޥ�ɤǵ�ư���롨RViz, `gmapping <http://wiki.ros.org/gmapping?distro=indigo>`_.

.. code-block::

 term-1a$ roslaunch spur_bringup minimal.launch                            # Real robot
 term-1b$ roslaunch spur_gazebo spur_world.launch visualize_laser:=true    # Simulation
 term-2$ roslaunch spur_description rviz.launch 
 term-3$ roslaunch spur_2dnav gmapping.launch

��ư�����顤��¸���塼�ȥꥢ��򻲹ͤˤ��ƥ�ܥåȤ��ư�����Ͽޤ�������� (e.g. `one from Turtlebot <http://wiki.ros.org/turtlebot_gazebo/Tutorials/indigo/Make%20a%20map%20and%20navigate%20with%20it>`_)��

�Ͽޤ��Ѥ��Ƽ�Χ��ư���㳲����
########################################################

���Υ�ܥåȱ��Ѥκݤ˺Ǥ�褯�Ȥ����ޥ�ɤ����Τ�ʤ��Τǡ�1�ԤΥ��ޥ�ɤǼ¹ԤǤ���褦�ˤ��Ƥ���ޤ����������

 * ���ߥ�졼����󡦥⡼�ɤ� Willow Garage �Ҥ��Ͽޤ�ǥե���Ȥ��Ѥ��ޤ�
 * �µ��Ǥ� `map_file` �������꤬**ɬ��**�Ǥ�

����1�ԤΥ��ޥ�ɤ� `move_base <http://wiki.ros.org/move_base?distro=indigo>`_ ����Χ��ư��ɬ�פʥΡ��ɤ� (��֡�RViz ���Ͽ޺������˻��Ѥ����Ρ��ɷ��ȶ���) ��ư���ޤ�::

.. code-block::

 term-1-sim$ roslaunch spur_2dnav amcl.launch sim:=true
 term-1-real$ roslaunch spur_2dnav amcl.launch map_file:=%PATH_MAPFILE%

 (Ex.) 
 term-1-real$ roslaunch spur_2dnav amcl.launch map_file:=`rospack find spur_2dnav`/launch/mysweethome.yaml

(Gazebo ��) RViz ��ɽ�����줿�顤RViz ��Ǽ������Ǽ�Χ��ư�򳫻Ϥ��ޤ���

1. `2D Pose Estimate` �ܥ��� (�̾� RViz �κǾ�����ɽ������Ƥ���) ����������ܥåȤθ��߰��֤���ꤹ�롥
2. ��ܥåȤΰ��֤���ä��� `2D Nav Goal` �ܥ���򲡤�����������ֻ�������ꤹ�롥

 .. image:: https://cloud.githubusercontent.com/assets/1840401/8664520/1ad23702-298d-11e5-9a18-54d7a33fee31.png
   :width: 500 px
   :alt: 2D Pose matched b/w rviz and gazebo
   :align: left

 Image. 2D pose of the robot is matched using `2D Pose Estimate` feature on `RViz`.

����¾���ξܺ٤ϴ�¸���塼�ȥꥢ��򻲾� (e.g. `Using rviz with the Navigation Stack <http://wiki.ros.org/navigation/Tutorials/Using%20rviz%20with%20the%20Navigation%20Stack>`_).

��������ֻ�����ץ�����Ϳ��������硤`geometry_msgs/PoseWithCovarianceStamped <http://docs.ros.org/api/geometry_msgs/html/msg/PoseWithCovarianceStamped.html>`_ �ȥԥå���ȯ�Ԥ��� (�ܺ١�`this QA <http://answers.ros.org/question/9686/how-to-programatically-set-the-2d-pose-on-a-map/>`_).

���ߥ�˥ƥ�
============

* `����ե������ (�Ѹ�, ������) <http://answers.ros.org/>`_
* `����ե������ (���ܸ�) <https://groups.google.com/forum/#!forum/ros-japan-users>`_
* `������� / ��ǽ�����ꥯ������ <https://github.com/tork-a/spur/issues>`_
