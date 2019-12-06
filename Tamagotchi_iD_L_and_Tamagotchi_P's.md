# Things we know

## Tamagotchi Specs

|                 |                                               |
| --------------- | --------------------------------------------- |
| CPU             | Epson, Romless?                               |
| Instruction Set | S1C33?                                        |
| Clock Rate      | **Unknown**                                   |
| ROM             | 64Mb Macronix flash rom, (likely no internal) |
| P's Figure      | SPI (Unknown protocol, likely SPI flash)      |

## Tamagotchi P's Deco Pierce Pinout (facing user)

|     |      |     |
| --- | ---- | --- |
| SDO | SCLK | SDI |
| Vcc | CS   | Gnd |

## Flash rom part number

<code>

` MX29LV320DTTI-70G`
` --: Macronix`
`   ----: 3V Parallel flash`
`       ---: 32Mb`
`          -: 0.13um`
`           -: Top Boot`
`            -: TSOP`
`             -: Industrial`
`               --: 70ns`
`                 -: RoHS`

</code>

## Tamagotchi debug port pinout (top down)

|      |      |      |      |      |      |     |      |
| ---- | ---- | ---- | ---- | ---- | ---- | --- | ---- |
| 1    | 2    | 3    | 4    | 5    | 6    | 7   | 8    |
| dst0 | dst1 | dcpo | dsio | dst2 | dclk | Gnd | Bat+ |

## External links

[S1C33 Instruction
set](http://www.epsondevice.com/webapp/docs_ic/DownloadServlet?id=ID001580)