^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Changelog for package apriltags_cpp
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

0.0.2 (2016-08-08)
------------------
* Adding libopencv-dev dependency
* Contributors: Tom Moore

0.0.1 (2016-08-08)
------------------
* Consistency with CMake variable capitalization
* Attempting to fix build issues on some machines
* Fixing issue with apriltags not actually linking against OpenCV
* Fixing installation of headers, updating cmake config
* Making package name adhere to ROS standards
* Adding CGAL dependency to package.xml and required CGAL-compatibility build flag to CMakeLists.txt
* Removing self-referential link
* catkinizing as a third-party package
* Fixed bug in CXX_FLAGS forwarding and added correct compile flags under Linux.
* frounding math should fix linux
* library linking is strange and mysterious
* refine unit parsing
* lots of getopt.h
* getopt requires unistd.h
* fixed some warnings & errors on Linux
* Initial commit
* Contributors: Matt Zucker, Pras Velagapudi, Tom Moore, mzucker
