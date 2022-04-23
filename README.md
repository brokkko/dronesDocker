# dronesDocker
Docker container for launching GeoScan simulator.
Это инструкция для запуска симулятора GeoScan в IDE компании JetBrains, а также в теорминале.

Вам потребуется установить Docker. Можно установить для удобства Docker Desktop: https://www.docker.com/products/docker-desktop/.

Так же если Вам потребуется симмулятор с визуализацией от GeoScan, то нужно разархивировать программу VcXsrv(её можно найти в репозитории). 

## Запуск xLaunch
Запустить xLaunch, в третьем пункте выбрав все варианты.

![image](https://user-images.githubusercontent.com/71688733/164915371-a9c88946-47c3-47d0-ae9e-d429d57509f7.png)


## Подготовка
1. Склонировать репозиторий.
2. Запустить Docker.
3. В терминале нужно собрать образы. Для этого пропишите следующие команды:

   `docker build -t testsim -f Dockerfile_test .`
   
   `docker build -t sim .`
   
 Данные команды создадут два образа - один для запуска симмулятора с визуализацией, второй - без.

## Запуск
### Запуск с IDE
1. Необходимо настроить следующие конфигурации:

    Перейдите в раздел Edit Configurations.

    ![image](https://user-images.githubusercontent.com/71688733/164914404-3f5a4957-ee09-4a2a-9eea-07540570d49f.png)
    
    Для конфигурации runSim нужно указать правильный host path(папки cache) в разделе Bind mounts:
    
    ![image](https://user-images.githubusercontent.com/71688733/164914618-1927f3b7-6a29-4b90-ad1c-76b4f5f5c556.png)
    
    Для конфигурации runDockerTest нужно указать точно также правильный host path(папки cache), а так же IP-адрес компьютера в Вашей локальной сети, то есть в разделе Enviroment variables Вы должны записать следующее - `<Ваш IP-адрес>:0.0`:
    
    ![image](https://user-images.githubusercontent.com/71688733/164914732-81627523-dc57-44fc-8730-0e1b6aa6e23c.png)
    
2. Запустить нужную Вам конфигурацию.

### Запуск в терминале

Для симмулятора с визуализацией:

`docker run -p 57891:8000 -v <путь до папки cache>:/usr/src/app/cache --env DISPLAY=<Ваш IP-адрес>:0.0 --name testsim --rm testsim`

Для симмулятора без визуализации:

`docker run -p 57891:8000 -v <путь до папки cache>:/usr/src/app/cache --name sim --rm sim ./start.sh`

### PS
При запуске симмулятора с визуализацией нужно выбрать подключение по UDP.

При запуске нескольких контейнеров нужно указывать разные host ports.


    
    



   
   
