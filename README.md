# A4-VAI-Drone
## PX4 V1.14.3 
1. 모델 등록
    - PX4-Autopilot / ROMFS / px4fmu_common / init.d-posix / airframes
        - [번호]_[모델 이름] 파일 생성

    - PX4-Autopilot / ROMFS / px4fmu_common /init.d-posix / airframes /CMakeLists/txt
        - [번호]_[모델 이름]

    - PX4-Autopilot / Tools / simulation / gazebo-classic /sitl_gazebo-classic / models 
        - [모델 이름] 파일 생성
        - 파일 구조
            - [meshes]파일
                - 모델 파일
                  - \\Acsl-nas2\2025\정효주\무인이동체\gazebo 모델 혹은 nas1 무인이동체 최기영교수님 폴더에 카티아 모델 있음

            - sdf
            - sdf.jinja
            - config
                - 예시
                    
                        <?xml version="1.0"?>
                        <model>
                        <name>3DR s2000</name>
                        <version>1.0</version>
                        <sdf version='1.6'>s2000.sdf</sdf>


                        <author>  
                        <name>Lorenz Meier and Thomas Gubler</name>
                        <email>lorenz@px4.io</email>
                        </author>


                        <description>
                        This is a model of the 3DR s2000 Octocopter. The original model has been created by
                        Thomas Gubler and is maintained by Lorenz Meier.
                        </description>
                        </model>
                        
    - PX4-Autopilot / Tools / simulation / gazebo-classic / .gitignore
        - models/[모델 파일 이름]/[모델 이름.sdf]

2. 모델 환경설정
    - PX4-Autopilot / .github / workflows / sitl_tests.yml
        - iris 복붙 -> 복붙 후 모델명만 변경

    - PX4-Autopilot / Tools / simulation / gazebo-classic /sitl_gazebo-classic / .github / workflows / firmware_build_test.yml
        - model: 줄에 [자신 모델 이름] 작성

    - PX4-Autopilot / Tools / simulation / gazebo-classic / sitl_multiple_run.sh (필수 아님)
        -  SUPPORTED_MODELS=([자신 모델 이름]) 작성

    - PX4-Autopilot / launch / [자신 모델].launch (필수 아님)
        - 예시
          
                <arg name="x" default="0"/>
                <arg name="y" default="0"/>
                <arg name="z" default="0"/>
                <arg name="R" default="0"/>
                <arg name="P" default="0"/>
                <arg name="Y" default="0"/>
                <!-- vehicle model and world -->
                <arg name="est" default="ekf2"/>
                <arg name="vehicle" default="s2000"/>
                <arg name="world" default="$(find mavlink_sitl_gazebo)/worlds/empty.world"/>
                <arg name="sdf" default="$(find mavlink_sitl_gazebo)/models/$(arg vehicle)/$(arg vehicle).sdf"/>
                <env name="PX4_SIM_MODEL" value="gazebo-classic_$(arg vehicle)" />

