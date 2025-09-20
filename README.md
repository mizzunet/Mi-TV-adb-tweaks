Enable ADB in Development Option

To do some settings in Android Shell you need to enable adb and download adb.exe here. (SDK Platform Tools PC/MAC)

Enable adb on the device: goto Android Settings > About > click 7 times on the Build text.

Goto Settings again > Find Development Options and enable Android Debugging.

ADB over Wifi

Find your device IP address in the network Settings.

The from the PC open a DOS window and type: adb.exe connect <deviceip>

Then type adb.exe shell

ADB with MicroUSB cable on your PC

Connect the device with a Micro USB cable with your PC.

Then type adb.exe shell

The following command sections can be copy & pasted as a block into the adb shell. After that type reboot in the shell.


Disable packages  (personal taste)

Tip: use ADB AppControl to disable/enable bloatware packages 

pm disable-user com.amazon.amazonvideo.livingroom                 #Prime Video
pm disable-user com.android.printspooler                                     #Android Printing
pm disable-user com.android.providers.calendar                           #we have no Calendar
pm disable-user com.android.providers.contacts                           #we have no contacts
pm disable-user com.google.android.music                                   #Google Music
pm disable-user com.google.android.play.games                           #Google Games
pm disable-user com.google.android.syncadapters.calendar          #we have no Calendar
pm disable-user com.google.android.syncadapters.contacts          #we have no contacts
pm disable-user com.google.android.tts                                         #Android Text to Speech, not needed
pm disable-user com.google.android.tv                                          # TV Live Channels, you might need it with Google standard Home app
pm disable-user com.google.android.tv.bugreportsender               #don't send reports
pm disable-user com.google.android.tv.remote.service                 #You might use this, I don't
pm disable-user com.google.android.videos                                  #Google Video
pm disable-user com.google.android.youtube.tv                           #Youtube, I use this
pm uninstall --user 0 android.autoinstalls.config.xioami.mibox3  #installs bloatware
#pm install-existing android.autoinstalls.config.xioami.mibox3    #installs bloatware
pm uninstall --user 0 com.miui.tv.analytics                                    #spyware
pm uninstall --user 0 com.google.android.marvin.talkback            #not used
pm uninstall --user 0 com.google.android.tvrecommendations      #spyware
pm uninstall --user 0 com.xiaomi.android.tvsetup.partnercustomizer  #installs bloatware
#pm install-existing com.xiaomi.android.tvsetup.partnercustomizer
pm uninstall --user 0 com.google.android.apps.nbu.smartconnect.tv  #installs "quicker" inet NOT
#pm install-existing com.google.android.apps.nbu.smartconnect.tv
#For feb 2021 firmware:
pm disable-user com.google.android.feedback
pm disable-user com.google.android.youtube.tvmusic
pm disable-user com.mitv.milinkservice                                       #don't if you use googleTV home
pm disable-user com.mitv.tvhome.michannel                               #don't if you use googleTV home

Note:
To enable packages: pm enable --user 0 <packagename>
To reinstall packages: pm install-existing <packagename>


Cleanup and free some space

for p in `pm list packages -d -u` ; do pm clear ${p/package:/} ; done #clear the data for every disabled package

pm trim-caches 4096G   #clear app cached data


Extra android settings (most actual are in __TV_STICK_MODS.CMD__  )

For the latest Android code look and search here: Android platform master Settings


#GLOBAL

settings put global HIC_enable 0

settings put global activity_manager_constants max_cached_processes=16,power_check_max_cpu_1=50 # dumpsys activity settings

settings put global activity_starts_logging_enabled 0

settings put global adaptive_battery_management_enabled 1 #also (force_)app_standby_enabled

settings put global adb_enabled 1

settings put global always_finish_activities 0 # Don't use 1 if you want to use Widgets in custom Launcher!!!

settings put global animator_duration_scale 0.5 #leave some animation for spinners etc

settings put global app_auto_restriction_enabled 1

settings put global app_standby_enabled 1

settings put global assisted_gps_enabled 0

settings put global job_scheduler_constants "fg_job_count=2,bg_normal_job_count=4,bg_moderate_job_count=2"

settings put global battery_saver_constants force_all_apps_standby=true,launch_boost_disabled=false,animation_disabled=true # dumpsys jobscheduler

settings put global battery_tip_constants app_restriction_enabled=true

settings put global ble_scan_always_enabled 0

settings put global ble_scan_background_mode 0 #0=low_power 1=balanced 2=low_latency 3=ambient_discovery

settings put global ble_scan_low_power_interval_ms 30000 #10240 now 30 sec, wifi/bt share antenna, after reboot goes back to 10240 (in framework res)

settings put global bluetooth_disabled_profiles 0

settings put global charging_vibration_enabled 0

settings put global connectivity_metrics_buffer_size 20000 #2000 max=10*2000

settings put global cpu_frequency_scaling_enabled 1 #only for MTK devices?

settings put global default_dns_server 1.1.1.1

settings put global default_restrict_background_data 0

settings put global development_settings_enabled 1

settings put global digital_audio_format 2 # 0=pcm 1=manual 2=auto 3=spdif

settings put global digital_audio_subformat "5,6,7,8,9,10,14,17,18,19"  #5,6,7,10 (dolby might cause problems)

settings put global drc_mode 1 #0=off 1=line 2=rf 1/2=passthrough

settings put global dropbox_age_seconds 1

settings put global dropbox_max_files 1

settings put global enable_automatic_system_server_heap_dumps 0

settings put global enable_cellular_on_boot 0

settings put global enable_diskstats_logging 0

settings put global enable_ephemeral_feature 0 # instant_apps

settings put global enable_freeform_support 0

settings put global encoded_surround_output 0 # 0=auto 1=never 2=always 3=manual (2/3 gives "not supported" box in Netflix)

settings put global encoded_surround_output_enabled_formats "5,6,7,8,9,10,14,17,18,19"  #5,6,7,10, cannot set if playing

settings put global external_surround_sound_enabled 0 # must be 0, no SPDIF

settings put global fancy_ime_animations 0

settings put global force_resizable_activities 0

settings put global forced_app_standby_enabled 1

settings put global foreground_service_starts_logging_enabled 0

settings put global fstrim_mandatory_interval 604800000


settings put global hdmi_control_enabled 0 # ENABLE IT YOURSELF AGAIN IN SETTINGS MENU

settings put global hdmi_control_auto_device_off_enabled 1

settings put global hdmi_control_auto_tv_off_enabled 1

settings put global hdmi_control_auto_wakeup_enabled 1

settings put global hdmi_system_audio_control_enabled 1

settings put global hdmi_system_audio_status_enabled 1

settings put global hdmi_control_one_touch_play_enabled 1


settings put global heads_up_notifications_enabled 0

settings put global keep_profile_in_background 0 # also always finish activities 1

settings put global location_background_throttle_interval_ms 3600000 #600000 600x1000ms

settings put global mhl_input_switching_enabled 0 # only for TV with HDMI port, not stick

settings put global mhl_power_charge_enabled 0 # only for TV with HDMI port, not stick

settings put global mobile_data 0

settings put global mobile_data_always_on 0

settings put global netstats_enabled 1 # bandwidth monitoring, some apps need this

settings put global netstats_poll_interval 3600000 #def 30min 30*60*1000

settings put global network_avoid_bad_wifi 0

settings put global network_metered_multipath_preference 2 #(0 or 3) 1=handover 2=reliable 4=performance (5ghz) 3=1+2

settings put global network_recommendations_enabled -1  #-1=forced off 0=disabled 1=enabled

settings put global network_scoring_ui_enabled 0 #wifi_badging_thresholds

settings put global nrdp_external_surround_sound_enabled 0 #must be 0, no SPDIF

settings put global nsd_on 1

settings put global ntp_server pool.ntp.org

settings put global ntp_timeout 60000 #def 5000, longer for network time

settings put global ota_disable_automatic_update 1 #system updates won't be automatically scheduled

settings put global private_dns_mode opportunistic # off / opportunistic / hostname(not for captive portal wifi connection)

settings put global private_dns_specifier dns.adguard.com

settings put global send_action_app_error 0 #not is secure

settings put global shortcut_manager_constants icon_quality=80

settings put global show_temperature_warning 1

settings put global swap_enabled 1

settings put global sys_free_storage_log_interval 1440 # 1 day

settings put global sys_storage_cache_max_bytes 262144 #256MB App cache

settings put global sys_storage_cache_percentage 5 #256MB from 5GB data partition

settings put global sys_traced 0

settings put global sysui_powerui_enabled 1

settings put global system_fonts_name "Android Font" #dunno what other font is installed

settings put global tcp_default_init_rwnd 20 #60, kernel 4-20 MAJOR network speedup!

settings put global transition_animation_scale 0.0

settings put global unused_static_shared_lib_min_cache_period 300000 #2h 15min is 15*60*1000=900000 5m=300000

settings put global usb_mass_storage_enabled 0

settings put global use_external_surround_sound_flag 0 #must be 0, no SPDIF

settings put global user_experience_enabled 0

settings put global user_switcher_enabled 0

settings put global warning_temperature 95 # is throttling down temp, cutoff is 120

settings put global webview_multiprocess 0 #1 might speed up but maybe crash

settings put global wifi_badging_thresholds "10:1000,20:2000,30:5000,40:10000,50:20000"

settings put global wifi_country_code GB #Country and Channels here. 2 letter country codes here.

settings put global wifi_coverage_extend_feature_enabled 0

settings put global wifi_display_on 1 ### enable MIRACAST too !!! ### Windows 10 doesn't seem to work, My Xiaomi phone does

settings put global wifi_enhanced_auto_join 0

settings put global wifi_ephemeral_out_of_range_timeout_ms 60000 #60*1000 1min

settings put global wifi_framework_scan_interval_ms 0 # 5*60*1000 5min 0=don't scan when connected, we are stationary/screen on!

settings put global wifi_frequency_band 0 #0=auto 1=5 2=2.4

settings put global wifi_max_dhcp_retry_count 99 #0

settings put global wifi_networks_available_notification_on 0 #alert for open wifi networks

settings put global wifi_poor_connection_warning 0

settings put global wifi_scan_always_enabled 0

settings put global wifi_scan_throttle_enabled 0

settings put global wifi_score_params "rssi2=-95:-85:-73:-60,rssi5=-85:-82:-70:-57" #,nud=0,horizon=5

settings put global wifi_sleep_policy 2 # 0=def 1=never while plugged 2=never sleep

settings put global wifi_suspend_optimizations_enabled 0

settings put global wifi_supplicant_scan_interval_ms 3000 #15000 15sec search while connected for connect, roaming or open network, screen on, not wakeup scan

settings put global wifi_verbose_logging_enabled 1 #the cure for Wifi 5Ghz dropouts, more info in Wifi settings like RSSI and SCORE (0-60)

settings put global wifi_wakeup_available 0 #doesn't show, enable wifi at location

settings put global wifi_wakeup_enabled 0

settings put global wifi_watchdog_on 1 # needed for connection?

settings put global wifi_watchdog_poor_network_test_enabled 0 #still used?
settings put global window_animation_scale 0.0

settings put global zram_enabled 1


#support_netflix 1 #for remote button or dolby?

#remote_netflix_key_state_xm ??

#settings put global tv_device_sleep_time "" #string 300000 ms

#settings put global mitv_enter_str 1 #int

#individual_privacy_enabled 1

#service_region us

#hw_rc_type NULL

#mitv.user.settingTimezone 

#device_tv_mode_settings 1 #1/2 RetailMode



#SYSTEM

settings put system advanced_settings 1 #google settings

settings put system auto_caps 0

settings put system auto_punctuate 0

settings put system auto_replace 0

settings put system bluetooth_discoverability 1 # 2=always 1=only connect 0=off, improve wifi!

settings put system bluetooth_discoverable_timeout 60

settings put system dk_desktop_pip -1 #-1  0...-1 how many PiP? what is dk?

settings put system dk_log_level 0

settings put system font_scale 1.0

settings put system haptic_feedback_enabled 0

settings put system notification_light_pulse 0

settings put system pointer_speed 4 # -7 (0) +7

settings put system screen_off_timeout 300000 #900000=15 min, time to screensaver/dreams

settings put system show_touches 1

settings put system sound_effects_enabled 1

settings put system support_dolby 1  #also in /sys/class/amaudio/dolby_enable

settings put system time_12_24 24

settings put system user_log_enabled 0

settings put system vibrate_input_devices 0

settings put system volume_bluetooth_sco 15

settings put system volume_music_bt_a2dp 15

settings put system volume_music_hdmi 15

settings put system volume_system 12
settings put system volume_voice 12

#settings put system tv_device_sleep_timer_key 1 #int min 60000

#panel_display_time 365378 #usage time

#tvapp_one_touch_play 1

#soundbar_upgrade_flag_progress / soundbar_upgrade_flag_broken_time / soundbar_upgrade_flag_current_version / soundbar_upgrade_flag_expected_version


#SECURE

#settings put secure gb_boosting 1 #??????

#settings put secure maintenance_window "0400-0600"

settings put secure automatic_storage_manager_enabled 0 #can clear app cache for you

settings put secure automatic_storage_manager_days_to_retain 3650 #(90d) 10y don't touch my files, only cache

settings put secure backup_enabled 0

settings put secure bluetooth_name "Mi TV Stick"

settings put secure camera_gesture_disabled 1

settings put secure clock_seconds 0

settings put secure double_tap_to_wake 0

settings put secure doze_enabled 0

settings put secure immersive_mode_confirmations 0

settings put secure instant_apps_enabled 0

settings put secure location_mode 0 #no gps, AndrTV 0=off 1=on/gpsonly 2=on/nogps 3=on/high accuracy

settings put secure location_providers_allowed -gps,-wifi,-network #(gps,network)AndrTV, test wifi, but it is already in network in Andr9

settings put secure long_press_timeout 500

settings put secure mount_ums_autostart 0 # mount usb mass storage doesn't work

settings put secure mount_ums_notify_enabled 1

settings put secure multi_press_timeout 400

settings put secure night_display_activated 0

settings put secure night_display_auto_mode 0

settings put secure parental_control_enabled 0

settings put secure show_ime_with_hard_keyboard 1

settings put secure sleep_timeout 3600000 # 1 hour auto off

settings put secure spell_checker_enabled 0

settings put secure system_navigation_keys_enabled 1 #n.a. for TV stick

settings put secure sysui_do_not_disturb 1 #volume down=not disturb (no notification/alarm sounds etc)

#(only if persist.sys.ui.hw]: [true]? force use gpu for 2d)

settings put secure sysui_hwui_edge_bleed 0

settings put secure sysui_hwui_rounded_divider 0

settings put secure sysui_volume_down_silent 1

settings put secure sysui_volume_up_silent 1

settings put secure theme_mode 1 #0=auto 1=light 2=dark

settings put secure upload_debug_log_pref 0

settings put secure upload_log_pref 0

settings put secure usb_audio_automatic_routing_disabled 1

settings put secure wake_gesture_enabled 0


#allow_oaid_used 1 #what is OAID?


TIP: Enable GPU rendering in Development Settings. It works good for me. (getprop persist.sys.ui.hw  should read true)


Disable background tasks


Some apps keep running in the background. We have little RAM. Less running activities is better.

For getting all possible "autorun" activities you can type: pm query-receivers --components -a android.intent.action.BOOT_COMPLETED

Note: we need root to disable Autoruns, but we can minimize backround processes

To see the actual running apps and processes type: ps -A|grep "\."

To see what have been running on the device type: dumpsys cpuinfo

Or to see live RAM usage: dumpsys meminfo


Rule of thumb: use appops command to disable all your installed apps, including preinstalled Netflix and Amazon etc.

For example if you don't use Amazon or Netflix then disable the package!!! See previous "disable packages".

#appops reset # reset all appops

appops set com.mobdro.android RUN_IN_BACKGROUND ignore

appops set com.mobdro.android RUN_ANY_IN_BACKGROUND ignore

appops set com.lgi.ziggotv RUN_IN_BACKGROUND ignore

appops set com.lgi.ziggotv RUN_ANY_IN_BACKGROUND ignore

appops set com.estrongs.android.pop RUN_IN_BACKGROUND ignore

appops set com.estrongs.android.pop RUN_ANY_IN_BACKGROUND ignore

appops set com.estrongs.android.pop CHANGE_WIFI_STATE allow

appops set tunein.player RUN_IN_BACKGROUND ignore

appops set tunein.player RUN_ANY_IN_BACKGROUND ignore

appops set radiotime.player RUN_IN_BACKGROUND ignore

appops set radiotime.player RUN_ANY_IN_BACKGROUND ignore

appops set ar.tvplayer.tv RUN_IN_BACKGROUND ignore

appops set ar.tvplayer.tv RUN_ANY_IN_BACKGROUND ignore

appops set com.netflix.ninja RUN_IN_BACKGROUND ignore

appops set com.netflix.ninja RUN_ANY_IN_BACKGROUND ignore

appops set org.xbmc.kodi RUN_IN_BACKGROUND ignore

appops set org.xbmc.kodi RUN_ANY_IN_BACKGROUND ignore

#appops set com.google.android.katniss RUN_IN_BACKGROUND ignore

#appops set com.google.android.tungsten.setupwraith RUN_IN_BACKGROUND ignore #e.g. screensaver

#appops set mitv.service RUN_IN_BACKGROUND ignore #is Miracast

...

...

appops write-settings

appops query-op RUN_IN_BACKGROUND ignore

appops query-op RUN_ANY_IN_BACKGROUND ignore


Text input on screen

When in ADB shell use this command: input text "....."


Get current temperature

logcat -d|grep -i temp

12-05 23:28:04.991  3015  3015 I ThermalHAL: current temperature:71.000000, throttling_threshold:95.000000, shutdown_threshold:120.000000


Some trivial commands


pm trim-caches 4096G

svc data disable

svc wifi enable

cmd shortcut reset-all-throttling

cmd netpolicy list wifi-networks #list saved wifi networks

dumpsys activity settings

dumpsys wifi |grep -i speed:   #get current wifi connection speed

dumpsys jobscheduler #get jobscheduler Settings and BackgroundJobsController

ps -ef  # list all processes


A good Internet Browser with Tabs and Ad Block is TV-BRO

A good keyboard is LeanKeyKeyboard.


Use another launcher


Install any launcher (here ATVlauncher pro) and disable default Android TV launcher

Or better use newer use Wolf Launcher (based on ATV Launcher Pro, can be downloaded here on XDA, use CCGTV version, kudos to SweenWolf)

First disable the default Android TV Launcher:  pm disable-user com.google.android.tvlauncher 

Now press the HOME button on the remote and select your new Home Launcher.

Also use widgets in a Home Launcher? New launcher needs permissions:   appwidget grantbind --package ca.dstudio.atvlauncher.pro

ps: In fact you can set any activity as your Home Launcher. 

cmd package set-home-activity ca.dstudio.atvlauncher.free/ca.dstudio.atvlauncher.screens.launcher.LauncherActivity

cmd shortcut get-default-launcher 


Create an app backup and restore (WIP)


adb shell

bmgr enabled          (is it enabled? )

bmgr enable true     (if not enabled yet does settings put secure backup_enabled 1)

Selecting the right transport (backup location)

bmgr list transports    (show all available transports)

    android/com.android.internal.backup.LocalTransport

    com.google.android.gms/.backup.migrate.service.D2dTransport

  * com.google.android.gms/.backup.BackupTransportService

Example to set transport to local:

bmgr transport android/com.android.internal.backup.LocalTransport  

Selected transport android/com.android.internal.backup.LocalTransport (formerly com.google.android.gms/.backup.BackupTransportService)

Note: This is the /cache/backup/<token>/_full/<packagename> (Environment.getDownloadCacheDirectory())

-rw------- 1 system system 1186816 2021-01-19 00:09 com.feedr

bmgr list transports

  * android/com.android.internal.backup.LocalTransport                     (/cache/backup)

    com.google.android.gms/.backup.migrate.service.D2dTransport

    com.google.android.gms/.backup.BackupTransportService             (Google Drive)

bmgr list sets      (show all devices with your google account, or local disk if transport is local)

  1 : Local disk image

or with gms BackupTransportService you see your devices in the cloud (google drive)

 ...ea593 : Redmi Note 8 Pro

 ...28418 : Xiaomi Redmi 4X

 ...ad91b : cm84

 ...86d68 : Asus Memo Pad HD7

 ...76576 : Samsung...

Do the backup

For the best backup use the fullbackup option! For example launchers will have widgets restored too.

bmgr fullbackup com.wolf.firelauncher

bmgr run                    (run any pending operations now)

dumpsys backup        (check for Pending key/value backup)

Do the restore

dumpsys backup|grep Current       (show current TOKEN)

Current:   1

bmgr restore 1 com.wolf.firelauncher

Scheduling restore: Local disk image

restoreStarting: 1 packages

onUpdate: 0 = com.wolf.firelauncher

restoreFinished: 0

done

bmgr run       (run any pending operations now)

Check backups and other info

dumpsys backup

...

Ever backed up: 7

    com.android.providers.settings

    android

    com.wolf.firelauncher

    com.android.vending

    com.google.android.inputmethod.latin

    com.android.providers.userdictionary

    com.estrongs.android.pop

...

Note:  https://developer.android.com/guide/topics/data/testingbackup

Lot of OOM due to low RAM

logcat -d|grep lowmemorykiller

12-11 13:16:41.952  3019  3019 I lowmemorykiller:    to free 53468kB because system is under medium memory pressure oom_adj 800

12-11 13:16:41.994  3019  3019 I lowmemorykiller: Killing 'com.google.process.gservices' (12336), uid 10017, adj 902

12-11 13:16:41.994  3019  3019 I lowmemorykiller:    to free 47396kB because system is under medium memory pressure oom_adj 800

12-11 13:16:42.023  3019  3019 I lowmemorykiller: Killing 'com.google.android.katniss:interactor' (13357), uid 10014, adj 900

12-11 13:16:42.023  3019  3019 I lowmemorykiller:    to free 65296kB because system is under medium memory pressure oom_adj 800

12-11 13:16:46.054  3019  3019 I lowmemorykiller: Killing 'com.google.android.gms' (13480), uid 10017, adj 800

12-11 13:16:46.054  3019  3019 I lowmemorykiller:    to free 108376kB because system is under medium memory pressure oom_adj 800

12-11 13:17:42.172  3019  3019 I lowmemorykiller: Killing 'com.google.android.gms' (13568), uid 10017, adj 900

12-11 13:17:42.172  3019  3019 I lowmemorykiller:    to free 108936kB because system is under medium memory pressure oom_adj 800

12-11 13:17:53.418  3019  3019 I lowmemorykiller: Killing 'com.google.process.gservices' (13513), uid 10017, adj 900

12-11 13:17:53.418  3019  3019 I lowmemorykiller:    to free 61484kB because system is under medium memory pressure oom_adj 800

12-11 13:17:53.529  3019  3019 I lowmemorykiller: Killing 'com.google.android.katniss:search' (13315), uid 10014, adj 800

12-11 13:17:53.529  3019  3019 I lowmemorykiller:    to free 82376kB because system is under medium memory pressure oom_adj 800


aquaman:/ $ free -m


                total        used        free      shared     buffers

Mem:              981         961          19           0           1

-/+ buffers/cache:            960          20

Swap:             511         199         312


aquaman:/ $ dumpsys activity settings 


ACTIVITY MANAGER SETTINGS activity_manager_constants:


  max_cached_processes=16

  background_settle_time=60000

  fgservice_min_shown_time=2000

  fgservice_min_report_time=3000

  fgservice_screen_on_before_time=1000

  fgservice_screen_on_after_time=5000

  content_provider_retain_time=20000

  gc_timeout=5000

  gc_min_interval=60000

  full_pss_min_interval=1200000

  full_pss_lowered_interval=300000

  power_check_interval=300000

  power_check_max_cpu_1=50

  power_check_max_cpu_2=25

  power_check_max_cpu_3=10

  power_check_max_cpu_4=2

  service_usage_interaction_time=1800000

  usage_stats_interaction_interval=7200000

  service_restart_duration=1000

  service_reset_run_duration=60000

  service_restart_duration_factor=4

  service_min_restart_time_between=10000

  service_max_inactivity=1800000

  service_bg_start_timeout=15000

  CUR_MAX_CACHED_PROCESSES=16

  CUR_MAX_EMPTY_PROCESSES=8

  CUR_TRIM_EMPTY_PROCESSES=4

  CUR_TRIM_CACHED_PROCESSES=2

ScrCpy: Tool for remote control


This opensource tool called ScrCpy makes it possible to remote control your Android device using PC/Mac and keyboard and mouse.

Also you can drag and drop (non APK) files onto it that will be placed in the /sdcard folder. When you drop an APK file it will be installed.

Download from github

More info on how to use it for example here: https://fossbytes.com/mirror-android-phone-to-pc-windows-macos/
