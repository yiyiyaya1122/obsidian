
```cpp
/*
 * @brief: 检测模式
 */
enum class Mode
{
	IDLE = 0,               //!< 空闲模式
	DETECT_PALLET = 1,      //!< 托盘检测
	DETECT_SPACE = 2,       //!< 空间检测
	DETECT_VAN = 3,         //!< 箱式货车检测 + 装车位姿检测
	DETECT_GOODS_SERVO = 4, //!< 伺服取货检测模式
	DETECT_SPACE_SERVO = 5, //!< 伺服放货检测模式
	DETECT_GOODS_STATES = 6,//!< 货物在货叉上的位姿检测
	DETECT_VAN_UNLOAD = 7,  //!< 箱式货车检测 + 卸车货物检测
	DETECT_STACK_SERVO = 8, //!< 货位伺服检测
	DETECT_STACK_ALIGNMENT_SERVO = 9,//!< 货位伺服检测
	DETECT_STACK_CONFIRM = 15,//!< 堆垛确认检测
	DETECT_GROUND = 99,     //!< 地面检测
	DETECT_CALIBRATION = 100,//!< 标定模式
	DETECT_LIDAR_CAMERA_CALIBRATION = 101,//!< 雷达相机标定模式
	DETECT_CALIBRATION_VERIFY = 102//!< 激光标定验证模式
};

/*!
 * @brief 任务模式参数
 */
struct ModeParam
{
    float servo_completed_dist; //! 伺服停止距离，小于该距离完成伺服
    float detect_roi_width;     //! 检测区域宽度
    float detect_roi_length;    //! 检测区域长度
    float detect_roi_height;    //! 检测区域高度
    int is_line_search;         //! 是否线库搜索模式，0表示普通取放，1表示线库搜索取放
};

struct CheckResult
{
	CheckResultInterface	    result;
	ServoResult				    servo_goal;
	ServoResult				    servo_goal_loc;
	OdometryMSG				    odom_sensor;
	uint32_t				    error_code;			//感知模块异常状态 
};

struct CheckResultInterface
{
    Pose3dFloat goal;            /* 载具前端中心相对于AGV中心的位置 */
    Pose3dFloat location_goal;   /* 定位目标点 */
    Pose3dFloat goodsOffset;     /* 货物在货叉上位姿偏移量，货柜车会用 */
    ERRORCODE_old state;         /* 叉臂感知模块状态 */
    PackageInfo packageInfo;     /* 货物信息 */
    float max_err;               /* 取货余度 */
    int32_t valid_frame;         /* 有效帧数标志位 */
    int64 sensor_timestamp;      /* 时间 */
};


// AGV parameters
struct AGV_Params 
{ 
	AGVType agvType; //AGV类型 
	float ForkLength; //货叉长度 
	float LoadPositionX; //货叉根部到定位轮的距离 
	float ForkDistance; //货叉间距 
	float ForkWidth; //货叉宽度 
	float ForkThickness; //货叉厚度 
	float DefaultAxialLength; //默认轴长 
	float WheelBase; //轮距 
	float SteeringWheelOffset; //偏置舵轮偏置量 
	float MaxForwardVelocity; //车体最大前进速度 
	float MaxBackwardVelocity; //车体最大后退速度 
	int AGVContourSize; // 
	point2D* AGVContour; //车体包络框 
};

// AGV Message
struct AGV_MSG 
{
	int64_t msg_time; //时间 
	Pose3dFloat ideal_pose; //目标位姿
	Pose3dFloat putOffset; //放货计算偏移量
	Pose3dFloat goodsOffset; //货物在货叉上位姿偏移量
	int card_key; //卡板编号
	int detect_type; //检测类型
	int alignment_mode; //放货对齐方式
};

// Sensor Data
struct SensorData 
{ 
	// 线程 
	std::thread* data_thread; 
	std::atomic_bool pause_preprocess; // 暂停标志 
	std::atomic_bool stop_preprocess; // 停止标志 
	SensorDataPackage latest_package; // 最新一帧数据包 
	LidarCloudPtr dense_cloud; // 叉尖防拥稠密点云 
	std::atomic_int frame_num; // 点云帧数 
	std::atomic_int update_fps; // 点云更新频率 
	std::mutex data_mutex; // 点云数据锁 
	std::vector<LidarCloudPtr> offline_clouds; // 离线数据点云 
	std::mutex offline_data_mutex; // 离线数据锁 
	int frame_index; // 数据帧索引 
	std::atomic_bool synchronization; // 同步 
	Offline_io offline_io; // 离线数据接口 
	std::string log_path; // 日志路径 
	std::atomic_bool recorde_state; // 录制状态 
	std::atomic<ROI> roi; // 感兴趣区域 
	std::mutex offline_io_mutex; // 离线数据锁 
	std::atomic<std::chrono::system_clock::time_point> last_recorde_time ={std::chrono::system_clock::now()}; // 录制时间 
	std::atomic<int> recorde_timegap; // 录制间隔（ms） 
};

//Sensor Data Package
struct SensorDataPackage 
{ 
	LidarCloudPtr cloud = std::make_shared<VN_Driver::LidarCloud>(); 
	CameraImagePtr image = std::make_shared<VN_Driver::CameraImage>(); 
	OdometryMSG odom{{0.0f, 0.0f, 0.0f, 0.0f, 0.0f, 0.0f}, {0.0f, 0.0f, 0.0f, 0.0f, 0.0f, 0.0f}, 0.0f, 0, 0}; 
}; 


struct OdometryMSG
{
	Pose3d			agv_pose;
	ForkPose		fork_pose;
	double			stamp;
	uint32_t		seq_num;
	uint32_t		first_num;
};


struct ForkPose
{
	float x;						/*!< x 方向平移 */
	float y;						/*!< y 方向平移 */
	float z;						/*!< z 方向平移 */
	float roll;					/*!< 绕 x 方向旋转 */
	float pitch;					/*!< 绕 y 方向旋转 */
	float yaw;					/*!< 绕 z 方向旋转 */
	float c;						/*!< 夹抱 */
};

struct LidarInfo 
{ 
	int pointsNum = 0; 
	uint64_t zapTime = 0; 
};


struct MinMaxXYZ
{
	float min_x;
	float max_x;
	float min_y;
	float max_y;
	float min_z;
	float max_z;
};

struct Params 
{ 
	int n_size; /* < 结构体大小*/
	int n_type; /* < 结构体类型枚举，VNPE_DATA_RUNNING_PARAMS*/
	std::vector<CardInfo> cards; 
	std::vector<SensorInfo> sensors; 
	DefaultCalibParams calib_params;
	HardwareInfo hardware; 
	CommonConfig config; 
	SensorPoolConfig pool; 
	DetectPalletParams pallet; 
	DetectHoleParams pallet_hole; 
	DetectPalletYoloParams pallet_yolo; 
	DetectVanParams van; 
	DetectSpaceParams space; 
	DetectLineParams line; 
	DetectMaterialCageParams cage; 
	DetectCageStackParams cage_stack; 
	DetectCageStackOccParams cage_stack_occ;
	DetectCageStackICPParams cage_stack_icp; 
	CageStackConfirmParams cage_stack_confirm; 
	DetectLimitedPostParams limited_post; 
	DetectWrapPalletParams wrap_pallet; 
	BackWardSafetyParams back_safety; 
	SafetyParams safety; 
	CalibrationParams calibration; 
	std::map<int, std::map<std::string, std::vector<cv::Point2f>>> channels;
	std::vector<DefaultAGVParams> agv_params; 
	ServoConfigParams servo; 
	OtherFunctionParams others; 
	BeVanParams be_van; 
};

struct DetectMaterialCageParams
{
    ExpandROI e_roi;

    float split_width;
    float ransac_dist_thresh;
    int vertical_line_min_size;
    float mat_max_dz;

    float tolerance;
    int cluster_min_size;
    float z_bias_thresh;

    int horizontal_line_min_points_size;
    float horizontal_line_min_length_scale;
    float horizontal_line_min_points_dist;

    float tolerance_cage_width;     // 料笼宽度容忍值（整数 单位: m）
    float min_points_per_cm;        // 密度过滤，单位cm高度的体素内的点数（浮点数）
    float nms_threshold;            // 非极大值抑制的阈值，越接近1表示提取近似的立柱越少（0-1）
    float min_column_gap;           // 立柱最小间隔（浮点数 单位: m）
    float min_column_height;        // 立柱最小高度（浮点数 单位: m）
    float column_y_edge;            // 立柱点云提取左右余量，即y方向余量（浮点数 单位: m）
    float column_x_thres;           // 立柱点云提取前后阈值，即x方向阈值（浮点数 单位: m）
    float point2plane_dist;         // 立柱拟合平面时，点到平面的最大距离阈值（浮点数 单位: m）
    float max_plane_angle;          // 立柱拟合平面时，平面的最大角度阈值（浮点数 单位: °）
    float max_agv_angle;            // 料笼检测要求的最低的agv角度范围
};

struct DefaultCalibParams
{
	std::vector<CardInfo>       calib_cards;
	std::vector<Coordinate3D>	init_extrinsic;
	std::vector<Coordinate3D>	room_init_extrinsic;
	int                         calib_method_type;
};

struct coordinate3D
{
    float x;  //!< x 方向平移
    float y;  //!< y 方向平移
    float z;  //!< z 方向平移
    float roll;  //!< 绕 x 方向旋转
    float pitch;  //!< 绕 y 方向旋转
    float yaw;  //!< 绕 z 方向旋转
};


struct SensorInfo
{
    int n_size;  //! 结构体大小
    int n_type;  //! 结构体类型枚举值，VNPE_DATA_SENSOR_INFO
    int serial_number;
    std::string ip;
    std::string broadcast;
    int port;
    std::vector<float> intrinsic_matrix;
    std::vector<float> extrinsic_matrix;
    Coordinate3D extrinsic;
    Coordinate3D extrinsic_ecal2perception;
    std::vector<float> distortion_coeffs;
    std::string other_info;
    CommetState comnet_state;
    SensorType sensor_type;
    SensorSite sensor_site;
    float grounding_fork_height;
    bool car_lidar_fix;
    bool car_lidar_transverse_fix;
    int intergrate_time;
    int patch_num;
    SensorName sensor_name;
};

struct SensorData {
    std::thread* data_thread;  // 线程
    std::atomic_bool pause_preprocess;  // 暂停标志
    std::atomic_bool stop_preprocess;  // 停止标志
    SensorDataPackage latest_package;  // 最新一帧数据包
    LidarCloudPtr dense_cloud;  // 叉尖防护稠密点云
    std::atomic_int frame_num;  // 点云帧数
    std::atomic_int update_fps;  // 点云更新频率
    std::mutex data_mutex;  // 点云数据锁
    std::vector<LidarCloudPtr> offline_clouds;  // 离线数据点云
    std::mutex offline_data_mutex;  // 离线数据锁
    int frame_index;  // 数据帧索引
    std::atomic_bool synchronization;  // 同步
    Offline_io offline_io;  // 离线数据接口
    std::string log_path;  // 日志路径
    std::atomic_bool recorde_state;  // 录制状态
    std::atomic<ROI> roi;  
    std::mutex offline_io_mutex;  // 离线数据锁
    std::atomic<std::chrono::system_clock::time_point> last_recorde_time = { std::chrono::system_clock::now() };  // 录制时间
    std::atomic<int> recorde_timegap;  // 录制间隔（ms）
};


struct TakeGoodsStruct
{
    std::string current_state = "";
    std::string error_code = "";
    std::string ideal_card = "";
    std::string detect_card = "";
    std::string detect_type = "";
    std::string roi = "";
    std::string roi_points_num = "";
    std::string pier_num = "";
    std::string pier_width = "";
    std::string pier_height = "";
    std::string hole_width = "";
    std::string card_pier_width = "";
    std::string card_pier_height = "";
    std::string card_hole_width = "";
    std::string ideal_pose = "";
    std::string detect_pose = "";
    std::string fork_thickness = "";
    std::string algorithm_time = "";
    std::string frame_count = "";
    std::string points_num = "";
    std::string load_state = "";
    std::string reserve_distance = "";
    std::string goods_detect_time = "";
    std::string goods_size = "";
    std::string goods_overplate = "";
};

struct ExpandROI
{
	float expand_x;
	float expand_y;
	float expand_z;
};

struct XYZ
{
	float x;
	float y;
	float z;
};


/*!
 * @brief: 检测返回数据:接口用
 */
struct CheckResultInterface
{
    Pose3dFloat goal;            /* <载具前端中心相对于AGV中心的位置 */
    Pose3dFloat location_goal;   /* 定位目标点 */
    Pose3dFloat goodsOffset;     /* <货物在货叉上位姿偏移量，货柜车会用 */
    ERRORCODE_old state;         /* <叉臂感知模块状态 */
    PackageInfo packageInfo;     /* <货物信息 */
    float max_err;               /* <取货余度 */
    int32_t valid_frame;         /* <有效帧标志位 */
    int64 sensor_timestamp;      /* <时间 */
};


```

  

  

编辑

分享

解释一下代码中每个变量的作用。

这段代码是如何处理图像数据的？

如何调用这个函数来实现点云到图像的转换？



```