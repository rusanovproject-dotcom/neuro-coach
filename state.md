# Потолок: держать ≤80 строк, курируемо — это якоря-курсоры, НЕ журнал. Единственный горячий файл фикса без жёсткого лимита иначе пухнет молча.

last_weekly: null            # последняя свёрнутая неделя (ISO). Двигает WEEKLY после ревью
last_monthly: null           # последний свёрнутый месяц. Двигает MONTHLY-разбор
last_capture: null           # дата последней записи дня. Двигает CAPTURE/EVENING; питает proactive (тишина)
cold_start: true             # true первые ~2 недели — «данных мало, не выдумываю паттерны». Снимает first-session на ~14 день
onboarded_at: null           # дата завершения first-session. Ставит first-session
current_week: null           # текущая ISO-неделя, напр. 2026-W21. Двигает MORNING/контур недели
week_planned: false          # зафиксированы ли фокусы недели. Ставит планирование недели (пн), легитимно остаётся false у хаотика
relationship_phase: знакомство   # знакомство / углубление / рабочая / прорыв / пересмотр. Двигают DEEP/WEEKLY по мере дуги
wheel_baseline: null         # разовый снимок Wheel of Life из онбординга. Ставит first-session, дальше не трогается
big_contract: null           # большой контракт: над чем работаем 3 месяца. Ставит first-session, пересматривает DEEP/WEEKLY/GOALS. Каноничен ТОЛЬКО здесь; goals.md «3 месяца» держит лишь декомпозицию к месяцам, не копию текста (без дублей — нечему рассинхрониться)
last_goals_review: null      # дата последней постановки/пересмотра целей (навык goal-setting). null = каскад в goals.md ещё не ставили. Питает graceful в MORNING + приглашение в MONTHLY + проактив «цели не поставлены»
task_source: internal        # где живут задачи. дефолт internal = внутри коуча (daily + goals), внешний источник опционален. опции: notion / github / file / свой — только если человек подключил. НЕ прибито к Notion

# --- проактивность (для MVP-транспорта: cron + тихие часы + лимит 1/день; сам код cron — отдельный компонент) ---
timezone: null               # таймзона человека (из profile), для всех расписаний. напр. Asia/Novosibirsk
last_proactive: null         # дата последней ИНИЦИАЦИИ коуча (любой) — лимит 1/день
last_proactive_kind: null    # что слал последним (morning/evening/silence/loop...) — для разнообразия
last_inbound_at: null        # когда человек писал последний раз (ISO) — питает детектор тишины
morning_ping_at: "08:30"     # время утреннего пинга (из profile)
evening_ping_at: "21:30"     # время вечернего пинга
quiet_hours: "23:00-07:30"   # тихие часы — НЕ инициировать контакт
vacation_until: null         # дата ISO или null — пауза проактива до даты
