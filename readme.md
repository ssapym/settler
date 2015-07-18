# Laravel Settler

The scripts that build the Laravel Homestead development environment.

# 自动构建支持Parallels Desktop版本的laravel/homestead的vagrant box
## 一，为什么要使用并自动构建开发环境
因为：

自动构建统一开发环境，避免程序员甲说：“在我这儿没事儿啊？！”这样的答复。

快速开始工作，新来的同学可以瞬间进入工作状态，并和大家同步。

持续更新环境，当大家从同一环境出发工作一段时间后，应该保持系统更新并统一。

适应不同平台，大家工作系统有所不同，应保持一定统一下的适应性。

隔离开发，大家协同工作，相互隔离，避免影响。

## 二，目标
完成构建后的系统将包括如下组件：
* Ubuntu 14.04
* PHP 5.6
* HHVM
* Nginx
* MySQL
* Postgres
* Node (With Bower, Grunt, and Gulp)
* Redis
* Memcached
* Beanstalkd
* Laravel Envoy
* Blackfire Profiler

## 三，必要组件
不重复发明轮子，站在巨人的肩膀上。
为了完成系统自动构建，使用Vagrant统一管理，虚拟机支持VBox，VMware，PD，使用Homestead做自定义配置。
前置环境准备，开始下面前请确认已经安装好如下组件：
* Vagrant
* Vagrant插件：vagrant-parallels（如果需要使用PD），vagrant-reload（如果需要构建box）
* VBox，VMware，PD其中的一个（MacOS下推荐PD）

## 四，开始
1. 构建box（如果已有box跳过）
  1. 在假定的工作目录~/work/中
  1. git clone https://github.com/ssapym/settler.git settler（我修改过的仓库，官方不支持PD）
  1. cd settler
  1. bash build.sh all（可以只构建相应box，如bash build.sh pd）
1. 添加box
  1. 在假定的工作目录~/work/中
  1. vagrant box add laravel/homestead PATH/TO/YOUR.box（box文件路径，可以试直接从别人构建好的box，也可以是第一步自己构建的box）
  1. vagrant box list 查看box
  1. 如果在第一步中构建了box，注意第一步中的中间box可以从pd中删除
1. 使用Homestead管理环境
  1. 在假定的工作目录~/work/中
  1. git clone https://github.com/laravel/homestead homestead
  1. cd homestead
  1. bash init.sh
  1. 编辑用户配置（如果需要）
  1. vagrant up

## 五，开始工作吧
构建box根据网速和配置而定，预计1小时，我的最快构建记录35分钟(包括下载所需所有文件)~~

也就是说最慢1小时投入工作状态！！！

就是这么快！收起激动的思绪，想想业务逻辑，开始干活吧！

## 六，编辑用户配置
总有时候需要自定义些配置，好吧，开始动手！

所有配置修改都在~/.homestead/Homestead.yaml文件里，配置语法简单，可参考 http://laravel.com/docs/5.1/homestead

启动后的box还会根据Homestead.yaml做些自动配置

box有4块网卡分别为


>  ==> default: Preparing network interfaces based on configuration...

>     default: Adapter 0: shared

>     default: Adapter 1: bridged

>     default: Adapter 2: hostonly

>     default: Adapter 3: hostonly  -> 这块是homestead.yaml中配置的ip所在的网卡
