freq_info directory contains a [website](https://www.spectrummonitoring.com/frequencies.php) that shows cellular frequencies information all over the world.

IQ sample can be captured to a file for [LTE_DL_receiver.m](https://github.com/JiaoXianjun/LTE-Cell-Scanner/blob/master/Matlab/LTE_DL_receiver.m) to use. See [get_signal_from_sdr.m](https://github.com/JiaoXianjun/LTE-Cell-Scanner/blob/master/Matlab/get_signal_from_sdr.m) for IQ sample capture command generation.

Example:

- HackRF
```
hackrf_transfer -f 1815300000 -s 19200000 -b 20000000 -n 1728000 -l 32 -a 1 -g 50 -r tmp.bin
```

- rtlsdr
```
rtl_sdr -f 1815300000 -s 1920000 -n 172800 -g 0  tmp.bin
```

- BladeRF
```
bladeRF-cli -s bladerf.script
```
bladerf.script content:
```
set frequency rx 1815300000
set samplerate rx 19200000
set bandwidth rx 20000000
set gain rx 70
rx config file= tmp.bin format=bin n=1728000
rx start
rx wait
```

- USRP
```
uhd_rx_cfile -f 1815300000 -r 19200000 -N 1728000 -s -g 100  tmp.bin
```

Finally the tmp.bin should be renamed to a formatted file name. Then you feed the file name to LTE_DL_receiver.m as an argument. 

Example: f1815.3_s19.2_bw20_0.08s_hackrf.bin

fXXXX_sYYYY_bZZZZ_AAAAs_boardname.bin
```
XXXX: Frequency in MHz
YYYY: Sampling rate in MHz (For rtlsdr, 1.92; Others, 19.2)
ZZZZ: Bandwidth in MHz     (For rtlsdr, 1.2;  Others, 20)
AAAA: Duration in second   (At least 0.08s)
boardname: hackrf/rtlsdr/bladerf/usrp
```
