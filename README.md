# micro_ros_sample
## 環境セットアップ

### Arduino IDEのインストール

1. 以下のURLから1.8.19のArduino IDEをダウンロードする。  
   [https://www.arduino.cc/en/software](https://www.arduino.cc/en/software)

2. 以下の手順でインストールする。  
   ```bash
   tar xvf arduino-1.8.19-linux64.tar.xz
   mkdir -p ~/.local/
   mv arduino-1.8.19 ~/.local/
   cd ~/.local/arduino-1.8.19/
   bash arduino-linux-setup.sh $USER
   sudo reboot

   cd ~/.local/arduino-1.8.19/
   sudo bash install.sh
   ```

### OpenCRのセットアップ

1. IDEのトップメニューにある「ファイル」＞「環境設定」をクリックする。
   「追加のボードマネージャのURL」に以下のURLを貼り付ける。  
   ```bash
   https://raw.githubusercontent.com/ROBOTIS-GIT/OpenCR/master/arduino/opencr_release/package_opencr_index.json
   ```

2. 「ツール」＞「ボード」＞「ボードマネージャ」をクリックし、「OpenCR」と検索欄に入力して1.5.2をインストールする。

### micro_ros_arduinoライブラリのインストール

1. 以下URLから右上の「Code」＞「Download ZIP」からZIPをダウンロードする。  
   [https://github.com/micro-ROS/micro_ros_arduino](https://github.com/micro-ROS/micro_ros_arduino)

2. Arduino IDEを開き、「スケッチ」＞「ライブライをインクルード」＞「.ZIP形式のライブラリをインストール」をクリックする。そこでダウンロードしたZIPを選択してインストールする。

### micro_ros_setupのセットアップ

1. ワークスペースを作成し、githubからmicro_ros_setupをクローンする。  
   ```bash
   cd ~/ros2_ws/src
   git clone -b iron https://github.com/micro-ROS/micro_ros_setup.git src/micro_ros_setup
   ```

2. rosdepインストールし、ビルドする。  
   ```bash
   cd ~/ros2_ws
   rosdep update && rosdep install --from-paths src --ignore-src -y
   colcon build
   ```

3. セットアップツールを使用して、micro_ros_agentをビルドする。  
   ```bash
   ros2 run micro_ros_setup create_agent_ws.sh
   ros2 run micro_ros_setup build_agent.sh
   ```

## 前提

- コード内にROS_DOMAIN_IDを指定するため、ArduinoコードとPC側のROS_DOMAIN_IDが同じである必要がある。

## 実行手順

1. OpenCRをUSBケーブルを経由してPCに挿す。

2. PCでターミナルを起動し、micro-ROS-Agentに接続する。  
   ```bash
   ros2 run micro_ros_agent micro_ros_agent serial --dev [OpenCRのデバイス /dev/tty〇〇] -v6
   ```

## 参考
- [https://qiita.com/ousagi_sama/items/b4eb3d9c6b337cbe1b05](https://qiita.com/ousagi_sama/items/b4eb3d9c6b337cbe1b05)
- [https://zenn.dev/tasada038/articles/7192b002e6c271](https://zenn.dev/tasada038/articles/7192b002e6c271)
- [https://zenn.dev/tasada038/articles/83d78c8a8a3916](https://zenn.dev/tasada038/articles/83d78c8a8a3916)
