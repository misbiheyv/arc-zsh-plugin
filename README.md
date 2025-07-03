# arc-zsh-plugin

**arc-zsh-plugin** — это **Zsh** плагин, для Яндексовой системы контроля версий **[Arc](https://habr.com/ru/companies/yandex/articles/482926/)** .

Плагин в себя включает:
* Отображение актуальной ветки и ее статуса, по аналогии с плагином для гита
![Screenshot](https://github.com/user-attachments/assets/a50f2ac1-d8d0-40bb-bc69-841ad92e530c)

* Набор удобных алиасов и функций, которыми я пользуюсь

## Установка

Склонируйте репозиторий в директорию пользовательских плагинов:
  ```bash
  git clone https://github.com/misbiheyv/arc-zsh-plugin.git ${ZSH_CUSTOM}/plugins/arc
  ```

Добавьте `arc` в список плагинов в файле `~/.zshrc`:
  ```zsh
  plugins=(... arc)
  ```
> Пример того как должен выглядеть файл, можно найти в `examples/.zshrc.example`

Добавьте отображение в тему:
1. Создайте оверрайд вашей темы
    ```bash
    cp ${ZSH}/themes/${ZSH_THEME}.zsh-theme ${ZSH_CUSTOM}/themes/${ZSH_THEME}.zsh-theme
    ```

2. В созданном файле `${ZSH_CUSTOM}/themes/${ZSH_THEME}.zsh-theme` отредактируйте PROMPT
    ```zsh
    PROMPT="...$(arc_prompt_info_async)"
    ```
> Пример того как должен выглядеть файл, можно найти в `examples/crunch.zsh-theme.example`

Перезапустите терминал или примените изменения командой `source ~/.zshrc`
Готово! Теперь перейдите в репозиторий с arc и проверьте, что ветка отображается

> Цвета и префиксы берутся из переменных темы OMZ (`ZSH_THEME_GIT_PROMPT_*`). В большинстве популярных тем ничего настраивать не придётся.

### Алиасы и функции

| Команда              | Эквивалент Arc                                   | Описание |
|----------------------|--------------------------------------------------|----------|
| `am [suffix]`        | `arc mount -m ~/arcs/arcadia[-suffix] -S ~/arcs/store[-suffix]` | Монтировать репозиторий в кастомные директории |
| `aum [suffix]`       | `arc unmount -m ~/arcs/arcadia[-suffix]` or `diskutil unmount force ~/arcs/arcadia[-suffix]`         | Размонтировать репозиторий из кастомных директорий |
| `ast`                | `arc st`                                         | Показать статус репозитория |
| `ap`                 | `arc pull`                                       | Получить актуальные изменения из origin |
| `apt`                | `arc pull trunk`                                 | Получить изменения из `trunk` |
| `art`                | `arc pull trunk && arc rebase trunk`             | Обновить локальную ветку поверх `trunk` |
| `ac <msg>`           | `arc commit <msg> --no-verify`                   | Коммит без pre-commit хуков |
| `aca <msg>`          | `arc commit <msg> --amend --no-verify`           | Amend-коммит с новым сообщением |
| `acan`               | `arc commit --amend --no-edit --no-verify`       | Тихий amend без изменения сообщения |
| `aprc <msg>`         | `arc pr create <msg> --no-verify`                | Создать Pull Request |
| `apf`                | `arc push --force`                               | Форс-пуш |
| `ach <branch>`       | `arc checkout <branch>`                          | Переключиться на ветку (создать, если ее такой) |

### Переменные окружения

При необходимости можно переопределить стандартные переменные темы OMZ для изменения вида префикса/суффикса или символов чистого/грязного состояния.

Пример:

```zsh
# .zshrc
ZSH_THEME_GIT_PROMPT_PREFIX="on %F{cyan}"
ZSH_THEME_GIT_PROMPT_CLEAN="%f"
ZSH_THEME_GIT_PROMPT_DIRTY="%F{red}*%f"
```
