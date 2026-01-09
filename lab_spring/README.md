# Lab — REST Spring web app 

## Реализованная функциональность

### 1. CRUD операции для задач
- **GET /api/tasks** - получение списка всех задач
- **GET /api/tasks/{id}** - получение задачи по ID
- **POST /api/tasks** - создание новой задачи
- **PUT /api/tasks/{id}** - обновление задачи
- **DELETE /api/tasks/{id}** - удаление задачи

### 2. Безопасность
- Spring Security с Basic Authentication
- Защита всех API endpoints (кроме H2 консоли)
- In-memory аутентификация пользователя
- BCrypt кодирование паролей

### 3. База данных
- H2 in-memory база данных
- JPA/Hibernate для работы с данными
- Автоматическое создание схемы БД
- H2 консоль для просмотра данных

### 4. Обработка ошибок
- Кастомное исключение `ResourceNotFoundException`
- Автоматическая обработка HTTP 404 для несуществующих ресурсов

## Установка и запуск

### Требования
- Java 17 или выше
- Maven 3.6+
- Node.js и npm (для E2E тестов)

### Запуск приложения

1. Клонируйте репозиторий и перейдите в директорию проекта:
```bash
cd lab_spring
```

2. Соберите проект с помощью Maven:
```bash
mvn clean install
```

3. Запустите приложение:
```bash
mvn spring-boot:run
```

Или запустите JAR файл:
```bash
java -jar target/task-management-system-0.0.1-SNAPSHOT.jar
```

4. Приложение будет доступно по адресу: http://localhost:8080

### Доступ к H2 консоли

1. Откройте браузер и перейдите по адресу: http://localhost:8080/h2-console
2. Используйте следующие параметры подключения:
   - **JDBC URL**: `jdbc:h2:mem:taskdb`
   - **Username**: `sa`
   - **Password**: `password`

## API Endpoints

### Аутентификация
Все API endpoints требуют Basic Authentication:
- **Username**: `admin`
- **Password**: `admin123`

### Задачи

#### Получить все задачи
```http
GET /api/tasks
Authorization: Basic YWRtaW46YWRtaW4xMjM=
```

#### Получить задачу по ID
```http
GET /api/tasks/{id}
Authorization: Basic YWRtaW46YWRtaW4xMjM=
```

#### Создать новую задачу
```http
POST /api/tasks
Authorization: Basic YWRtaW46YWRtaW4xMjM=
Content-Type: application/json

{
  "title": "Новая задача",
  "description": "Описание задачи",
  "status": "Pending"
}
```

#### Обновить задачу
```http
PUT /api/tasks/{id}
Authorization: Basic YWRtaW46YWRtaW4xMjM=
Content-Type: application/json

{
  "title": "Обновленная задача",
  "description": "Новое описание",
  "status": "In Progress"
}
```

#### Удалить задачу
```http
DELETE /api/tasks/{id}
Authorization: Basic YWRtaW46YWRtaW4xMjM=
```

## Примеры использования

### Использование curl

#### Получить все задачи
```bash
curl -u admin:admin123 http://localhost:8080/api/tasks
```

#### Создать задачу
```bash
curl -X POST -u admin:admin123 \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Изучить Spring Boot",
    "description": "Изучить основы Spring Boot",
    "status": "Pending"
  }' \
  http://localhost:8080/api/tasks
```

#### Получить задачу по ID
```bash
curl -u admin:admin123 http://localhost:8080/api/tasks/1
```

#### Обновить задачу
```bash
curl -X PUT -u admin:admin123 \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Изучить Spring Boot",
    "description": "Изучить основы Spring Boot",
    "status": "In Progress"
  }' \
  http://localhost:8080/api/tasks/1
```

#### Удалить задачу
```bash
curl -X DELETE -u admin:admin123 http://localhost:8080/api/tasks/1
```

## Модель данных

### Task (Задача)
- `id` (Long) - уникальный идентификатор (автоматически генерируется)
- `title` (String) - название задачи
- `description` (String) - описание задачи
- `status` (String) - статус задачи:
  - `Pending` - ожидает выполнения
  - `In Progress` - в процессе
  - `Completed` - завершена
- `createdAt` (LocalDateTime) - дата и время создания (устанавливается автоматически)

## Запуск тестов

### Unit тесты
```bash
mvn test
```

### E2E тесты
1. Убедитесь, что приложение запущено на порту 8080
2. Перейдите в директорию с тестами:
```bash
cd e2e
```

3. Установите зависимости:
```bash
npm install
```

4. Запустите тесты:
```bash
npm test
```

## Структура проекта

```
lab_spring/
├── pom.xml                                    # Maven конфигурация
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/taskmanagement/
│   │   │       ├── TaskManagementSystemApplication.java  # Главный класс
│   │   │       ├── config/
│   │   │       │   └── SecurityConfig.java              # Конфигурация безопасности
│   │   │       ├── controller/
│   │   │       │   └── TaskController.java              # REST контроллер
│   │   │       ├── model/
│   │   │       │   └── Task.java                        # Модель данных
│   │   │       ├── repository/
│   │   │       │   └── TaskRepository.java             # JPA репозиторий
│   │   │       ├── service/
│   │   │       │   └── TaskService.java                # Бизнес-логика
│   │   │       └── exception/
│   │   │           └── ResourceNotFoundException.java   # Кастомное исключение
│   │   └── resources/
│   │       └── application.yml                          # Конфигурация приложения
│   └── test/                                            # Unit тесты
└── e2e/
    ├── package.json                                     # Конфигурация E2E тестов
    └── tests/
        └── api.spec.ts                                  # Playwright тесты
```

## Конфигурация

### application.yml
- База данных: H2 in-memory
- JPA: автоматическое создание схемы
- H2 консоль: включена по адресу `/h2-console`

### Безопасность
- Тип аутентификации: HTTP Basic Authentication
- Пользователь по умолчанию: `admin` / `admin123`
- CSRF: отключен (для упрощения и работы с H2 консолью)

## Примечания

- База данных H2 является in-memory, поэтому данные теряются при перезапуске приложения
- Для production использования рекомендуется заменить H2 на PostgreSQL или MySQL
- CSRF защита отключена для упрощения работы с API и H2 консолью
