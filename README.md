# AMANEQ-Skeleton
AMANEQ Skeleton firmware

## Vivado version
2023.1.1

## Update submodule
You need to update the submodule (sitcp) after cloning.
The used SiTCP version is v11.0.
```
git submodule update -i
```

## Modify gig_ethernet_pcs_pma IP
On AMANEQ, the reference clock frequency for GTX is 156.25 since AMANEQ supports 10GbE.
In order to use the pcs_pma IP core for GbE, the IP setting must be changed.
After cloning the repogitory to your PC, once you need to do the procedure below.
```
[TCL console] set_param project.defaultIPCacheSetting none
[TCL console] set_property IS_MANAGED true [get_files gig_ethernet_pcs_pma.xci]
```
Once reset and generates the output products, and again set IS_MANAGED to false.
```
[TCL console] set_property IS_MANAGED false [get_files gig_ethernet_pcs_pma.xci]
```
Then, change the IP setting. Please CPLL_FBDIV_45 from 5 to 4 in gig_ethernet_pcs_pma_gtwizard_gt.vhd and change gtrefclk period from 8.000 to 6.400 in gig_ethernet_pcs_pma_ooc.xdc.
Finnaly, please update .dcp file from Design Runs. Select gig_ethernet_pcs_pma IP and click the triangle button (Launch Runs).
After updating, please check that the .dcp file date is actually updated.

![image](https://github.com/RyotaroHonda/AMANEQ-Skeleton/assets/41090607/ef80a234-1e09-4c0c-974d-42bb4d387098)
