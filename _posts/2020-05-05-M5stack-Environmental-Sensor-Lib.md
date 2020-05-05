---
layout: post
title: M5stack用のBME280+CCS811ライブラリ
data: 2020-05-05
categorues: tech
tags: micom esp32 m5stack
---

## ライブラリの使い方説明

室内の温湿度気圧(bme280)と空気品質(ccs811)を取得するセンサの
M5Stack用のライブラリを作成したので使い方の説明

## M5Stack用とは

前提としてArduino IDE or Coreを利用して開発している.

Arduino Coreを使用してM5Stackの開発をしていると
\<M5Stack.h\>をincludeして開発することがほとんどだと思う．
新しめM5Stackでは内部の電源ICとの通信のために
すでにI2Cを使用しているのでそれをそのまま利用して
追加でセンサと通信するためのライブラリを作成した．

## 使い方

グローバルに宣言してsetup関数内でM5.I2Cを渡してやる．

```cpp
#include <M5Stack.h>
#include "bme280.h"
#include "ccs811.h"

BME280 bme280;
CCS811 ccs811;

void setup(){

	M5.begin();

	M5.Power.begin();

	bme280.begin(&M5.I2C);
	ccs811.begin(&M5.I2C);

	if(bme280.isConnected())
		M5.Lcd.printf("bme280: connected\n");
	else
		M5.Lcd.printf("bme280: not found\n");

	if(ccs811.isConnected())
		M5.Lcd.printf("ccs811: connected\n");
	else
		M5.Lcd.printf("ccs811: not found\n");


	delay(3 * 1000);
	M5.Lcd.clearDisplay();
	M5.Lcd.setTextSize(3);
}

void loop() {
	M5.Lcd.setCursor(0,0);
	bme280.updateSenser();
	ccs811.updateSenser();
	M5.Lcd.printf("TEMP:%4ld['C]\n HUM:%4ld[%%]\nPRES:%4ld[hPa]\n", bme280.getTemp(), bme280.getHum(), bme280.getPres());
	M5.Lcd.printf("eCO2:%4d[ppm]\ntVOC:%4d[ppb]\n", ccs811.getEco2(), ccs811.getTvoc());
	delay(1000);
}
```

[参考資料]<br>
[BME280用のライブラリ](https://github.com/link-forte/bme280_for_m5stack)<br>
[CCS811用のライブラリ](https://github.com/link-forte/ccs811_for_m5stack)
