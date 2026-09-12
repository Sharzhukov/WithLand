![C++17](https://img.shields.io/badge/C%2B%2B-17-blue.svg)
![CMake](https://img.shields.io/badge/CMake-3.16%2B-green.svg)
![Platform](https://img.shields.io/badge/platform-macOS%20%7C%20Linux%20%7C%20Windows-lightgrey.svg)
![License](https://img.shields.io/badge/license-MIT-yellow.svg)

# 🏛️ WithLand — Colony Survival Simulator

Пошаговый симулятор выживания колонии на **C++17**. Игрок управляет группой
поселенцев: их здоровьем, голодом, настроением, профессиями и социальными
связями. Каждый день меняет состояние колонии — выживет она или нет, зависит
от решений игрока.

Проект собирается через **CMake**, поддерживает **консольный (TUI)** и
**графический (GUI, Raylib)** интерфейсы.

---

## ✨ Возможности

- 🧑‍🌾 **5 профессий:** Farmer, Builder, Medic, Scout, Guard — каждая влияет
  на экономику колонии по-своему
- ❤️ **Динамика состояния:** здоровье, голод, настроение — меняются каждый день
- 💍 **Социальные связи:** свадьбы, отношения между поселенцами
- 📅 **Пошаговая симуляция:** день за днём, с отчётами и событиями
- 📜 **Журнал событий:** что произошло в колонии и почему
- 🖥️ **Два интерфейса:** цветной консольный (TUI) и графический (GUI)
- 💾 **Сохранение/загрузка** — в разработке
- 🧵 **Многопоточная симуляция** — в планах

---

## 🏗️ Структура проекта

```
WithLand/
├── CMakeLists.txt          # корневой сборочный скрипт
├── include/                # публичные заголовки
├── src/
│   ├── main.cpp            # точка входа
│   ├── core/               # ядро симуляции (Colony, Colonist, Wedding, ...)
│   ├── common/             # утилиты (Logger, FileManager, common)
│   ├── tui/                # консольный интерфейс
│   └── gui/                # графический интерфейс (Raylib)
├── resources/              # иконки, ассеты
└── docs/                   # архитектурная документация (в разработке)
```

---

## 📦 Требования

| Компонент | Версия |
|---|---|
| **CMake** | 3.16+ |
| **Компилятор** | Clang, GCC 9+, MSVC 2019+ |
| **C++** | C++17 |
| **Git** | для клонирования (и для FetchContent) |

Raylib подтягивается автоматически через `FetchContent` при сборке GUI —
отдельно ставить не нужно.

---

## 🚀 Сборка и запуск

### 1. Клонирование

```bash
git clone https://github.com/Sharzhukov/WithLand.git
cd WithLand
```

### 2. TUI-сборка (быстрая, без raylib)

```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug
cmake --build build -j 8
./build/bin/WithLand
```

### 3. GUI-сборка (Raylib, первый раз ~2 мин)

```bash
cmake -S . -B build-gui -DCMAKE_BUILD_TYPE=Debug -DENABLE_GUI=ON
cmake --build build-gui -j 8
```

**macOS:**
```bash
open build-gui/bin/WithLand.app
# или
./build-gui/bin/WithLand.app/Contents/MacOS/WithLand
```

**Linux / Windows:**
```bash
./build-gui/bin/WithLand
build-gui\bin\WithLand.exe
```

### 4. Release-сборка

```bash
cmake -S . -B build-release -DCMAKE_BUILD_TYPE=Release
cmake --build build-release -j 8
```

---

## ⚙️ Опции CMake

| Опция | По умолчанию | Описание |
|---|---|---|
| `ENABLE_GUI` | `OFF` | Собрать GUI-версию на Raylib вместо TUI |
| `CMAKE_BUILD_TYPE` | *(пусто)* | `Debug` / `Release` / `RelWithDebInfo` |

Пример:
```bash
cmake -S . -B build-gui -DENABLE_GUI=ON -DCMAKE_BUILD_TYPE=Release
```

---

## 🎮 Как играть

1. Запусти бинарник (TUI или GUI).
2. Создай колонию — задай имя и стартовых поселенцев.
3. Управляй ресурсами: еда, материалы, укрытия.
4. Каждый ход = один день. Следи за состоянием поселенцев.
5. Игра заканчивается, когда колония гибнет или достигает цели выживания.

*(Более подробное руководство — в `docs/gameplay.md`, когда появится.)*

---

## 🛠️ Платформы

| Платформа | Статус |
|---|---|
| macOS (Apple Silicon / Intel) | ✅ Основная |
| Linux | ✅ Собирается |
| Windows (MSVC / MinGW) | 🔄 В работе |

---

## 🔮 Roadmap

- [x] Базовая логика колонии и поселенцев
- [x] Система профессий
- [x] Социальные связи (свадьбы)
- [x] Консольный интерфейс (TUI)
- [x] Разделение на модули (`core`, `common`, `tui`, `gui`)
- [x] Сборка через CMake + FetchContent
- [ ] GUI на Raylib — довести до играбельного состояния
- [ ] Система сохранения и загрузки
- [ ] Случайные события и болезни
- [ ] ИИ для врагов и животных
- [ ] Многопоточная симуляция дня
- [ ] Юнит-тесты (Catch2 / Google Test)
- [ ] Логика магии и тематическое расширение

---

## 🤝 Вклад в проект

Проект открыт для идей, баг-репортов и пул-реквестов.

1. Форкни репозиторий
2. Создай ветку: `git checkout -b feature/my-idea`
3. Сделай изменения, убедись что собирается без warning'ов
4. Открой Pull Request с описанием

Перед PR — прогони сборку с `-Wall -Wextra` (уже включено в проект) и
проверь, что всё чисто.

---

## 📚 Документация

| Путь | Содержание |
|---|---|
| `include/core/` | Заголовки ядра — комментарии в коде |
| `include/common/` | Утилиты и хелперы |
| `docs/` | Архитектура, геймплей (в разработке) |

---

## 📄 Лицензия

Распространяется под лицензией **MIT**.
См. файл [LICENSE](LICENSE).

---

**Автор:** Alexander Sharzhukov
**GitHub:** [@Sharzhukov](https://github.com/Sharzhukov)

---

## ⭐ Поддержка

Если проект интересен:
- Поставь звезду ⭐ на GitHub
- Расскажи друзьям
- Предложи идею или найди баг — открой Issue

Спасибо, что заглянул в **WithLand**! 🚀
