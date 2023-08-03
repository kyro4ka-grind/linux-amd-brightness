# Linux Amd Brightness
# lenovo thinkpad t14 gen 2 Ryzen 7 5850u
# Ru
К сожалению яркость на видеоадаптерах Amd не регулируется с помощью xBacklight, а также с помощью многих других похожих утилит,
поэтому было принято решение изменять яркость непосредственно в конфиге видеоадаптера с помощью пары простых bash скриптов.

Дорогу осилит идущий:
1. Сперва необходимо понять, где располагается необходимый файл, в котором записывается значение яркости.
Как правило полный путь выглядит так: _/sys/class/backlight/Что-то свое/brightness_ .
В моем случае было так: _/sys/class/backlight/amdgpu_b10/brightness_ .
Также видел еще и так: _/sys/class/backlight/acpi_video0/brightness_ .

3. Следующим шагом необходимо предоставить пользователю(вы же не используете систему через root?:.) ) права на изменения этого
файла с помощью скриптов, поскольку по-хорошему у пользователя, по умолчанию, не должно быть доступа к его изменению:
_#sudo chmod 666 /sys/class/backlight/amdgpu_b10/brightness_
(после выполнения команды, данный файл станет доступен всем живым и не живым как rw-)

4. Превращаем скрипты из фантиков в автомат(делаем исполняемыми):
_#chmod +x ~/.scripts/brightnessUp_
_#chmod +x ~/.scripts/brightnessDown_

5. Затем нужно закинуть в удобное место 2 скрипта из репозитория (в моем случае я создал директорию ~/.scripts), запоминаем их путь.

6. Далее представлена настройка для оконного менеджера i3, вероятнее всего в других будет +- также, но это не точно.
В файл конфигурации i3 помещаем следующие 2 строчки:
_#bindsym XF86MonBrightnessUp exec --no-startup-id ~/.scripts/brightnessUp_
_#bindsym XF86MonBrightnessDown exec --no-startup-id ~/.scripts/brightnessDown_
Эти строчки позволяют системе, при нажатии клавиш прибавления/убавления яркости запускать скрипт, который и выполнит желаемое действие.

7. Вот и все, при желании можно изменить дельту изменений яркости в самих скриптах.

# En
Unfortunately, the brightness on Amd video adapters is not regulated using xBacklight as well as using many other similar utilities, so it was decided to change the brightness
directly in the video adapter config, using a couple of simple bash scripts.

The road will be mastered by the person walking:
1. First you need to understand where the necessary file is located, in which the brightness value is recorded.
As a rule, the full path looks like this: _/sys/class/backlight/Something of its own/brightness_ .
In my case it was like this: _/sys/class/backlight/amdgpu_b10/brightness_ .
I also saw it like this: _/sys/class/backlight/acpi_video0/brightness_ .

3. The next step is to grant the user (Don't you use the system through root?:.)) the rights to change this
file using scripts, because in a good way, the user, by default, should not have access to change it:
_#sudo chmod 666 /sys/class/backlight/amdgpu_b10/brightness_
(after executing the command, this file will be available to everyone alive and not alive as rw-)

4. We turn scripts from wrappers into gun (we make them executable):
_#chmod +x ~/.scripts/brightnessUp_
_#chmod +x ~/.scripts/brightnessDown_

5. Then you need to drop 2 scripts from the repository into a convenient place (in my case, I created the ~/.scripts directory), remember their path.

6. The following is the setting for the i3 window manager, most likely in others it will be +- as well, but this is not accurate.
We put the following 2 lines in the i3 configuration file:
_#bindsym XF86MonBrightnessUp exec --no-startup-id ~/.scripts/brightnessUp_
_#bindsym XF86MonBrightnessDown exec --no-startup-id ~/.scripts/brightnessDown_
These lines allow the system, when pressing the add/decrease brightness keys, to run a script that will perform the desired action.

7. That's all, if desired, you can change the delta of brightness changes in the scripts.

----------------------------------AVERAGE AMD ENJOYER----------------------------------

⣿⣿⣿⣿⣿⣿⣿⣿⡿⠿⠛⠛⠛⠋⠉⠈⠉⠉⠉⠉⠛⠻⢿⣿⣿⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣿⡿⠋⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠉⠛⢿⣿⣿⣿⣿
⣿⣿⣿⣿⡏⣀⠀⠀⠀⠀⠀⠀⠀⣀⣤⣤⣤⣄⡀⠀⠀⠀⠀⠀⠀⠀⠙⢿⣿⣿
⣿⣿⣿⢏⣴⣿⣷⠀⠀⠀⠀⠀⢾⣿⣿⣿⣿⣿⣿⡆⠀⠀⠀⠀⠀⠀⠀⠈⣿⣿
⣿⣿⣟⣾⣿⡟⠁⠀⠀⠀⠀⠀⢀⣾⣿⣿⣿⣿⣿⣷⢢⠀⠀⠀⠀⠀⠀⠀⢸⣿
⣿⣿⣿⣿⣟⠀⡴⠄⠀⠀⠀⠀⠀⠀⠙⠻⣿⣿⣿⣿⣷⣄⠀⠀⠀⠀⠀⠀⠀⣿
⣿⣿⣿⠟⠻⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠶⢴⣿⣿⣿⣿⣿⣧⠀⠀⠀⠀⠀⠀⣿
⣿⣁⡀⠀⠀⢰⢠⣦⠀⠀⠀⠀⠀⠀⠀⠀⢀⣼⣿⣿⣿⣿⣿⡄⠀⣴⣶⣿⡄⣿
⣿⡋⠀⠀⠀⠎⢸⣿⡆⠀⠀⠀⠀⠀⠀⣴⣿⣿⣿⣿⣿⣿⣿⠗⢘⣿⣟⠛⠿⣼
⣿⣿⠋⢀⡌⢰⣿⡿⢿⡀⠀⠀⠀⠀⠀⠙⠿⣿⣿⣿⣿⣿⡇⠀⢸⣿⣿⣧⢀⣼
⣿⣿⣷⢻⠄⠘⠛⠋⠛⠃⠀⠀⠀⠀⠀⢿⣧⠈⠉⠙⠛⠋⠀⠀⠀⣿⣿⣿⣿⣿
⣿⣿⣧⠀⠈⢸⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠟⠀⠀⠀⠀⢀⢃⠀⠀⢸⣿⣿⣿⣿
⣿⣿⡿⠀⠴⢗⣠⣤⣴⡶⠶⠖⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣀⡸⠀⣿⣿⣿⣿
⣿⣿⣿⡀⢠⣾⣿⠏⠀⠠⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠛⠉⠀⣿⣿⣿⣿
⣿⣿⣿⣧⠈⢹⡇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣰⣿⣿⣿⣿
⣿⣿⣿⣿⡄⠈⠃⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⣠⣴⣾⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣧⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⣠⣾⣿⣿⣿⣿⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣷⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⣴⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣿⣦⣄⣀⣀⣀⣀⠀⠀⠀⠀⠘⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⡄⠀⠀⠀⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣧⠀⠀⠀⠙⣿⣿⡟⢻⣿⣿⣿⣿⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠇⠀⠁⠀⠀⠹⣿⠃⠀⣿⣿⣿⣿⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣿⣿⣿⣿⡿⠛⣿⣿⠀⠀⠀⠀⠀⠀⠀⠀⢐⣿⣿⣿⣿⣿⣿⣿⣿⣿
⣿⣿⣿⣿⠿⠛⠉⠉⠁⠀⢻⣿⡇⠀⠀⠀⠀⠀⠀⢀⠈⣿⣿⡿⠉⠛⠛⠛⠉⠉
⣿⡿⠋⠁⠀⠀⢀⣀⣠⡴⣸⣿⣇⡄⠀⠀⠀⠀⢀⡿⠄⠙⠛⠀⣀⣠⣤⣤⠄
