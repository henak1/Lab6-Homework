### Лабораторная работа 6: Использование планировщика задач at

#### Предварительные требования:
- Установленный Linux или любая UNIX-подобная система.
- Основные знания работы с командной строкой.
- Возможность выполнять команды с правами администратора.

#### Введение
Данная лабораторная работа поможет изучить основы использования планировщика задач `at`, который позволяет запускать команды или скрипты в определённое время.

---

### Часть 1: Основы использования at

#### Задача
Познакомиться с базовыми возможностями `at` для планирования задач.

#### Шаги выполнения:
1. **Проверьте наличие at:**
   Убедитесь, что планировщик задач `at` установлен на вашей системе:
   ```bash
   at -V
   ```
   Если не установлен, установите его:
   ```bash
   sudo apt-get install at
   ```

2. **Запустите демон atd:**
   Убедитесь, что демон `atd` запущен:
   ```bash
   sudo systemctl start atd
   sudo systemctl enable atd
   ```

3. **Запланируйте задачу:**
   - Используйте команду `at` для запуска задачи через определённое время:
     ```bash
     echo "echo 'Hello, World!' >> ~/task_output.txt" | at now + 1 minute
     ```
   - Убедитесь, что задача запланирована:
     ```bash
     atq
     ```

4. **Просмотрите результаты выполнения:**
   После выполнения задачи проверьте содержимое файла `task_output.txt`:
   ```bash
   cat ~/task_output.txt
   ```

5. **Удалите задачу:**
   Если задача больше не нужна, удалите её из очереди:
   ```bash
   atrm <job_id>
   ```

---

### Часть 2: Расширенные возможности at

#### Задача
Использовать `at` для планирования сложных сценариев.

#### Шаги выполнения:
1. **Создайте скрипт:**
   - Напишите скрипт `backup.sh` для резервного копирования:
     ```bash
     #!/bin/bash
     tar -czf ~/backup_$(date +%F).tar.gz ~/important_data
     ```
   - Сделайте скрипт исполняемым:
     ```bash
     chmod +x backup.sh
     ```

2. **Запланируйте выполнение скрипта:**
   - Настройте выполнение через `at`:
     ```bash
     echo "~/backup.sh" | at midnight
     ```

3. **Убедитесь в выполнении:**
   Проверьте, что резервная копия создана:
   ```bash
   ls ~ | grep backup
   ```

---

### Задания

#### Задание 1
Запланируйте выполнение команды, которая создаёт текстовый файл с текущей датой и временем. Убедитесь, что задача выполняется через 5 минут после её добавления.

##### Решение:
1. Создайте файл с текущей датой и временем:
   ```bash
   echo "$(date)" > ~/date_file.txt
   ```
2. Запланируйте выполнение команды через 5 минут:
   ```bash
   echo "echo \"$(date)\" > ~/date_file.txt" | at now + 5 minutes
   ```
3. Проверьте очередь задач:
   ```bash
   atq
   ```
4. После выполнения задачи убедитесь, что файл создан:
   ```bash
   cat ~/date_file.txt
   ```

#### Задание 2
Создайте и запланируйте выполнение скрипта, который архивирует указанную папку. Убедитесь, что скрипт выполняется в определённое время.

##### Решение:
1. Напишите скрипт для архивирования папки:
   ```bash
   #!/bin/bash
   tar -czf ~/my_folder_backup_$(date +%F).tar.gz ~/my_folder
   ```
   Сохраните его как `archive.sh`.
2. Сделайте скрипт исполняемым:
   ```bash
   chmod +x archive.sh
   ```
3. Запланируйте выполнение скрипта:
   ```bash
   echo "~/archive.sh" | at 2:00 PM
   ```
4. Убедитесь, что задача добавлена:
   ```bash
   atq
   ```
5. Проверьте, что архив создан после выполнения задачи:
   ```bash
   ls ~ | grep my_folder_backup
   ```

---

### Отчёт

1. **Выполнение задания 1:**
   - Команда для планирования задачи:
     ```bash
     echo "echo \"$(date)\" > ~/date_file.txt" | at now + 5 minutes
     ```
   - Убедились, что файл создан:
     ```bash
     cat ~/date_file.txt
     ```
   Результат: файл успешно создан с текущей датой и временем.

2. **Выполнение задания 2:**
   - Создан скрипт `archive.sh`.
   - Запланирована задача выполнения скрипта:
     ```bash
     echo "~/archive.sh" | at 2:00 PM
     ```
   - Убедились, что архив создан:
     ```bash
     ls ~ | grep my_folder_backup
     ```
   Результат: архив успешно создан в указанное время.

---

### Ресурсы
- [Linux at Command Documentation](https://man7.org/linux/man-pages/man1/at.1.html)
- [Linux Systemctl Documentation](https://man7.org/linux/man-pages/man1/systemctl.1.html)
- [Bash Scripting Guide](https://www.gnu.org/software/bash/manual/bash.html)



