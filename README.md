#How to compile ndpi-netfilter:
 
In your openwrt source dir git my tree then run make menuconfig and choose iptables-mod-ndpi and kmod-ipt-ndpithen enable support for connlabel, after that save and exit then run make download V=s it will start to donwload the source after that you can run
make package/ndpi-netfilter2/compile V=s .

#It's compile and working fine for x86 and x64 arch, but it will fail to compile for MIPS.

#TODO:

I need to make a patch for MIPS Arch.

#forum link : https://forum.lede-project.org/t/how-to-compile-vel21ripn-ndpi-netfilter2-and-using-for-lede-openwrt/10325/36
