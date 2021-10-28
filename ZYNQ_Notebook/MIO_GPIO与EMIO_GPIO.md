#### MIO_GPIO与EMIO_GPIO

对于控制相同的多个外设，只需要初始化这个外设一次即可（如控制多个MIO_GPIO与EMIO_GPIO只需要XGpios，Xgpios_Config*一次即可）

##### 配置步骤

###### 初始化外设

```c
XGpioPs gpiops;            //PS端 GPIO 驱动实例
XGpioPs_Config *gpiops_cfg_ptr; //PS端 GPIO 配置信息

//根据器件ID查找配置信息
gpiops_cfg_ptr = XGpioPs_LookupConfig(GPIOPS_ID);
//初始化器件驱动
XGpioPs_CfgInitialize(&gpiops, gpiops_cfg_ptr, gpiops_cfg_ptr->BaseAddr);
```

###### 配置外设

```c
//设置(EMIO)MIO_GPIO为输出（输出为1，输入为0）
XGpioPs_SetDirectionPin(&gpiops, MIO_PIN, 1);

//使能(EMIO)MIO_GPIO输出（输入不用使能）

XGpioPs_SetOutputEnablePin(&gpiops, MIO_PIN, 1);

//向PIN中写值
XGpioPs_WritePin(&gpiops, MIO_PIN, KEY_VALUE);

//从PIN中读值`

XGpioPs_ReadPin(&gpiops, MIO_PIN);
```

