# projectSE2sem
ИИ-проект, ориентированный на реферирование текстов, по дисциплине "Программная инженерия".

## Состав команды:
* [Кожин Артём](https://github.com/ctakan4ik) - Тимлид, разработка функциональности приложения, описание проекта в github
* [Лихачев Денис](https://github.com/Liha4) - Разработка тестов
* [Пихтовникова Ирина](https://github.com/IraPikhtovnikova) - Разработка дизайна приложения
* [Чераева Олеся](https://github.com/rulthw) - Настройка github actions
* [Лебедева Дарья](https://github.com/dashleb33) - Развёртывание приложения в облаке

## Описание приложения
Цель данного приложения - реферирование (суммаризация) текстов. 

Данный ИИ-проект предназначен только для реферирования текстов на английском языке.


Алгоритм работы:
1. Ввод исходного текста;
2. Суммаризация текста с помощью модели API Pipeline Hugging Face - этот API позволяет пользоваться моделями для автоматического реферирования текстов;
3. Вывод полученных результатов.

   
## Ссылка на модель на Hugging Face:
[https://huggingface.co/facebook/bart-large-cnn](https://huggingface.co/facebook/bart-large-cnn)


## Пример работы приложения:
![Пример работы приложения](https://github.com/ctakan4ik/projectSE2sem/blob/main/2023-06-19-16-30-35.gif)

## Пример развертывания приложения в ранее созданной и активной виртуальной машине в Яндекс.Облаке
## Рекомендуемые ресурсы виртуальной машины:
![Рекомендуемые ресурсы виртуальной машины](https://github.com/ctakan4ik/projectSE2sem/blob/main/%D0%A0%D0%B5%D0%BA%D0%BE%D0%BC%D0%B5%D0%BD%D0%B4%D1%83%D0%B5%D0%BC%D1%8B%D0%B5%20%D1%80%D0%B5%D1%81%D1%83%D1%80%D1%81%D1%8B%20%D0%B2%D0%B8%D1%80%D1%82%D1%83%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D0%B9%20%D0%BC%D0%B0%D1%88%D0%B8%D0%BD%D1%8B.png)
## Порядок команд в терминале: 
1. Подключение к виртуальной машине - ssh dashleb@84.252.140.107, где для примера: dashleb - имя пользователя в виртуальной машине в Яндекс.Облаке, 84.252.140.107 - IP виртуальной машины
2. sudo apt install python-is-python3 - установили Python
3. pwd - можно вывести для информации рабочий каталог (результат в примере: /home/dashleb/)
4. mkdir projects - создали каталог для проектов
5. cd projects/ - перешли в каталог для проектов
6. проверить наличие Git, если нет - установить его
7. sudo apt-get upgrade - не обязательно, но можно
8. sudo apt-get update - обязательно, иначе ошибку выдаёт на следующем шаге
9. sudo apt install python3.10-venv - обязательно, иначе не будет работать установка виртуального окружения
10. mkdir /home/dashleb/python-venvs/ - создаем каталог под виртуальное окружение
11. python -m venv /home/dashleb/python-venvs/- устанавливаем виртуальное окружение
12. source /home/dashleb/python-venvs/bin/activate - активируем виртуальное окружение !!! если все хорошо, должно появиться его название в круглых скобочках - (python-venvs) - перед именем пользователя и названием виртуальной машины
13. cd /home/dashleb/projects/ - переходим в каталог с проектами
14. git clone git@github.com:ctakan4ik/projectSE2sem.git - клонируем репозиторий с приложением, которое нужно развернуть, если репозиторий собственный либо git clone https://github.com/ctakan4ik/projectSE2sem - можно по ссылке https, если не планируем репозиторий потом менять и нет прав на него, т.к. он не собственный
15. pip install -r /home/dashleb/projects/projectSE2sem/requirements.txt - устанавливаем библиотеки из файла requirements.txt
16. cd /home/dashleb/projects/projectSE2sem - перешли к нашему проекту
17. sudo apt install uvicorn - иногда требуется
18. uvicorn main:app --host=0.0.0.0 - запускаем приложение из каталога, где лежит проект (параметр --host=0.0.0.0 означает, что приложение запущено на всех портах виртуальной машины)
http://84.252.140.107:8000/summarization - по этому адресу открывается наше приложение, где 84.252.140.107 - IP виртуальной машины

Затем для того, чтобы деплой на Яндекс.Облаке работал при закрытом терминале, необходимо использовать специальные инструменты, такие как nohup или screen (https://russianblogs.com/article/35331498181/)

Nohup - это команда Unix, которая позволяет запускать процессы в фоновом режиме и сохранять их вывод в отдельном файле, который можно просмотреть позже. Для использования nohup необходимо выполнить команду в следующем формате:


nohup command > logfile 2>&1 &


где command - команда, которую нужно выполнить, logfile - файл, в который будет записываться вывод команды, 2>&1 - перенаправление стандартного вывода и вывода ошибок в файл logfile, & - запуск процесса в фоновом режиме.

Screen - это программа Unix, которая позволяет запускать процессы в отдельных виртуальных терминалах, которые можно открывать и закрывать по мере необходимости. Для использования screen необходимо выполнить команду в следующем формате:


screen -S sessionname


где sessionname - имя новой сессии. После этого можно запустить процесс внутри сессии и отключиться от нее, нажав клавиши Ctrl+A и затем D. Для повторного подключения к сессии нужно выполнить команду:


screen -r sessionname


где sessionname - имя сессии.
Таким образом, для того чтобы деплой на Яндекс.Облаке работал при закрытом терминале, можно использовать либо nohup, либо screen. 
В зависимости от конкретной ситуации и требований проекта, один из этих инструментов может оказаться более удобным и эффективным.
