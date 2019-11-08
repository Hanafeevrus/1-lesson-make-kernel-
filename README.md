## 1-lesson-make-kernel-
## lesson 1-make kernel


   #отредактировать Vagrantfile для работы VirtualBox Shared Folders
    MACHINES.each do |boxname, boxconfig|
    # Disable shared folders
    config.vm.synced_folder ".", "/vagrant", disabled: false
    
    ##обновил ядро до последней версии согласно методичке (ради эксперимента)
    ##Подключаем репозиторий, откуда возьмем необходимую версию ядра.
  sudo yum install -y http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
    ##Ставим последнее ядро:
  sudo yum --enablerepo elrepo-kernel install kernel-ml -y
    ##Обновляем конфигурацию загрузчика:
  sudo grub2-mkconfig -o /boot/grub2/grub.cfg
    ## Выбираем загрузку с новым ядром по-умолчанию:
  sudo grub2-set-default 0
    ##Перезагружаем виртуальную машину:
  sudo reboot

    ##скачал исходник ядра linux-5.2.21 
  wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.2.21.tar.xz
    ##установил необхлдимые компоненты
  yum install -y ncurses-devel make gcc bc bison flex elfutils-libelf-devel openssl-devel grub2
    ##Распаковал и скопировал текущее ядро(5.3.9) в директорию ~/linux-5.2.21/.config
    ##выполнил конфигурацию на основе текущего конфига(old) 5.3.9
  make oldconfig
    ##выполнил сборку
  make
