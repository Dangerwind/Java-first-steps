# Гайд: Настройка окружения для Java-разработки

Этот гайд предназначен для студентов, которые начинают изучать Java и готовятся к своему первому проекту. Мы шаг за шагом разберём установку окружения и инструментов, необходимых для комфортной работы.


## 1. Какую систему выбрать

Лучший выбор для разработки — **Linux (Ubuntu)**. Она широко используется в индустрии, имеет удобный терминал и совместимость со всеми инструментами. Есть три варианта установки:

- **WSL (Windows Subsystem for Linux)** — если вы используете Windows 10/11, можно установить Ubuntu прямо внутри Windows.  
  [Как работать с Linux используя Windows](https://ru.hexlet.io/blog/posts/ubuntu-linux-in-windows)
- **Виртуальная машина (VirtualBox/VMware)** — подходит, если не хотите менять систему. [Как установить Linux используя Virtualbox](https://ru.hexlet.io/blog/posts/virtualbox)
- **Двойная загрузка** — можно установить Ubuntu параллельно с Windows.

Если вы используете **macOS** — это тоже отличный вариант. macOS, как и Linux, основана на Unix, поэтому все команды и установка будут практически одинаковыми. Отличие только в менеджере пакетов — на macOS чаще используется [Homebrew](https://brew.sh/).

Вывод: выбирайте Ubuntu (WSL/VM/dual boot) или macOS. Windows для разработки на Java не рекомендуется.


## 2. Установка Java (JDK)

Вначале вы можете ознакомиться со следующей [инструкцией](https://github.com/Hexlet/ru-instructions/blob/main/java.md) и следовать ей, либо воспользоваться описанием ниже.

Мы будем использовать **OpenJDK 21** (LTS — долгосрочная поддержка).

### Ubuntu
```bash
sudo apt update
sudo apt install openjdk-21-jdk
java -version
```

### macOS (через Homebrew)
```bash
brew install openjdk@21
java -version
```

Обратите внимание: при выполнении команд с sudo система может запросить ваш пароль. Введите его, чтобы продолжить установку.

Проверяем, что вывод показывает `openjdk version "21"`.
![Проверка java --version](https://github.com/Dangerwind/Java-first-steps/blob/main/image/01-java-version.png)


## 3. Установка Gradle
Если вы ещё не установили Gradle по этой [инструкции](https://github.com/Hexlet/ru-instructions/blob/main/java.md) то следуйте описанию ниже.

Gradle — основной инструмент сборки в проектах Hexlet.  
Важно использовать современную версию **не ниже 8.7**, так как старые версии могут не поддерживать актуальные возможности Gradle и Kotlin DSL.

### Рекомендуемый способ: SDKMAN! (Linux и macOS)
SDKMAN! позволяет легко устанавливать любую версию Gradle и переключаться между ними.

```bash
# Установка SDKMAN!
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"

# Список доступных версий Gradle
sdk list gradle

# Установка нужной версии (например, 8.7)
sdk install gradle 8.7

# Проверка версии
gradle -v
```

Если вы на macOS, этот способ работает точно так же.

![Проверка gradle --version](https://github.com/Dangerwind/Java-first-steps/blob/main/image/02-gradle-version.png)


### Альтернативный способ: официальный дистрибутив Gradle

1. Скачайте Gradle 8.7+ с официального сайта: [https://gradle.org/releases/](https://gradle.org/releases/)  
2. Распакуйте, например, в `/opt/gradle/gradle-8.7/`  
3. Добавьте в PATH:
```bash
export PATH=/opt/gradle/gradle-8.7/bin:$PATH
```
4. Проверьте:
```bash
gradle -v
```

## 4. Установка Git


Git — это инструмент для работы с репозиториями. Чтобы пользоваться им с GitHub, установите Git, настройте его, сгенерируйте SSH-ключ и добавьте его в GitHub. Подробно об этом написано [здесь](https://github.com/Hexlet/ru-instructions/blob/main/git.md).
   
Во время выполнения команд в терминале могут появляться запросы (например, на ввод пути для сохранения ключа или парольную фразу). Просто нажимайте Enter, чтобы принять значения по умолчанию.

![Генерация SSH](https://github.com/Dangerwind/Java-first-steps/blob/main/image/03-ssh-generate.png)

Для добавления ключа (`ssh-ed25519...`) в GitHub: откройте настройки вашего аккаунта GitHub (клик по аватарке в правом верхнем углу → Settings), затем перейдите в раздел “SSH and GPG keys” и нажмите “New SSH key”. Вставьте скопированный ключ в поле “Key” и сохраните.
[Полная инструкция](https://docs.github.com/ru/authentication/connecting-to-github-with-ssh).


## 5. Установка редактора (IDEA)

Мы будем использовать **IntelliJ IDEA Community Edition** — бесплатную версию от JetBrains. Это лучший редактор для Java.

- [Скачать IDEA](https://www.jetbrains.com/idea/download/) Если загрузка недоступна, можно использовать средства обхода блокировок.
- [Руководство: как работать в IntelliJ IDEA с WSL](https://www.jetbrains.com/help/idea/how-to-use-wsl-development-environment-in-product.html)

Установите и запустите IDEA. Это основное место работы.


## 6. Создание проекта

Теперь мы готовы создать первый проект на Java с помощью Gradle.

### Шаги:
1. Войдите в свой GitHub и создайте новый репозиторий (**Repositories → New**).
2. Дайте репозиторию имя, например `java-project`.
3. Склонируйте его:
   ```bash
   git clone git@github.com:username/java-project.git
   cd java-project
   ```

`username` это имя вашего аккаунта на GitHub.

4. В IntelliJ IDEA создайте новый **Gradle-проект**:
   - Название проекта: `app`
   - Location: `путь к директории, куда вы склонировали проект`
   - Build system: `Gradle`
   - JDK: `21`, (поставшик corretto, temurin, homebrew... не играет роли)
   - Gradle DSL: `Kotlin`
   - GroupId: `hexlet.code`

![IDEA new project](https://github.com/Dangerwind/Java-first-steps/blob/main/image/07-idea-start.png)

Структура проекта будет такой:
```
  ├── README.md
  └── app
      ├── build.gradle.kts
      ├── gradlew
      ├── settings.gradle.kts
      └── src
          ├── main
          │   └── java
          └── test
              └── java
```

4. Создайте пакет `hexlet.code` и класс `App`:
```java
package hexlet.code;

public class App {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

![Создание пакета](https://github.com/Dangerwind/Java-first-steps/blob/main/image/04-new-pak.png)

![Создание класса](https://github.com/Dangerwind/Java-first-steps/blob/main/image/05-new-class.png)


5. Запустите программу и убедитесь, что выводится `Hello World!`.

![Запуск и вывод в терминал](https://github.com/Dangerwind/Java-first-steps/blob/main/image/06-run-app.png)

___

## 7. Работа с зависимостями и плагинами

Для проверки обновлений в Gradle используем плагин `gradle-versions-plugin`.  
Документация: [Gradle Versions Plugin](https://github.com/ben-manes/gradle-versions-plugin).

Выполните:
```bash
./gradlew dependencyUpdates
```



## 8. Push проекта на GitHub

После изменений:
```bash
git add .
git commit -m "Init project"
git push origin main
```

Теперь ваш проект доступен на GitHub.



## 9. Типичные ошибки новичков и как их исправить

1. **Команда `java` не найдена**  
   — Проверьте, что JDK установлена и добавлена в PATH.  
   — На Ubuntu: `sudo update-alternatives --config java`.

2. **Gradle не запускается**  
   — Убедитесь, что версия не ниже 8.7 (`gradle -v`).  
   — Используйте `./gradlew`, если Gradle установлен через wrapper.

3. **GitHub не принимает push**  
   — Значит не настроен SSH-ключ. Проверьте `ssh -T git@github.com`.

4. **Проект не запускается в IDEA**  
   — Проверьте, что выбрана JDK 21: `File → Project Structure → SDK`.

5. **Ошибка в структуре проекта**  
   — Сравните с [примером проекта](https://github.com/hexlet-boilerplates/java-package).


## 10. Где искать помощь

- [Блог Hexlet](https://ru.hexlet.io/blog)  
- [Hexlet: инструкции по Java](https://github.com/Hexlet/ru-instructions/blob/main/java.md)
- [Как упростить разработку с помощью виртуализации](https://ru.hexlet.io/blog/posts/kak-uprostit-razrabotku-s-pomoschyu-virtualizatsii)
- [Документация OpenJDK](https://openjdk.org/)  
- [Документация Gradle](https://gradle.org/docs/)  

___

Теперь у вас полностью готовое окружение для работы с Java и вы можете уверенно приступать к своим учебным проектам!
