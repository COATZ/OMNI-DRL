# OMNI-DRL
## Description
This repository is still in development mode. I need to perform some code and comments clean up. If you really need access to this code, message me at artizzu@i3s.unice.fr and I will answer you ASAP.

## Related Articles
OMNI-DRL: Learning to Fly in Forests with Omnidirectional Images [[1]](#1)

Deep Reinforcement Learning with Omnidirectional Images: application to UAV Navigation in Forests [[2]](#2)

## VIDEOS

[YOUTUBE](https://www.youtube.com/@coatz3943/videos)

## UE EXEC

RDMAP environment: [Google Drive](https://drive.google.com/file/d/1eXtP3qAzfYgbX9XLl9FMyo_fs0FdtO8x/view?usp=sharing)

### ADDITIONAL INFOS

"DefaultQuadrotor": {"PawnBP": "Class'/Game/Grid_425/BP/BP_FlyingPawn_1.BP_FlyingPawn_1_C'"},

0 = classic drone
1 = not visible in game drone
2 = transparent drone
3 = smaller drone (x0.1)

Airsim Request for images

Scene = 0, 
DepthPlanar = 1, 
DepthPerspective = 2,
DepthVis = 3, 
DisparityNormalized = 4,
Segmentation = 5,
SurfaceNormals = 6,
Infrared = 7,
OpticalFlow = 8,
OpticalFlowVis = 9



To get non stiched images in equi reconstruction in Unreal Engine:

PostProcessVolume->Lens->ImageEffects->VignetteIntensity->0
AutoExposure->OFF
AtmosphericFog->OFF

### Run EXEC
```
sh run_Grid_Forest_425_opengl_ip12.sh 
```


## PIP ENV
Create the pip env
```
python3 -m venv OMNI_DRL_ENV
source OMNI_DRL_ENV/bin/activate
python3 -m pip install -r requirements.txt
pip install -e .
```
   
## RUN DRL
Run
```
nohup python3 env_test/env_run.py -ip 12 &> nohup12.out &
```
Tensorboard
```
nohup tensorboard --logdir forest_drone_tensorboard/ --port=6008 > tensorboard_nohup.out 2>&1 &
```

## LUT
imode = 0: Wequi = Wcube / imode = 1: Wequi = 2 * Wcube
```
python3
import OMNI_DRL.envs.create_LUT as cLUT
cLUT.create_lookup_table(1024, './LUT', "bilinear", 0)
> Creating LookUp Table Cube 1024x1024 to Equi 1024x1024 imode 0
> (1024, 1024, 3)
cLUT.create_lookup_table(1024, './LUT', "bilinear", 1)
> Creating LookUp Table Cube 1024x1024 to Equi 2048x1024 imode 1
> (1024, 2048, 3)
```

## OFFSETS
Offset file created in OFFSETS DIR.
```
python3 policies/create_offset_tensor.py --w 100 --h 100 --k 8 --s 4 --p 0
```

## Citations
<a id="1">[1]</a> 
```
@inproceedings{artizzu:hal-03777700,
  TITLE = {{OMNI-DRL: Learning to Fly in Forests with Omnidirectional Images}},
  AUTHOR = {Artizzu, Charles-Olivier and Allibert, Guillaume and Demonceaux, C{\'e}dric},
  URL = {https://hal.archives-ouvertes.fr/hal-03777700},
  ADDRESS = {Matsumoto, Japan},
  BOOKTITLE = {13th IFAC Symposium on Robot Control (SYROCO)},
  YEAR = {2022},
  MONTH = Oct,
  KEYWORDS = {Omnidirectional sensors ; Perception and sensing ; Mobile robots and vehicles ; Learning robot control ; Deep Reinforcement Learning},
  PDF = {https://hal.archives-ouvertes.fr/hal-03777700/file/SYROCO2022.pdf},
  HAL_ID = {hal-03777700},
  HAL_VERSION = {v1},
}
```

<a id="2">[2]</a> 
```
@inproceedings{artizzu:hal-03812448,
  TITLE = {{Deep Reinforcement Learning with Omnidirectional Images: application to UAV Navigation in Forests}},
  AUTHOR = {Artizzu, Charles-Olivier and Allibert, Guillaume and Demonceaux, C{\'e}dric},
  URL = {https://hal.archives-ouvertes.fr/hal-03812448},
  BOOKTITLE = {{17th International Conference on Control, Automation, Robotics and Vision (ICARCV)}},
  ADDRESS = {Singapore, Singapore},
  YEAR = {2022},
  MONTH = Dec,
  KEYWORDS = {Vision for robots ; Mobile robotics ; Perception systems},
  PDF = {https://hal.archives-ouvertes.fr/hal-03812448/file/ICARCV_OMNI_22.pdf},
  HAL_ID = {hal-03812448},
  HAL_VERSION = {v1},
}
```
