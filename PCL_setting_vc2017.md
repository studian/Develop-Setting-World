#install "`PCL-1.8.1-AllInOne-msvc2017-win64.exe`"

#`Include` PATH of Visual Studio 2017

* C:\Program Files\PCL 1.8.1\include\pcl-1.8
* C:\Program Files\PCL 1.8.1\3rdParty\Boost\include\boost-1_64
* C:\Program Files\PCL 1.8.1\3rdParty\Eigen\eigen3
* C:\Program Files\PCL 1.8.1\3rdParty\FLANN\include
* C:\Program Files\PCL 1.8.1\3rdParty\Qhull\include
* C:\Program Files\PCL 1.8.1\3rdParty\VTK\include\vtk-8.0
* C:\OpenNI2\Include

#`LIB` PATH of Visual Studio 2017

* C:\Program Files\PCL 1.8.1\lib
* C:\Program Files\PCL 1.8.1\3rdParty\Boost\lib
* C:\Program Files\PCL 1.8.1\3rdParty\FLANN\lib
* C:\Program Files\PCL 1.8.1\3rdParty\Qhull\lib
* C:\Program Files\PCL 1.8.1\3rdParty\VTK\lib
* C:\OpenNI2\Lib

#Add in the `stdafx.cpp`

````````````````````````````````````````````````````````````````````
#ifdef _DEBUG
 #pragma comment(lib, "pcl_common_debug.lib")
 #pragma comment(lib, "pcl_features_debug.lib")
 #pragma comment(lib, "pcl_filters_debug.lib")
 #pragma comment(lib, "pcl_io_debug.lib")
 #pragma comment(lib, "pcl_kdtree_debug.lib")
 #pragma comment(lib, "pcl_keypoints_debug.lib")
 #pragma comment(lib, "pcl_ml_debug.lib")
 #pragma comment(lib, "pcl_octree_debug.lib")
 #pragma comment(lib, "pcl_outofcore_debug.lib")
 #pragma comment(lib, "pcl_people_debug.lib")
 #pragma comment(lib, "pcl_recognition_debug.lib")
 #pragma comment(lib, "pcl_registration_debug.lib")
 #pragma comment(lib, "pcl_sample_consensus_debug.lib")
 #pragma comment(lib, "pcl_search_debug.lib")
 #pragma comment(lib, "pcl_segmentation_debug.lib")
 #pragma comment(lib, "pcl_stereo_debug.lib")
 #pragma comment(lib, "pcl_surface_debug.lib")
 #pragma comment(lib, "pcl_tracking_debug.lib")
 #pragma comment(lib, "pcl_visualization_debug.lib")
#else
 #pragma comment(lib, "pcl_common_release.lib")
 #pragma comment(lib, "pcl_features_release.lib")
 #pragma comment(lib, "pcl_filters_release.lib")
 #pragma comment(lib, "pcl_io_ply_debug.lib")
 #pragma comment(lib, "pcl_io_ply_release.lib")
 #pragma comment(lib, "pcl_io_release.lib")
 #pragma comment(lib, "pcl_kdtree_release.lib")
 #pragma comment(lib, "pcl_keypoints_release.lib")
 #pragma comment(lib, "pcl_ml_release.lib")
 #pragma comment(lib, "pcl_octree_release.lib")
 #pragma comment(lib, "pcl_outofcore_release.lib")
 #pragma comment(lib, "pcl_people_release.lib")
 #pragma comment(lib, "pcl_recognition_release.lib")
 #pragma comment(lib, "pcl_registration_release.lib")
 #pragma comment(lib, "pcl_sample_consensus_release.lib")
 #pragma comment(lib, "pcl_search_release.lib")
 #pragma comment(lib, "pcl_segmentation_release.lib")
 #pragma comment(lib, "pcl_stereo_release.lib")
 #pragma comment(lib, "pcl_surface_release.lib")
 #pragma comment(lib, "pcl_tracking_release.lib")
 #pragma comment(lib, "pcl_visualization_release.lib")
#endif
````````````````````````````````````````````````````````````````````

#Add in the `main.cpp`

``````````````````````````````
#include <pcl/io/pcd_io.h>
#include <pcl/point_types.h>
using namespace pcl;
using namespace io;
``````````````````````````````
