## GDDR6/GDDR6X GPU Memory Temperature Reader for Linux

Reads GDDR6/GDDR6X VRAM memory temperatures from multiple supported NVIDIA GPUs found in a host Linux system.
These findings are based on reverse engineering of the NVIDIA GPU Linux driver.

Thanks to the greate work of "olealgoritme"!

We wanted to add the feature to send the temperature data directly via Telegraf to InfluxDB.
That we can Monitore everything on a Grafana Website.

The Idea behind this ist to combine "nvidia-smi" and "gddr6" tool to have a good Overview for AI-Traning or Mining.

![grafik](https://github.com/AImmd/gddr6/assets/135707290/dfa14d69-fc61-49d2-9ca3-ac81f738f4ee)



#Installation

## Dependencies
- libpci-dev 
```
sudo apt install libpci-dev -y
```

- Kernel boot parameter: iomem=relaxed
```
sudo vim /etc/default/grub
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash iomem=relaxed"
sudo update-grub
sudo reboot
```

## Supported GPUs
- RTX 4090 (AD102)
- RTX 4070 Ti (AD104) 
- RTX 3090 (GA102)
- RTX 3070 (GA104)
- RTX A2000 (GA106)

## Telegraf

The Configuration for the Telegraf Agent to InfluxDB has to be configred like that:
```
[[inputs.exec]]
  commands = ["/usr/local/bin/gddr6a"]
  timeout = "5s"
  data_format = "influx"
```  
