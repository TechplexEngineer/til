Update system time and the hardware RTC clock
=============================================



## Update system time
```
ntpdate -u time.nist.gov
```

## Write system time to hardware clock
```
hwclock --systohc --localtime
```

[Ref](https://www.vultr.com/docs/setup-timezone-and-ntp-on-centos-6)
