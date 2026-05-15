# Voice Copywriter — Настройка для Миракали

Скилл из репозитория [qwwiwi/voice-copywriter](https://github.com/qwwiwi/voice-copywriter).

Превращает AI-агента в копирайтера, который пишет в твоём голосе и помнит стиль между сессиями.

## Структура памяти

```
memory/
  cold/
    MEMORY.md          ← постоянный архив, лог правок, история сессий
  warm/
    WARM_MEMORY.md     ← профиль автора, каналы, золотые правила
    TONE_OF_VOICE.md   ← глобальные правила стиля
    channel-telegram.md    ← правила для "Реклама на Юпитере"
    channel-instagram.md   ← правила для нового Instagram
  hot/
    HOT_MEMORY.md      ← активный контекст сессии (очищается)
```

## Как использовать

1. Открой новый чат с агентом
2. Прикрепи файлы в таком порядке:
   - `memory/cold/MEMORY.md` — читать первым
   - `memory/warm/WARM_MEMORY.md`
   - `memory/warm/TONE_OF_VOICE.md`
   - Нужный channel-файл (telegram или instagram)
3. Прикрепи `SKILL.md` — это инструкция для агента
4. Дай задачу: "Напиши пост для Telegram про X"

## Что делать с правками

Когда агент написал и ты что-то изменила — скажи агенту:
> "Залогируй: я изменила [оригинал] → [итог] потому что [причина]"

Агент запишет в `MEMORY.md` и потом не будет повторять ошибку.

## Файлы скилла

- `SKILL.md` — инструкция для агента (основной файл)
- `references/memory-structure.md` — схема всей структуры памяти
- `references/channel-template.md` — шаблон для нового канала
- `templates/` — стартовые шаблоны (уже заполнены в `memory/warm/`)
