# Qurb Content — SQLite language packs

Каждый язык хранится в одном SQLite-файле `translations_<code>.db`.

## Таблицы
- `metadata` — сведения о языковом пакете.
- `resources` — переводы всех разделов.
- `builtin_sections` — разделы, которые для арабского языка остаются встроенными в приложение.

## Разделы в `resources.section`
- policies
- quran
- dua
- azkar
- system
- holidays
- names99

## Компактность
`resources.data` хранит исходный ресурс как gzip BLOB. Поэтому база остаётся SQLite,
но крупные тексты (особенно Коран) не раздуваются как обычный несжатый SQLite TEXT.

После SELECT:
1. взять `data`;
2. распаковать gzip;
3. для `content_type=json` декодировать JSON;
4. для `markdown` читать как UTF-8 текст.
