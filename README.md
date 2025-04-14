# Неустойчивость Кельвина-Гельмгольца

## Overview

Подробное объяснение явления, результаты моделирования и прочие разъяснения в видео: https://youtu.be/Kg3NtLaF4oM

## Запуск

Приведу подробный алгоритм запуска для **Ubuntu**

### Установка OpenFOAM

Для начаала установим сам OpenFOAM

```shell
curl -s https://dl.openfoam.com/add-debian-repo.sh | sudo bash
sudo apt-get install openfoam2112-default
```

Необходимо настроить конфигурацию в `~/.bashrc`. Для этого откроем его с помощью `nano`:

```shell
nano ~/.bashrc
```

И вставим в конец:

```nano
source /usr/lib/openfoam/openfoam2112/etc/bashrc
```

### ParaView

Устанавливаем ParaView, если ещё не установлен:

```shell
sudo apt-get install paraview
```

### Запуск кода

Клонируем себе репозиторий и переходим в него:

```shell
git clone https://github.com/Vioma-tech/Kelvin-Helmholtz.git
cd Kelvin-Helmholtz/
```

Сделаем директорию `0` для OpenFOAM:

```shell
cp -r '0 .orig'/ 0
```

**Важно**: команду выше необходимо проделывать каждый раз после изменения геометрии (в том числе при изменении мелкости сетки)

Сгенерируем сетку:

```shell
blockMesh
```

 Зададим начальное распределение полей:

```shell
setFields
```

Запустим моделирование:

```shell
interFoam
```

По завершении процесса создаём `.foam` файл (можно назвать как душе угодно) и открываем его в ParaView и развлекаемся:

```shell
touch result.foam
paraview result.foam
```

Аналогичным образом запускается `damBreak-AMR` (Adaptive Mesh Refinement)
