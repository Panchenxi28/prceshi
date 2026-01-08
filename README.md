# AlphaPlatform具身智能仿真平台

## 简介
**基于自研引擎的场景渲染、物理仿真、训练可视化一体式仿真平台**

AlphaPlatform聚焦具身智能的真实感仿真与训练，支持实时渲染、动力学求解与训练闭环的完整流程。

## 特性

#### 高质量实时渲染引擎
- 实时动态响应：支持机器人模型运动轨迹的实时可视化
- 基于物理真实渲染：基于PBR渲染技术，准确模拟光照、材质、阴影效果

#### 高精度物理仿真引擎
- 多体动力学解算：采用递归牛顿-欧拉算法与复合刚体算法，高效处理机器人系统
- 驱动与感知：支持力矩、位置、速度控制执行器系统与触觉、加速度计、陀螺仪、关节编码器等传感器


## 功能场景

#### （1）支持机器人类型：人型/四足/轮式/机械臂/灵巧手

<table align="left">
  <thead>
    <tr>
      <th>G1</th>
      <th>H1</th>
      <th>Go2w</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><img src="img/g1.png" width="240" alt="G1"></td>
      <td><img src="img/h1.png" width="240" alt="H1"></td>
      <td><img src="img/go2.png" width="240" alt="Go2w"></td>
    </tr>
  </tbody>
</table>

<table align="right">
  <thead>
    <tr>
      <th>Franka_Emika_Panda</th>
      <th>XHand</th>
      <th>R1_pro</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><img src="img/franka+panda.png" width="240" alt="Franka Panda"></td>
      <td><img src="img/xhand.png" width="240" alt="XHand"></td>
      <td><img src="img/r1_pro.png" width="240" alt="R1_pro"></td>
    </tr>
  </tbody>
</table>

#### （2）支持RGB，深度，实例分割相机数据获取
<table align="right">
  <thead>
    <tr>
      <th>RGB</th>
      <th>Depth</th>
      <th>Segmentation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><img src="img/RGB.png" width="250" alt="RGB"></td>
      <td><img src="img/depth.png" width="250" alt="Depth"></td>
      <td><img src="img/segmentation.png" width="250" alt="Seg"></td>
    </tr>
  </tbody>
</table>

#### （3）支持关节控制，碰撞检测

<table align="right">
  <thead>
    <tr>
      <th>关节控制</th>
      <th>碰撞检测</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><img src="img/机械臂.gif" width="370" alt="Joint Control"></td>
      <td><img src="img/碰撞检测.gif" width="370" alt="Collision"></td>
    </tr>
  </tbody>
</table>

#### （4）支持训练过程/结果可视化

<table align="right">
  <tbody>
    <tr>
      <td><img src="img/强化学习演示.gif" height="220" alt="强化学习演示"></td>
      <td><img src="img/pnp任务.gif" height="220" alt="pnp任务"></td>
    </tr>
  </tbody>
</table>


## 安装教程

### Building for Ubuntu24.04

需安装以下依赖：
```
sudo apt update
```
#### QT组件
```
sudo apt install qtbase5-dev libqt5svg5-dev libqt5x11extras5-dev qttools5-dev-tools qtdeclarative5-dev libzmq3-dev cppzmq-dev
```
#### GUI
```
sudo apt install libglfw3-dev libxinerama-dev libxcursor-dev libxi-dev
```
#### Vulkan
```
sudo apt install vulkan-validationlayers
```

#### Build commands:
```
mkdir build && cd build
cmake ..
cmake --build . --config=Release
```

#### 可执行文件位于: proj_root/target/bin/
```

cd ../target/bin
./alphaplatform
```

## 使用说明

### 1. 平台入口

   统一入口（推荐）：`target/bin/alphaplatform`

   说明：
   常用命令行参数：
   - `--scene=<scene.xml>` / `--config=<scene.xml>`：场景文件（支持绝对/相对路径）
   - `--kinematics=<file>`：运动/配置驱动文件（UpdateMode::Config），例如 `configs/kinematics_config/*`
   - `--model=<model.xml>`：物理模式下 AlphaPHY 模型覆盖
   - `--physics-hz=<float>`：物理仿真频率（默认 240）
   - `--endpoint=<tcp://...>`：训练流地址
   - `--num-envs=<N>`：训练并行环境数量
   - `--frame-width=<W>`：训练输出帧宽

   示例：
   ```
   ./target/bin/alphaplatform --scene=workspace/scenes/robots/bipedal_robots/g1/scene.xml
   ./target/bin/alphaplatform --scene=workspace/scenes/robots/bipedal_robots/g1/scene.xml --kinematics=configs/kinematics_config/g1
   ./target/bin/alphaplatform --scene=workspace/scenes/robots/bipedal_robots/g1/scene.xml --endpoint=tcp://127.0.0.1:6006 --num-envs=64 --frame-width=17
   ```

#####  提示：如果用了Wayland
```
export QT_QPA_PLATFORM=xcb
QT_QPA_PLATFORM=xcb ./target/bin/alphaplatform 
```
### 2.UI 使用流程：

   - 选择模式：场景 / 物理 / 训练
   - 设置场景路径，按需填写 `kinematics` 
   - 训练模式填写 endpoint/num-envs/frame-width/labels 后点击重载

## TODO List
- [x] mjcf场景描述支持
- [ ] USD场景描述支持
- [ ] 提供训练框架代码
- [ ] 高度场支持
- [ ] 完善跨平台构建运行

## 联系邮箱
如有合作交流需求，请通过以下邮箱联系我们：
- zhangheng17@iscas.ac.cn
- zhengjiashuo@iscas.ac.cn
- hewei@iscas.ac.cn
