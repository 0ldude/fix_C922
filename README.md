# fix_C922
A simple shell script to fix your Logitech c922 webcam on Linux.

Fixes horrible issues with autofocus, autoexposure, autocolor temperature, brightness, color saturation...

## Run me:
Don't do this for scripts you don't trust! (Also, why do you trust me?)


    sudo wget -O - https://raw.githubusercontent.com/0ldude/fix_C922/main/fix_C922.sh | sudo bash

## Too bright, overexposed, or underexposed?:
Use [fix_C922_bright.sh](https://github.com/mkrupczak3/fix_C922_bright.sh/blob/main/fix_C922_bright.sh) instead, it the same settings but with auto-exposure adjustment enabled

    sudo wget -O - https://raw.githubusercontent.com/0ldude/fix_C922_bright.sh/main/fix_C922_bright.sh | sudo bash

## Original Author
[mkrupczak3](https://github.com/mkrupczak3)
## More Info:
[christitus.com/logitech-c920-linux-driver](https://christitus.com/logitech-c920-linux-driver/)

## fix_C922.sh

```bash
#!/usr/bin/env bash
# 0ldudes's fix_C922.sh

# Designed for use with Logitech c922,
#     pls modify grep to work w/ others.

# Using code stolen from github.com/hoaxdream

device=$(v4l2-ctl --list-devices | grep "C922" -A 1 | grep "/dev/video." -o)

v4l2-ctl -d $device --set-ctrl=exposure_auto=1
v4l2-ctl -d $device --set-ctrl=white_balance_temperature_auto=0
v4l2-ctl -d $device --set-ctrl=exposure_absolute=300
v4l2-ctl -d $device --set-ctrl=saturation=128
v4l2-ctl -d $device --set-ctrl=contrast=128
v4l2-ctl -d $device --set-ctrl=sharpness=128
# white_balance_temperature 0x0098091a (int)    :
#     min=2000 max=6500 step=1 default=4000 value=6500
v4l2-ctl -d $device --set-ctrl=white_balance_temperature=3400

#-----------------------------------------------
#    List of ctrls for Logitech c920 webcam:
#-----------------------------------------------
#
# $ v4l2-ctl -d /dev/video0 --list-ctrls
#                      brightness 0x00980900 (int)    : min=0 max=255 step=1 default=128 value=128
#                        contrast 0x00980901 (int)    : min=0 max=255 step=1 default=128 value=128
#                      saturation 0x00980902 (int)    : min=0 max=255 step=1 default=128 value=128
#  white_balance_temperature_auto 0x0098090c (bool)   : default=1 value=0
#                            gain 0x00980913 (int)    : min=0 max=255 step=1 default=0 value=226
#            power_line_frequency 0x00980918 (menu)   : min=0 max=2 default=2 value=2
#       white_balance_temperature 0x0098091a (int)    : min=2000 max=6500 step=1 default=4000 value=3400
#                       sharpness 0x0098091b (int)    : min=0 max=255 step=1 default=128 value=128
#          backlight_compensation 0x0098091c (int)    : min=0 max=1 step=1 default=0 value=0
#                   exposure_auto 0x009a0901 (menu)   : min=0 max=3 default=3 value=1
#               exposure_absolute 0x009a0902 (int)    : min=3 max=2047 step=1 default=250 value=312
#          exposure_auto_priority 0x009a0903 (bool)   : default=0 value=1
#                    pan_absolute 0x009a0908 (int)    : min=-36000 max=36000 step=3600 default=0 value=0
#                   tilt_absolute 0x009a0909 (int)    : min=-36000 max=36000 step=3600 default=0 value=0
#                  focus_absolute 0x009a090a (int)    : min=0 max=250 step=5 default=0 value=35
#                      focus_auto 0x009a090c (bool)   : default=1 value=0
#                   zoom_absolute 0x009a090d (int)    : min=100 max=500 step=1 default=100 value=100
```
