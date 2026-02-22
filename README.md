# Jadlis-Advisor-Sales-Pitch

Claude Code plugin — Sales Pitch advisor по методологии **Sales Pitch: How to Craft a Story to Stand Out and Win** (April Dunford, 2023).

## Что делает

Проводит через 8-step sales pitch storyboard для создания **sales narrative**, помогающего покупателям понять, почему ваш продукт — лучший выбор:

> Setup (о рынке) → Follow-Through (о решении)

### 8 шагов + диагностика

| # | Фаза | Шаг | Результат |
|---|------|-----|-----------|
| 0 | — | Health Check | Симптом → рекомендованная стадия |
| 0.5 | — | Quick Positioning Check | 5 компонентов позиционирования (если нет positioning.local.md) |
| 1 | Setup | Insight | Уникальный market insight, указывающий на вашу ценность |
| 2 | Setup | Alternatives | Подходы (не компании) с pros/cons + discovery |
| 3 | Setup | Perfect World | Критерии идеального решения + «Right?» qualification gate |
| 4 | Follow-Through | Introduction | Market category, одно предложение |
| 5 | Follow-Through | Value Demo | Демо по value themes (макс 3), не feature tour |
| 6 | Follow-Through | Proof | Доказательства (8-tier hierarchy), matched к prospect |
| 7 | Follow-Through | Objections | Проактивные ответы на невысказанные возражения |
| 8 | Follow-Through | Ask | Рекомендация следующего шага, не вопрос |

## Установка

```bash
# Через маркетплейс
claude plugin install jadlis-advisor-sales-pitch@jadlis-advisors

# Или напрямую
claude plugin install beCyborg/Jadlis-Advisor-Sales-Pitch
```

## Использование

```
/jadlis-advisor-sales-pitch:advisor
```

Advisor активируется только при явном вызове (`disable-model-invocation: true`).

## Что Claude НЕ умеет без этого advisor'а

- **2-phase structure**: Setup (о рынке) → Follow-Through (о продукте). Claude по умолчанию начинает с продукта
- **Insight derivation**: обратная инженерия из differentiated value → unique market insight. Claude генерирует generic insights типа "AI меняет всё"
- **Approaches, not companies**: группировка конкурентов в подходы с pros/cons. Claude перечисляет отдельные компании
- **«Right?» qualification gate**: branching (yes/partial/no) ДО показа продукта. Claude не квалифицирует через согласие с критериями
- **Value Demo by themes (max 3)**: организация демо по ценности, не по меню продукта. Claude делает feature walkthrough
- **8-tier proof hierarchy**: от matching case study до awards, с подбором по prospect. Claude использует только "вот наши кейсы"
- **12 named anti-patterns**: Feature Walkthrough, Generic Insight, Vision Narrative, Problem/Solution Trap, Hero's Journey Trap, Discovery Void, Discovery as Interrogation, Setup Overrun, Undifferentiated Value, Proof Mismatch, Complicated Ask, Pitch Drift
- **Positioning→Pitch mapping**: 5 компонентов позиционирования → 8 steps storyboard
- **Soft dependency**: автоматически читает `positioning.local.md` от jadlis-advisor-positioning

## Источник

**Sales Pitch: How to Craft a Story to Stand Out and Win** — April Dunford (2023). 8-step storyboard, field-tested with 200+ technology companies. Сиквел Obviously Awesome (2019).

## Лицензия

Структура плагина и skill — MIT. Методология и фреймворки принадлежат автору книги.
