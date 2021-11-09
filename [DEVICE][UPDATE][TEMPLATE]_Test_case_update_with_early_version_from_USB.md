| TEST CASE ID | UPD-2                                      |
| ------------ | ------------------------------------------ |
| TEST TITLE   | Update from USB-flash                      |
| TEST MODULE  | Updates                                    |
| DESCRIPTION  | Обновление через USB с более низкой версии |

| PRE-CONDITIONS | STEPS                                                  | TEST DATA                                                    |
| -------------- | ------------------------------------------------------ | ------------------------------------------------------------ |
| 1              | Открыть страницу                                       | login:                                                           pass: |
| 2              | Найти устройство по IMEI или Serial Number             | IMEI:                                                        |
| 3              | Выбрать вкладку "Информация об устройстве"             |                                                              |
| 4              | В блоке "Статистика" стоит: 1                          |                                                              |
| 5              | Подключиться к устройству посредством SSH(Port: , IP:) | login:                                                                                                      pass: |
| 6              | Дать команду                                           | mount -o remount,rw /                                        |



|  #   | STEPS                                                        | TEST DATA | EXPECTED RESULTS                                             | STATUS | BUG-ID | NOTES |
| :--: | ------------------------------------------------------------ | --------- | ------------------------------------------------------------ | ------ | ------ | ----- |
|  1   | Подключить для USB-flash специальный кабель в AUX разъем     |           | Разъем подключен                                             |        |        |       |
|  2   | Содержимое USB-flash 4 пакета для обновления в **\updates**: |           | Пакеты добавлены                                             |        |        |       |
|  3   | Открыть файл  **updater.conf ** в папке  **/mnt/data/**      |           | Файл открыт                                                  |        |        |       |
|  4   | Включить логгирование добавляя две строки:         general =                                                                                          {                                                                                                    ...                                                                                                   Log_Level = "DEBUG"                                                           Log_To_Console = true                                                                        } |           | Строки добавлены                                             |        |        |       |
|  5   | Заменить на тестовую среду изменив порт на **8001**:                    {                                                                                           Unit_Update_URL = "https://8000"        Firmware_Update_URL = "https://8000"                    test_mode = false                                                                                     } |           | {                                                                                           Unit_Update_URL = "https://8001"        Firmware_Update_URL = "https://8001"                     test_mode = false                                                                                     } |        |        |       |
|  6   | Сохранить файл **updater.conf **                             |           | Файл сохранен                                                |        |        |       |
|  7   | Открыть файл  **updater-r.conf ** в папке  **/mnt/data/**    |           | Файл открыт                                                  |        |        |       |
|  8   | Включить логгирование добавляя две строки:         general =                                                                                          {                                                                                                    ...                                                                                                   Log_Level = "DEBUG"                                                           Log_To_Console = true                                                                        } |           | Строки добавлены                                             |        |        |       |
|  9   | Заменить на тестовую среду изменив порт на **8001**:                    {                                                                                           Unit_Update_URL = "https://8000"        Firmware_Update_URL = "https://8000"                    test_mode = false                                                                                     } |           | {                                                                                           Unit_Update_URL = "https://8001"        Firmware_Update_URL = "https://8001"                     test_mode = false                                                                                     } |        |        |       |
|  10  | Сохранить файл **updater-r.conf**                            |           | Файл сохранен                                                |        |        |       |
|  11  | Вставляем USB-flash (ждем 30 секунд)                         |           | Ничего не происходит                                         |        |        |       |
|  12  | Даем команду: /data/updatesys-root.sh                        |           | Начнется обновление                                          |        |        |       |

