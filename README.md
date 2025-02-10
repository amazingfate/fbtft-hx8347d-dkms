This package is for a tft panel [TD-TNQV24-SBT240-012](https://www.wdmomo.fun:81/doc/index.html?file=006_%E5%90%84%E7%B1%BB%E5%B1%8F%E5%B9%95/017_TD-TNQV24-SBT240-012).

To make it work a devicetree overlay is necessary. For example on orangepi3b:
```
/dts-v1/;
/plugin/;

&spi3{
        status = "okay";
        pinctrl-names = "default", "high_speed";
        pinctrl-0 = <&spi3m0_cs0 &spi3m0_pins>;
        pinctrl-1 = <&spi3m0_cs0 &spi3m0_pins_hs>;
        cs-gpios = <&gpio4 6 1>;

        hx8347d@0 {
                compatible = "himax,hx8347d";
                reg = <0>; //chip select 0:cs0  1:cs1
                spi-max-frequency = <32000000>; //spi output clock
                fps = <30>;
                bgr;
                buswidth = <8>;
                reset-gpios = <&gpio1 0 1>; //reset GPIO1 A0
                dc-gpios = <&gpio4 5 0>; //DC GPIO4 A5
    };
};
```
