# homeassistant-Custom_UI_more-info-qinver-tv
homeassistant电视遥控器的自定义详情页。Homeassistant TV remote custom details page.
> homeassistant接入电视之后，能操作的功能不多，但是我们往往又接入了遥控器的全部功能，比如通过博联或者小米红外等。  
但是基于ha的操作方式，几乎不能当遥控器用！ 你想想，每一个按键都是一个开关，操作是很困难的！  
当然可以使用一些其他的自定义ui，但是都不方便，因为我认为遥控器使用最多的还是在手机上，而手机上的操作只有触控和滑动才是最方便的！  
因为这样才能一边看电视一边盲操作！  
所以，我制作了这样的一个UI，可以实现触控滑动来控制你的电视！  
## 目录  
*[更新记录](#更新记录) 
*[功能介绍](#功能介绍和截图)  
*[安装](#安装以开始使用)  
*[配置文件](#编写配置文件)  
*[混合使用](#与其他自定义UI一起使用)  
*[与我联系](#与我联系和反馈)  
## 更新记录  
2018年6月12日
> 首次发布，如有疑问，欢迎与我联系！
## 功能介绍和截图
```  
你可以在任何一个卡片上使用此自定义电视详情页，当点击卡片之后就会弹出这个遥控器UI  
1. 通过触摸滑动控制遥控器上下左右/返回/主页的功能  
2. 可以增加你需要的其他按钮
3. 可以与其他的自定义卡片UI一起使用
4. 当然你也不一定非要用于电视遥控器，其他用法自行研究
```
![]()   
![]()   

## 安装以开始使用  
1. 下载[more-info-qinver-tv.html]()文件放入到你homeassistant配置文件目录的`~~/www/custom_ui`文件夹下  
如图所示：  
![]()  
2. 在homeassistant配置文件`configuration.yaml`中的对因位置加入以下代码  
``` yaml
frontend:
  javascript_version: auto
  extra_html_url:
    - /local/custom_ui/more-info-qinver-tv.html
  extra_html_url_es5:
    - /local/custom_ui/more-info-qinver-tv.html  
```  
**就这么简单两部，你就可以开始使用了！**  
## 编写配置文件
### 同样的我写了一个示例:  
里面包含了两个例子，也有详细的注释，你可以下载此文件，放入到你homeassistant配置文件目录的`~~/packages`文件夹下  
如果你之前从未使用过packages文件夹，那么请在配置文件`configuration.yaml`中加入以下代码:  
``` yaml
homeassistant:
  packages: !include_dir_named packages 
```
### 全部配置文件内容  
``` yaml 
  customize:
    input_boolean.boolean_tvceshi1:       #假设这是我的电视开关ID
      friendly_name: 电视遥控器1
      icon: mdi:television-guide
      custom_ui_more_info: more-info-qinver-tv   ##使用此自定义详情页面
      entities:               #以下是触控滑动功能的ID
        menu: script.bl_cmcc_hezi_menu
        home: script.bl_cmcc_hezi_home
        back: script.bl_cmcc_hezi_back
        up: script.bl_cmcc_hezi_shang
        down: script.bl_cmcc_hezi_xia
        left: script.bl_cmcc_hezi_zuo
        right: script.bl_cmcc_hezi_you
        ok: script.bl_cmcc_hezi_ok
        buttons:             #除了触控区，你还需要增加的按钮。请一起填写icon
          - entity: input_boolean.boolean_tvceshi1
            icon: mdi:skip-previous-circle-outline
          - entity: input_boolean.boolean_tvceshi2
            icon: mdi:skip-next-circle-outline
          - entity: input_boolean.boolean_tvceshi3
            icon: mdi:format-list-bulleted
          - entity: input_boolean.boolean_tvceshi4
            icon: mdi:backup-restore
   ```
   ## 与其他自定义UI一起使用
   这个项目是自定义详情页，也就是点击卡片弹出来的页面，那么它可以与其他任何自定义卡片UI一起使用！  
   `以下是一个与我之前制作的[state-card-button](https://github.com/Qinver-china/homeassistant-Custom_UI.state-card-button)（自定义按钮卡片）一起使用的例子：
``` yaml
  customize:
    input_boolean.boolean_tvceshi2:
      friendly_name: 电视遥控器2
      icon: mdi:television-guide
      custom_ui_state_card: state-card-button    #这里使用自定义卡片UI，也可以使用其他的
      config:
        gap: 10px                   # 间距（默认为8px）
        ha_entity_toggle_display: none    # 不显示右边本来的按钮（默认显示）
        entities:
          - entity: script.bl_cmcc_hezi_home               #这是我的home按钮
            icon: mdi:home-outline                         #只要一个图标,其它都默认
          - entity: script.bl_cmcc_hezi_voljian            #音量-
            icon: mdi:volume-minus
          - entity: script.bl_cmcc_hezi_voljia             #音量+ 
            icon: mdi:volume-plus
          - entity: script.bl_cmcc_hezi_kaiguan            #电源开关按钮
            icon: mdi:power
            color_off: '#E45E65'                           #电源按钮我把他设为红色
##上面配置为自定义按钮卡片ui，详情请看项目
##下面开始遥控器UI配置，同示例一
      custom_ui_more_info: more-info-qinver-tv   ##使用此自定义详情页面
      entities:               #以下是触控滑动功能的ID
        menu: script.bl_cmcc_hezi_menu
        home: script.bl_cmcc_hezi_home
        back: script.bl_cmcc_hezi_back
        up: script.bl_cmcc_hezi_shang
        down: script.bl_cmcc_hezi_xia
        left: script.bl_cmcc_hezi_zuo
        right: script.bl_cmcc_hezi_you
        ok: script.bl_cmcc_hezi_ok
        buttons:             #除了触控区，你还需要增加的按钮。请一起填写icon
          - entity: input_boolean.boolean_tvceshi1
            icon: mdi:skip-previous-circle-outline
          - entity: input_boolean.boolean_tvceshi2
            icon: mdi:skip-next-circle-outline
          - entity: input_boolean.boolean_tvceshi3
            icon: mdi:format-list-bulleted
          - entity: input_boolean.boolean_tvceshi4
            icon: mdi:backup-restore 
  ```
  









