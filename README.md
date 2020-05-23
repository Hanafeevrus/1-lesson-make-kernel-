## make-kernel		

edit Vagrantfile for VirtualBox Shared Folders to work		
```    
    MACHINES.each do |boxname, boxconfig|		
      #Disable shared folders		
          config.vm.synced_folder ".", "/vagrant", disabled: false		
```    
Kernel update				
We connect the repository, where we get the necessary version of the kernel.		
`sudo yum install -y http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm`		
Put the last core version:		
`sudo yum --enablerepo elrepo-kernel install kernel-ml -y`		
Updating the grub configuration:		
`sudo grub2-mkconfig -o /boot/grub2/grub.cfg`		
Select boot with the new default kernel:		
`sudo grub2-set-default 0`		
Reboot the virtual machine:		
`sudo reboot`		
	
#### assembly the kernel from the source.		
downloaded the linux-5.2.21 kernel source 		
`wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.2.21.tar.xz`		
installed the necessary components		
`yum install -y ncurses-devel make gcc bc bison flex elfutils-libelf-devel openssl-devel grub2 perl`		
Unpacked and copied the current kernel (5.3.9) to the ~ / linux-5.2.21 / .config directory		
made a configuration based on the current config (old) 5.3.9		
`make oldconfig`		
 completed assembly		
 ```
make
make modules
make install
make modules_install
```	
https://www.kernel.org/
