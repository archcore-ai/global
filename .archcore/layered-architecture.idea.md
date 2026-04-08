---
title: "Layered Architecture: Intent API → Domain Flows → Typed Artifacts → MCP Primitives"
status: draft
tags:
  - "api-design"
  - "architecture"
---

## Idea

Четырёхуровневая архитектура Archcore, где каждый слой абстрагирует нижележащий:

### Layer 1 — Intent API

То, что видит большинство пользователей — высокоуровневые команды:

- `/document` — создать/найти документ
- `/plan` — спланировать работу
- `/decide` — принять и зафиксировать решение
- `/review` — провести ревью артефакта

### Layer 2 — Domain Flows

Внутренняя маршрутизация intent'ов по доменным трекам:

- **product-track** — продуктовые артефакты (prd, mrd, idea)
- **sources-track** — источники требований (strs, brs, urd)
- **iso-track** — стандарты и спецификации (srs, syrs, spec)
- **architecture-track** — архитектурные решения (adr, rfc, rule)

### Layer 3 — Typed Artifacts

Конкретные типы документов, создаваемые каждым треком:

prd, adr, mrd, strs, srs, brs, urd, syrs, rfc, rule, guide, doc, spec, idea, plan, task-type, cpat

### Layer 4 — MCP Primitives

Низкоуровневые операции над хранилищем:

- `create_document`
- `update_document`
- `add_relation`
- `list_documents`

## Value

- **Для пользователя** — не нужно знать типы документов и MCP-вызовы; достаточно intent'а (`/decide`)
- **Для domain flow** — инкапсуляция логики выбора типа артефакта и шаблона
- **Для системы** — единый набор MCP-примитивов, поверх которого строятся любые flow
- **Расширяемость** — новые треки и типы добавляются без изменения Intent API

## Possible Implementation

1. **Intent API** реализуется как набор skill'ов (slash-commands), каждый из которых:
   - определяет контекст (домен, цель)
   - выбирает подходящий Domain Flow
   - передаёт управление

2. **Domain Flows** — orchestration-логика (может быть skill или agent), которая:
   - задаёт уточняющие вопросы
   - выбирает тип артефакта
   - заполняет шаблон
   - вызывает MCP-примитивы

3. **Typed Artifacts** — уже реализованы как document types в Archcore с required sections

4. **MCP Primitives** — уже реализованы (`create_document`, `update_document`, `add_relation`, `list_documents`)

## Risks and Constraints

- **Сложность маршрутизации** — Layer 2 должен корректно определять домен по intent'у; ошибочная маршрутизация → неправильный тип артефакта
- **Overhead для простых случаев** — иногда пользователь точно знает, что хочет создать adr, и промежуточные слои только мешают
- **Поддержание согласованности** — при добавлении нового типа документа нужно обновить и flow, и intent API
- **Bypass** — опытные пользователи захотят обращаться напрямую к Layer 3/4, нужно это разрешать