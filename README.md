![C++17](https://img.shields.io/badge/C%2B%2B-17-blue.svg)
![CMake](https://img.shields.io/badge/CMake-3.15%2B-green.svg)
![Raylib](https://img.shields.io/badge/GUI-Raylib-lightgrey.svg)
![Platform](https://img.shields.io/badge/platform-macOS%20%7C%20Linux%20%7C%20Windows-lightgrey.svg)
![License](https://img.shields.io/badge/license-GPLv3-yellow.svg)

<div align="center">

**A small colony. A harsh world. Endless decisions.**

*Build your colony, manage your settlers, and survive one day at a time.*

</div>

> **Project status:** 🚧 Active development · 🧪 Core tests available · 🎮 TUI + Raylib GUI
>
> **Checklist legend:** ✅ Done · ⬜ Planned · ⚠️ Needs verification

# 🏛️ WithLand — Colony Survival Simulator

WithLand is a small turn-based colony survival simulator written in C++17.

You manage a group of settlers and try to keep the colony alive for as long as possible. Every day can change the condition of your colonists, so you need to pay attention to their health, hunger, mood, professions, relationships, and the events happening around them.

The project is being developed as a modular game with two interface modes:

- TUI — a terminal-based interface for the core simulation.
- GUI — a graphical interface powered by Raylib.

This repository is a fork of the original WithLand project by Alexander Sharzhukov. The fork contains ongoing changes to the project structure, core logic, inventory, resource gathering, tests, and gameplay systems.

Original repository: https://github.com/Sharzhukov/WithLand

Current repository: https://github.com/vctvchg-cmd/WithLand

---

## 🌍 Language / Язык

English is the main language of the project.

Russian localization is not available yet, but it is planned for a future update.

<details>
<summary><strong>📚 Quick navigation</strong></summary>

- [What the game includes](#-what-the-game-includes)
- [Inventory](#-inventory)
- [Food and health](#-food-and-health)
- [Armor](#-armor)
- [Resource gathering](#-resource-gathering)
- [Interfaces](#-interfaces)
- [Project structure](#-project-structure)
- [Requirements](#-requirements)
- [Building and running](#-building-and-running)
- [Testing](#-testing)
- [Development status](#-development-status)
- [Roadmap](#️-roadmap)
- [Recommended next changes](#-recommended-next-changes)

</details>

---

## ✨ What the game includes

### 👥 Colony management

- Manage a group of settlers.
- Monitor colonist health, hunger, and mood.
- Assign professions.
- Track the general condition of the colony.
- Handle daily changes and colony events.
- Manage relationships and social interactions.

### 🧑‍🌾 Professions

The current project contains the following professions:

- Farmer
- Builder
- Medic
- Scout
- Guard
- Mage
- Idle

Professions provide different work outputs and are used by the colony simulation.

### ❤️ Survival systems

The core currently contains systems for:

- Health.
- Hunger.
- Mood.
- Damage.
- Death conditions.
- Recovery.
- Age and days lived.
- Daily simulation.
- Colony events.
- Randomized gameplay values.

### 📅 Day-by-day gameplay

The simulation advances one day at a time.

During the daily update, colonists can age, lose hunger, recover health or mood, and change their overall state. The colony remains alive while it still has living colonists.

### 📜 Events and reports

The project contains event and report-related systems for tracking changes in the colony and its settlers.

---

## 🎒 Inventory

The first version of the inventory system is already present in the project.

Current inventory functionality includes:

- Opening and closing the inventory with the `Tab` key where supported by the interface.
- Storing items and their quantities.
- Stackable items.
- Food items.
- Wood resources.
- Adding resources to the inventory.
- Removing items from the inventory.
- Checking the quantity of an item.
- Reading the current inventory slots.

The current inventory implementation includes the basic item identifiers `food` and `wood`.

The inventory is still being expanded and is not yet a complete equipment system.

---

## 🍎 Food and health

Food and health are treated as separate gameplay systems.

The current implementation and tests cover health limits and inventory-related behavior. Food is intended to restore health, while health must remain within its allowed range.

Armor is not restored by food. Health and armor are separate values in the planned gameplay model.

Some food and armor interactions are still under development and may change as the core is expanded.

---

## 🛡️ Armor

The project contains the initial foundation for armor-related behavior, but the complete armor system is not finished yet.

The current direction includes:

- Keeping armor separate from health.
- Starting without equipped armor.
- Allowing armor to remain at `0` when nothing is equipped.
- Keeping food recovery separate from armor recovery.

Planned armor features:

- Armor items.
- Equipment slots.
- Armor equipment.
- Armor durability.
- Armor damage.
- Armor repair.
- Armor crafting.

---

## 🌲 Resource gathering

Basic resource gathering has been added to the project.

The current implementation includes:

- Interacting with trees.
- Harvesting wood.
- Adding gathered wood to the inventory.
- Updating the world state after harvesting.

More resource types and more advanced gathering rules are planned for later development.

---

## 🖥️ Interfaces

### TUI

The terminal interface is intended for running the core simulation without opening a graphical window. It is useful for testing and playing the basic simulation directly from a terminal.

### GUI

The graphical interface is powered by Raylib. It includes the current world and interface foundation, but it is still under active development and should not be considered feature-complete.

---

## 🏗️ Project structure

```text
WithLand/
├── .github/
│   └── ISSUE_TEMPLATE/
├── include/
│   ├── common/
│   ├── core/
│   ├── gui/
│   │   └── lib/
│   └── tui/
├── src/
│   ├── common/
│   ├── core/
│   ├── gui/
│   │   └── lib/
│   └── tui/
├── resources/
│   ├── assets/
│   └── img/
├── tests/
├── CMakeLists.txt
├── COPYING
├── CONTRIBUTING.md
├── Info.plist
├── NOTICE
├── README.md
├── SECURITY.md
└── UPSTREAM.md
```

Important core files include:

- `Colonist` — colonist state and daily behavior.
- `Colony` — colony population and colony state.
- `Event` — event data and event behavior.
- `DayReport` — daily report data.
- `Wedding` — social and marriage-related logic.
- `PlayerInventory` — item storage and inventory operations.
- `FileManager` — file-related utilities.
- `Logger` — logging support.
- `ThreadPool` — thread-pool infrastructure.

---

## 📦 Requirements

| Component | Requirement |
|---|---|
| C++ | C++17 |
| CMake | 3.15 or newer |
| Compiler | Clang, GCC, or MSVC |
| Git | Required for cloning and FetchContent |
| Raylib | Automatically fetched for GUI builds |

Raylib is downloaded automatically through CMake `FetchContent` when GUI support is enabled.

The TUI and test builds use the core sources without requiring a Raylib window.

---

## 🚀 Building and running

### 1. Clone the repository

```bash
git clone https://github.com/vctvchg-cmd/WithLand.git
cd WithLand
```

### 2. Build the TUI version

The default build uses the terminal interface.

```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug
cmake --build build -j 8
```

Run on Linux or macOS:

```bash
./build/bin/WithLand
```

Run on Windows:

```powershell
.\build\bin\WithLand.exe
```

The executable is configured as `WithLand` in this fork.

### 3. Build the GUI version

Enable GUI support with `ENABLE_GUI=ON`.

```bash
cmake -S . -B build-gui -DENABLE_GUI=ON -DCMAKE_BUILD_TYPE=Debug
cmake --build build-gui -j 8
```

Raylib is fetched automatically during configuration.

Run on Linux:

```bash
./build-gui/bin/WithLand
```

Run on macOS:

```bash
open build-gui/bin/WithLand.app
```

Run on Windows:

```powershell
.\build-gui\bin\WithLand.exe
```

### 4. Build the Release version

```bash
cmake -S . -B build-release -DCMAKE_BUILD_TYPE=Release
cmake --build build-release -j 8
```

---

## ⚙️ CMake options

| Option | Default | Description |
|---|---|---|
| `ENABLE_GUI` | `OFF` | Enables the Raylib graphical interface |
| `BUILD_TESTS` | `OFF` | Builds the CTest test executable |
| `CMAKE_BUILD_TYPE` | Not set | `Debug`, `Release`, or `RelWithDebInfo` |

Example GUI build:

```bash
cmake -S . -B build-gui -DENABLE_GUI=ON -DCMAKE_BUILD_TYPE=Release
```

Example test build:

```bash
cmake -S . -B build-tests -DBUILD_TESTS=ON -DCMAKE_BUILD_TYPE=Debug
```

---

## 🧪 Testing

The project contains a lightweight test framework and a core test executable.

Build the tests:

```bash
cmake -S . -B build-tests -DBUILD_TESTS=ON -DCMAKE_BUILD_TYPE=Debug
cmake --build build-tests -j 8
```

Run the tests:

```bash
ctest --test-dir build-tests --output-on-failure
```

Current test coverage includes:

- Initial colonist state.
- Health boundaries.
- Hunger boundaries.
- Mood boundaries.
- Damage handling.
- Death conditions.
- Age limits.
- Daily updates.
- Name validation.
- Profession names.
- Profession work output.
- Colony population.
- Living-colonist count.
- Colony death conditions.
- Event defaults and event data.
- Inventory item addition.
- Inventory item removal.
- Inventory quantity checks.
- Stack limits.
- Invalid inventory input.

The test suite is part of the ongoing stabilization work. More regression tests will be added as new gameplay systems are implemented.

---

## 🎮 How to play

The exact gameplay flow is still evolving, but the general loop is:

1. Start the TUI or GUI version.
2. Create or enter a colony.
3. Review the condition of the settlers.
4. Assign or use professions and available resources.
5. Advance the simulation day by day.
6. React to events and changes in the colony.
7. Try to keep at least one colonist alive.

Some interface and gameplay details may change while the project is under development.

---

## 🛠️ Platform support

| Platform | Status |
|---|---|
| macOS — Apple Silicon / Intel | Main development platform |
| Linux | Supported build target |
| Windows — MSVC / MinGW | Requires additional verification and may need fixes |

---

## 📊 Development status

WithLand is an active work-in-progress project.

The current development focus is on keeping the core stable, making the inventory and resource systems usable, and adding tests before expanding the gameplay further.

Currently present in the codebase:

- [x] Core colony and colonist logic.
- [x] Profession system.
- [x] Social and wedding-related logic.
- [x] Daily simulation.
- [x] Events and reports.
- [x] Inventory foundation.
- [x] Food and wood item identifiers.
- [x] Basic wood gathering.
- [x] TUI build.
- [x] Raylib GUI build path.
- [x] Save and file utility foundations.
- [x] Logging utilities.
- [x] Thread-pool infrastructure.
- [x] Core regression tests.

The following areas are incomplete or require further verification:

- [ ] Full GUI gameplay.
- [ ] Complete inventory and equipment behavior.
- [ ] Full armor mechanics.
- [ ] Crafting.
- [ ] Complete save and load workflow.
- [ ] Expanded diseases and random events.
- [ ] Enemy and animal behavior.
- [ ] Full Windows support.
- [ ] Broader automated test coverage.

---

## 🗺️ Roadmap

### Core and gameplay

- [x] Basic colony and colonist logic.
- [x] Profession system.
- [x] Social and wedding-related logic.
- [x] Daily simulation foundation.
- [x] Event and report foundations.
- [ ] Expand survival mechanics.
- [ ] Improve daily events.
- [ ] Expand diseases and recovery.
- [ ] Improve relationships and social interactions.
- [ ] Add enemy and animal AI.

### Inventory

- [x] Basic inventory class.
- [x] Item quantities.
- [x] Stack limits.
- [x] Food item.
- [x] Wood item.
- [x] Add and remove operations.
- [ ] Improve multi-stack inventory behavior.
- [ ] Add more item types.
- [ ] Add item usage rules.
- [ ] Add equipment support.

### Armor

- [x] Separate armor concept.
- [x] Initial armor foundation.
- [ ] Add armor items.
- [ ] Add equipment slots.
- [ ] Add armor equipment.
- [ ] Add durability.
- [ ] Add armor damage.
- [ ] Add repair.
- [ ] Add armor crafting.

### Resource gathering

- [x] Tree interaction foundation.
- [x] Wood harvesting.
- [x] Adding wood to inventory.
- [ ] Add more resource types.
- [ ] Add resource regeneration.
- [ ] Expand world interaction.
- [ ] Add advanced gathering mechanics.

### Crafting

- [ ] Add crafting recipes.
- [ ] Add crafting stations.
- [ ] Add resource-based production.

### World and GUI

- [ ] Improve the GUI into a complete playable interface.
- [ ] Improve camera movement.
- [ ] Expand the world.
- [ ] Add more environmental objects.
- [ ] Improve visual feedback.

### Persistence

- [ ] Complete save and load workflow.
- [ ] Improve save validation.
- [ ] Add save-version compatibility.

### Localization

- [ ] Add Russian localization.
- [ ] Prepare the project for additional languages.

### Testing and quality

- [x] Add core regression tests.
- [ ] Expand edge-case coverage.
- [ ] Add more inventory and gathering tests.
- [ ] Add automated build checks.
- [ ] Verify Windows builds.
- [ ] Verify that all project, target, bundle, and documentation names consistently use `WithLand`.

---

## 🔧 Recommended next changes

> **Priority:** ⭐ High-impact cleanup before expanding gameplay

The following changes are recommended for the fork before adding larger gameplay features:

1. Ensure the CMake project and executable are consistently named `WithLand`.
2. Update the macOS bundle identifier and bundle name from the original project name.
3. Keep the fork attribution in `NOTICE`, `UPSTREAM.md`, and source-file headers.
4. Add tests for the complete inventory behavior, including multiple stacks and invalid amounts.
5. Finish and verify the food-consumption flow in the actual TUI and GUI.
6. Finish the armor data model before adding equipment or durability.
7. Add a clear save/load format and tests before relying on persistent saves.
8. Verify the GUI build on Linux, macOS, and Windows.
9. Keep README claims synchronized with the actual implementation.
10. Continue separating core logic from TUI and GUI code so the core remains easy to test.

---

## 🤝 Contributing

Contributions, bug reports, suggestions, and pull requests are welcome.

Before opening a Pull Request:

1. Build the project successfully.
2. Run the test suite.
3. Check that existing gameplay logic still works.
4. Add regression tests for new core behavior where possible.
5. Keep GUI and TUI code separate from the core simulation.
6. Document important changes.

Create a feature branch with:

```bash
git checkout -b feature/my-idea
```

Then commit your changes and open a Pull Request with a clear description.

---

## 📚 Documentation

| Path | Description |
|---|---|
| `include/core/` | Core headers and gameplay interfaces |
| `include/common/` | Common utilities and helper classes |
| `src/core/` | Core simulation implementation |
| `src/common/` | Logging, files, and shared utilities |
| `src/tui/` | Terminal interface |
| `src/gui/` | Raylib graphical interface |
| `tests/` | Core regression tests |
| `docs/` | Additional documentation when available |
| `UPSTREAM.md` | Information about the upstream project and fork |

---

## 📄 License

WithLand is distributed under the **GNU General Public License version 3 or any later version**.

See the `COPYING` file for the full license text.

---

## 📌 Attribution

This project is a fork of the original project by Alexander Sharzhukov.

Original repository:

https://github.com/Sharzhukov/WithLand

Current repository:

https://github.com/vctvchg-cmd/WithLand

---

## ⭐ Support the project

If you like the idea of WithLand:

- Star the repository on GitHub.
- Report bugs through Issues.
- Suggest new features.
- Share the project with other developers.
- Contribute improvements through Pull Requests.

Thanks for checking out WithLand!

---

# 🏛️ WithLand — симулятор выживания колонии

WithLand — небольшой пошаговый симулятор выживания колонии, написанный на C++17.

Вы управляете группой поселенцев и пытаетесь сохранить колонию живой как можно дольше. Каждый день может изменить состояние колонистов, поэтому необходимо следить за их здоровьем, голодом, настроением, профессиями, отношениями и происходящими событиями.

Проект развивается как модульная игра с двумя режимами интерфейса:

- TUI — интерфейс на основе терминала для основной симуляции.
- GUI — графический интерфейс на базе Raylib.

Этот репозиторий является форком оригинального проекта WithLand Александра Шаржукова. Форк содержит текущие изменения структуры проекта, основной логики, инвентаря, добычи ресурсов, тестов и игровых систем.

Оригинальный репозиторий: https://github.com/Sharzhukov/WithLand

Текущий репозиторий: https://github.com/vctvchg-cmd/WithLand

---

## 🌍 Язык

Английский является основным языком проекта.

Русская локализация пока недоступна, но запланирована для будущего обновления.

<details>
<summary><strong>📚 Быстрая навигация</strong></summary>

- [Что уже есть в игре](#-что-уже-есть-в-игре)
- [Инвентарь](#-инвентарь)
- [Еда и здоровье](#-еда-и-здоровье)
- [Броня](#-броня)
- [Добыча ресурсов](#-добыча-ресурсов)
- [Интерфейсы](#-интерфейсы)
- [Структура проекта](#-структура-проекта)
- [Требования](#-требования)
- [Сборка и запуск](#-сборка-и-запуск)
- [Тестирование](#-тестирование)
- [Статус разработки](#-статус-разработки)
- [План развития](#-план-развития)
- [Рекомендуемые следующие изменения](#-рекомендуемые-следующие-изменения)

</details>

---

## ✨ Что уже есть в игре

### 👥 Управление колонией

- Управление группой поселенцев.
- Отслеживание здоровья, голода и настроения колонистов.
- Назначение профессий.
- Отслеживание общего состояния колонии.
- Обработка ежедневных изменений и событий колонии.
- Управление отношениями и социальными взаимодействиями.

### 🧑‍🌾 Профессии

В текущем проекте представлены следующие профессии:

- Фермер.
- Строитель.
- Медик.
- Разведчик.
- Страж.
- Маг.
- Без дела.

Профессии дают разные результаты работы и используются в симуляции колонии.

### ❤️ Системы выживания

Ядро сейчас содержит системы для:

- Здоровья.
- Голода.
- Настроения.
- Урона.
- Условий смерти.
- Восстановления.
- Возраста и прожитых дней.
- Ежедневной симуляции.
- Событий колонии.
- Случайных игровых значений.

### 📅 Игровой процесс по дням

Симуляция продвигается по одному игровому дню за раз.

Во время ежедневного обновления колонисты могут стареть, терять сытость, восстанавливать здоровье или настроение и менять своё общее состояние. Колония остаётся живой, пока в ней есть хотя бы один живой колонист.

### 📜 События и отчёты

В проекте есть системы событий и отчётов, предназначенные для отслеживания изменений в колонии и среди её поселенцев.

---

## 🎒 Инвентарь

Первая версия системы инвентаря уже присутствует в проекте.

Текущая функциональность инвентаря включает:

- Открытие и закрытие инвентаря клавишей `Tab`, если это поддерживается интерфейсом.
- Хранение предметов и их количества.
- Предметы, объединяемые в стаки.
- Еду.
- Ресурсы древесины.
- Добавление ресурсов в инвентарь.
- Удаление предметов из инвентаря.
- Проверку количества предмета.
- Чтение текущих слотов инвентаря.

Текущая реализация инвентаря включает базовые идентификаторы предметов `food` и `wood`.

Инвентарь всё ещё расширяется и пока не является полноценной системой экипировки.

---

## 🍎 Еда и здоровье

Еда и здоровье рассматриваются как отдельные игровые системы.

Текущая реализация и тесты охватывают ограничения здоровья и поведение, связанное с инвентарём. Предполагается, что еда будет восстанавливать здоровье, а здоровье должно оставаться в допустимом диапазоне.

Еда не восстанавливает броню. Здоровье и броня являются отдельными значениями в планируемой игровой модели.

Некоторые взаимодействия еды и брони всё ещё находятся в разработке и могут измениться по мере расширения ядра.

---

## 🛡️ Броня

В проекте есть начальная основа для поведения, связанного с бронёй, но полноценная система брони ещё не завершена.

Текущее направление включает:

- Отделение брони от здоровья.
- Начало игры без экипированной брони.
- Возможность оставлять броню равной `0`, если ничего не экипировано.
- Отделение восстановления еды от восстановления брони.

Запланированные возможности брони:

- Предметы брони.
- Слоты экипировки.
- Экипировка брони.
- Прочность брони.
- Урон по броне.
- Ремонт брони.
- Создание брони.

---

## 🌲 Добыча ресурсов

В проект добавлена базовая добыча ресурсов.

Текущая реализация включает:

- Взаимодействие с деревьями.
- Добычу древесины.
- Добавление добытой древесины в инвентарь.
- Обновление состояния мира после добычи.

Больше типов ресурсов и более сложные правила добычи запланированы на последующие этапы разработки.

---

## 🖥️ Интерфейсы

### TUI

Терминальный интерфейс предназначен для запуска основной симуляции без открытия графического окна. Он полезен для тестирования и игры в базовую симуляцию непосредственно из терминала.

### GUI

Графический интерфейс работает на базе Raylib. Он включает текущий мир и основу интерфейса, но всё ещё активно разрабатывается и не должен считаться полностью завершённым.

---

## 🏗️ Структура проекта

```text
WithLand/
├── .github/
│   └── ISSUE_TEMPLATE/
├── include/
│   ├── common/
│   ├── core/
│   ├── gui/
│   │   └── lib/
│   └── tui/
├── src/
│   ├── common/
│   ├── core/
│   ├── gui/
│   │   └── lib/
│   └── tui/
├── resources/
│   ├── assets/
│   └── img/
├── tests/
├── CMakeLists.txt
├── COPYING
├── CONTRIBUTING.md
├── Info.plist
├── NOTICE
├── README.md
├── SECURITY.md
└── UPSTREAM.md
```

Важные файлы ядра включают:

- `Colonist` — состояние колониста и ежедневное поведение.
- `Colony` — население и состояние колонии.
- `Event` — данные событий и поведение событий.
- `DayReport` — данные ежедневного отчёта.
- `Wedding` — логика социальных взаимодействий и брака.
- `PlayerInventory` — хранение предметов и операции инвентаря.
- `FileManager` — утилиты для работы с файлами.
- `Logger` — поддержка журналирования.
- `ThreadPool` — инфраструктура пула потоков.

---

## 📦 Требования

| Компонент | Требование |
|---|---|
| C++ | C++17 |
| CMake | 3.15 или новее |
| Компилятор | Clang, GCC или MSVC |
| Git | Требуется для клонирования и FetchContent |
| Raylib | Автоматически загружается для GUI-сборок |

Raylib автоматически загружается через CMake `FetchContent`, когда включена поддержка GUI.

Сборки TUI и тестов используют исходники ядра без необходимости открывать окно Raylib.

---

## 🚀 Сборка и запуск

### 1. Клонирование репозитория

```bash
git clone https://github.com/vctvchg-cmd/WithLand.git
cd WithLand
```

### 2. Сборка версии TUI

Сборка по умолчанию использует терминальный интерфейс.

```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug
cmake --build build -j 8
```

Запуск в Linux или macOS:

```bash
./build/bin/WithLand
```

Запуск в Windows:

```powershell
.\\build\\bin\\WithLand.exe
```

Исполняемый файл в этом форке настроен как `WithLand`.

### 3. Сборка версии GUI

Включите поддержку GUI с помощью `ENABLE_GUI=ON`.

```bash
cmake -S . -B build-gui -DENABLE_GUI=ON -DCMAKE_BUILD_TYPE=Debug
cmake --build build-gui -j 8
```

Raylib автоматически загружается во время конфигурации.

Запуск в Linux:

```bash
./build-gui/bin/WithLand
```

Запуск в macOS:

```bash
open build-gui/bin/WithLand.app
```

Запуск в Windows:

```powershell
.\\build-gui\\bin\\WithLand.exe
```

### 4. Сборка Release-версии

```bash
cmake -S . -B build-release -DCMAKE_BUILD_TYPE=Release
cmake --build build-release -j 8
```

---

## ⚙️ Опции CMake

| Опция | Значение по умолчанию | Описание |
|---|---|---|
| `ENABLE_GUI` | `OFF` | Включает графический интерфейс Raylib |
| `BUILD_TESTS` | `OFF` | Собирает исполняемый файл тестов CTest |
| `CMAKE_BUILD_TYPE` | Не задано | `Debug`, `Release` или `RelWithDebInfo` |

Пример сборки GUI:

```bash
cmake -S . -B build-gui -DENABLE_GUI=ON -DCMAKE_BUILD_TYPE=Release
```

Пример сборки тестов:

```bash
cmake -S . -B build-tests -DBUILD_TESTS=ON -DCMAKE_BUILD_TYPE=Debug
```

---

## 🧪 Тестирование

В проекте есть лёгкий тестовый фреймворк и исполняемый файл тестов ядра.

Сборка тестов:

```bash
cmake -S . -B build-tests -DBUILD_TESTS=ON -DCMAKE_BUILD_TYPE=Debug
cmake --build build-tests -j 8
```

Запуск тестов:

```bash
ctest --test-dir build-tests --output-on-failure
```

Текущее покрытие тестами включает:

- Начальное состояние колониста.
- Границы здоровья.
- Границы голода.
- Границы настроения.
- Обработку урона.
- Условия смерти.
- Ограничения возраста.
- Ежедневные обновления.
- Проверку имён.
- Названия профессий.
- Результаты работы профессий.
- Население колонии.
- Количество живых колонистов.
- Условия смерти колонии.
- Значения событий по умолчанию и данные событий.
- Добавление предметов в инвентарь.
- Удаление предметов из инвентаря.
- Проверку количества предметов в инвентаре.
- Ограничения стаков.
- Некорректные входные данные инвентаря.

Набор тестов является частью продолжающейся работы по стабилизации. По мере реализации новых игровых систем будут добавляться дополнительные регрессионные тесты.

---

## 🎮 Как играть

Точный игровой процесс всё ещё меняется, но общий цикл выглядит так:

1. Запустите версию TUI или GUI.
2. Создайте колонию или войдите в неё.
3. Проверьте состояние поселенцев.
4. Назначайте или используйте профессии и доступные ресурсы.
5. Продвигайте симуляцию день за днём.
6. Реагируйте на события и изменения в колонии.
7. Старайтесь сохранить жизнь хотя бы одному колонисту.

Некоторые детали интерфейса и игрового процесса могут измениться во время разработки проекта.

---

## 🛠️ Поддержка платформ

| Платформа | Статус |
|---|---|
| macOS — Apple Silicon / Intel | Основная платформа разработки |
| Linux | Поддерживаемая цель сборки |
| Windows — MSVC / MinGW | Требует дополнительной проверки и может потребовать исправлений |

---

## 📊 Статус разработки

WithLand — активный проект, находящийся в разработке.

Текущий фокус разработки — поддержание стабильности ядра, обеспечение удобства инвентаря и системы ресурсов, а также добавление тестов перед дальнейшим расширением игрового процесса.

Сейчас в кодовой базе присутствуют:

- Основная логика колонии и колонистов.
- Система профессий.
- Логика социальных взаимодействий и брака.
- Ежедневная симуляция.
- События и отчёты.
- Основа инвентаря.
- Идентификаторы предметов еды и древесины.
- Базовая добыча древесины.
- Сборка TUI.
- Путь сборки GUI на базе Raylib.
- Основы сохранения и файловых утилит.
- Утилиты журналирования.
- Инфраструктура пула потоков.
- Регрессионные тесты ядра.

Следующие области ещё не завершены или требуют дополнительной проверки:

- Полноценный игровой процесс GUI.
- Полное поведение инвентаря и экипировки.
- Полная механика брони.
- Крафт.
- Полный процесс сохранения и загрузки.
- Расширенные болезни и случайные события.
- Поведение врагов и животных.
- Полная поддержка Windows.
- Более широкое автоматизированное покрытие тестами.

---

## 🗺️ План развития

### Ядро и игровой процесс

- [x] Базовая логика колонии и колонистов.
- [x] Система профессий.
- [x] Логика социальных взаимодействий и брака.
- [x] Основа ежедневной симуляции.
- [x] Основы событий и отчётов.
- [ ] Расширить механики выживания.
- [ ] Улучшить ежедневные события.
- [ ] Расширить болезни и восстановление.
- [ ] Улучшить отношения и социальные взаимодействия.
- [ ] Добавить ИИ врагов и животных.

### Инвентарь

- [x] Базовый класс инвентаря.
- [x] Количество предметов.
- [x] Ограничения стаков.
- [x] Предмет еды.
- [x] Предмет древесины.
- [x] Операции добавления и удаления.
- [ ] Улучшить работу инвентаря с несколькими стаками.
- [ ] Добавить больше типов предметов.
- [ ] Добавить правила использования предметов.
- [ ] Добавить поддержку экипировки.

### Броня

- [x] Отдельная концепция брони.
- [x] Начальная основа брони.
- [ ] Добавить предметы брони.
- [ ] Добавить слоты экипировки.
- [ ] Добавить экипировку брони.
- [ ] Добавить прочность.
- [ ] Добавить урон по броне.
- [ ] Добавить ремонт.
- [ ] Добавить создание брони.

### Добыча ресурсов

- [x] Основа взаимодействия с деревьями.
- [x] Добыча древесины.
- [x] Добавление древесины в инвентарь.
- [ ] Добавить больше типов ресурсов.
- [ ] Добавить восстановление ресурсов.
- [ ] Расширить взаимодействие с миром.
- [ ] Добавить продвинутые механики добычи.

### Крафт

- [ ] Добавить рецепты крафта.
- [ ] Добавить станции крафта.
- [ ] Добавить производство на основе ресурсов.

### Мир и GUI

- [ ] Улучшить GUI до полноценного игрового интерфейса.
- [ ] Улучшить перемещение камеры.
- [ ] Расширить мир.
- [ ] Добавить больше объектов окружения.
- [ ] Улучшить визуальную обратную связь.

### Сохранения

- [ ] Завершить процесс сохранения и загрузки.
- [ ] Улучшить проверку сохранений.
- [ ] Добавить совместимость версий сохранений.

### Локализация

- [ ] Добавить русскую локализацию.
- [ ] Подготовить проект для дополнительных языков.

### Тестирование и качество

- [x] Добавить регрессионные тесты ядра.
- [ ] Расширить покрытие крайних случаев.
- [ ] Добавить больше тестов инвентаря и добычи ресурсов.
- [ ] Добавить автоматические проверки сборки.
- [ ] Проверить сборки Windows.
- [ ] Проверить, что названия проекта, целей сборки, бандла и документации везде используют `WithLand`.

---

## 🔧 Рекомендуемые следующие изменения

Перед добавлением крупных игровых функций для форка рекомендуются следующие изменения:

1. Убедиться, что проект и исполняемый файл CMake везде имеют имя `WithLand`.
2. Обновить идентификатор bundle и имя bundle macOS, чтобы они больше не использовали оригинальное название проекта.
3. Сохранить информацию о форке в `NOTICE`, `UPSTREAM.md` и заголовках исходных файлов.
4. Добавить тесты для полного поведения инвентаря, включая несколько стаков и некорректные количества.
5. Завершить и проверить фактический процесс потребления еды в TUI и GUI.
6. Завершить модель данных брони перед добавлением экипировки или прочности.
7. Добавить понятный формат сохранений и тесты до того, как полагаться на постоянные сохранения.
8. Проверить сборку GUI в Linux, macOS и Windows.
9. Синхронизировать утверждения README с фактической реализацией.
10. Продолжать отделять логику ядра от кода TUI и GUI, чтобы ядро оставалось удобным для тестирования.

---

## 🤝 Участие в разработке

Приветствуются вклад в проект, сообщения об ошибках, предложения и pull request.

Перед открытием Pull Request:

1. Успешно соберите проект.
2. Запустите набор тестов.
3. Проверьте, что существующая игровая логика продолжает работать.
4. По возможности добавьте регрессионные тесты для нового поведения ядра.
5. Держите код GUI и TUI отдельно от основной симуляции.
6. Документируйте важные изменения.

Создайте ветку для новой функции:

```bash
git checkout -b feature/my-idea
```

Затем создайте коммит и откройте Pull Request с понятным описанием.

---

## 📚 Документация

| Путь | Описание |
|---|---|
| `include/core/` | Заголовки ядра и интерфейсы игрового процесса |
| `include/common/` | Общие утилиты и вспомогательные классы |
| `src/core/` | Реализация основной симуляции |
| `src/common/` | Журналирование, работа с файлами и общие утилиты |
| `src/tui/` | Терминальный интерфейс |
| `src/gui/` | Графический интерфейс Raylib |
| `tests/` | Регрессионные тесты ядра |
| `docs/` | Дополнительная документация, если доступна |
| `UPSTREAM.md` | Информация об оригинальном проекте и форке |

---

## 📄 Лицензия

WithLand распространяется по **GNU General Public License версии 3 или любой более поздней версии**.

Полный текст лицензии находится в файле `COPYING`.

---

## 📌 Атрибуция

Этот проект является форком оригинального проекта Александра Шаржукова.

Оригинальный репозиторий:

https://github.com/Sharzhukov/WithLand

Текущий репозиторий:

https://github.com/vctvchg-cmd/WithLand

---

## ⭐ Поддержка проекта

Если вам нравится идея WithLand:

- Поставьте звезду репозиторию на GitHub.
- Сообщайте об ошибках через Issues.
- Предлагайте новые функции.
- Делитесь проектом с другими разработчиками.
- Предлагайте улучшения через Pull Requests.

Спасибо, что посмотрели WithLand!
