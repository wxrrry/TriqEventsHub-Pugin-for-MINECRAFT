# Инструкции по сборке TRIQ Events Hub

## Требования для сборки

- Java 17 или выше
- Maven 3.6 или выше
- Git (для клонирования репозитория)

## Установка Maven

### Windows
1. Скачайте Maven с официального сайта: https://maven.apache.org/download.cgi
2. Распакуйте архив в папку (например, `C:\Program Files\Apache\maven`)
3. Добавьте путь к Maven в переменную PATH:
   - Откройте "Система" → "Дополнительные параметры системы" → "Переменные среды"
   - В разделе "Переменные среды пользователя" найдите PATH
   - Добавьте путь к папке `bin` Maven (например, `C:\Program Files\Apache\maven\bin`)

### Linux/macOS
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install maven

# CentOS/RHEL
sudo yum install maven

# macOS (с Homebrew)
brew install maven
```

## Сборка проекта

1. **Клонируйте репозиторий** (если еще не сделали):
   ```bash
   git clone https://github.com/your-repo/triq-events-hub.git
   cd triq-events-hub
   ```

2. **Проверьте версию Java**:
   ```bash
   java -version
   ```
   Убедитесь, что версия Java 17 или выше.

3. **Проверьте версию Maven**:
   ```bash
   mvn -version
   ```

4. **Соберите проект**:
   ```bash
   mvn clean package
   ```

5. **Найдите готовый JAR файл**:
   После успешной сборки JAR файл будет находиться в папке `target/triq-events-hub-1.0.0.jar`

## Установка на сервер

1. **Скопируйте JAR файл** в папку `plugins/` вашего Minecraft сервера
2. **Перезапустите сервер**
3. **Настройте конфигурацию** в файле `plugins/TRIQEventsHub/config.yml`

## Альтернативные способы сборки

### Сборка без Maven (если Maven недоступен)

Если у вас нет Maven, вы можете:

1. **Использовать IDE** (IntelliJ IDEA, Eclipse, VS Code):
   - Откройте проект в IDE
   - Настройте Maven в IDE
   - Используйте встроенные инструменты сборки

2. **Скачать готовый JAR** (если доступен):
   - Проверьте релизы на GitHub
   - Скачайте готовый JAR файл

### Сборка в Docker

Создайте `Dockerfile`:
```dockerfile
FROM maven:3.8-openjdk-17 AS build
WORKDIR /app
COPY . .
RUN mvn clean package

FROM openjdk:17-jre-slim
COPY --from=build /app/target/triq-events-hub-1.0.0.jar /app/plugin.jar
```

Соберите образ:
```bash
docker build -t triq-events-hub .
```

## Устранение проблем

### Ошибка "mvn не найден"
- Убедитесь, что Maven установлен и добавлен в PATH
- Перезапустите командную строку после установки Maven

### Ошибки компиляции
- Проверьте версию Java (должна быть 17+)
- Убедитесь, что все зависимости доступны
- Проверьте синтаксис Java кода

### Ошибки при запуске на сервере
- Убедитесь, что используется Paper/Spigot 1.20.4
- Проверьте логи сервера на наличие ошибок
- Убедитесь, что конфигурация корректна

## Структура проекта после сборки

```
triq-events-hub/
├── target/
│   └── triq-events-hub-1.0.0.jar    # Готовый плагин
├── src/
│   └── main/
│       ├── java/                     # Исходный код
│       └── resources/                # Ресурсы
├── pom.xml                          # Конфигурация Maven
├── README.md                        # Документация
└── BUILD.md                         # Этот файл
```

## Контакты

Если у вас возникли проблемы со сборкой, создайте issue в репозитории проекта.
