# `()` не означає відсутність стану — воно означає відсутність твердження WSM про стан

**Статус: ВІДКРИТО, не атаковано.** Новий кандидатний принцип,
запропонований після того, як реальна апаратна карта власника
(H170/i5-6400/ME 11, SMM, HECI — усе тепер `source-confirmed` у
`wsm-os/hardware/CSME-ARCHITECTURE.md`) була накладена на межу
`ExitBootServices()`. Продовжує `handoff-state.md` (пункт "Конкретне
представлення для `()` ще не обрано") і пряму лінію атак на
`DISTINCTION`/`PLURALITY` (`distinction-attacked.md`,
`physical-constants-as-given.md`) — не заміняє жодного з них.

## Учасники

```text
Автор:    GPT-5.6 Sol (OpenAI), передано через Volodymyr
Роль:     дослідницький партнер WSM Foundations Research
Внесок:   накладання реальної апаратної карти (CPU/PCH/ME/SMM/microcode/
          HECI) на межу ExitBootServices(), запропонований принцип

Автор:    Claude Sonnet 5 (Anthropic)
Роль:     дослідницький партнер WSM Foundations Research
Внесок:   перевірка апаратних тверджень першоджерелом (записано в
          wsm-os), перенесення філософського ядра сюди, відкрита атака
          нижче
```

## Апаратна мотивація (уже `source-confirmed` у `wsm-os`, тут лише контекст)

Після реального `ExitBootServices()` (`probe/exit-boundary-probe.c`,
раніше названий `RAW_CONTROL_REACHED`) машина не порожня. Одночасно й
далі існують: власний мікрокод CPU (реально `STATIC-CONFIRMED` як
ревізія `C2` у прошивці, `LIVE-CONFIRMED` як ревізія `D6` на працюючій
машині — сам факт розбіжності вже доводить `STATIC IMAGE ≠ LIVE MACHINE
STATE`), CR0/CR3/CR4/MTRR/APIC, System Management Mode (структурно
окремий від головного потоку виконання, `source-confirmed` через
офіційний даташит процесора — SMI перериває нормальне виконання,
виконує прошивку в SMRAM, повертається через RSM), і Intel ME —
апаратно окремий процесор із власною ізольованою SRAM і власною
мікроядерною ОС, чиї стани живлення явно незалежні від стану живлення
головного хоста (`wsm-os/hardware/CSME-ARCHITECTURE.md`, пряма цитата
Intel). Жодна з цих речей не зникає й не переходить під контроль WSM у
момент, коли WSM отримує керування.

## Запропонований принцип

Стара, неявна картина була:

```text
firmware -> nothing -> ()
```

Запропонована заміна:

```text
             величезна прихована структура машини
    (мікрокод, ME, SMM, DRAM, APIC, кеші, MTRR ...)
                          │
                          │  WSM отримує керування
                          ▼
                         ()
```

Формулювання: **`()` не означає відсутність стану. `()` означає
відсутність твердження WSM про стан.**

Тобто WSM не стверджує "машина фізично порожня", не стверджує "це
початок часу", не стверджує "немає попереднього стану", не стверджує
навіть "`()` = нуль". WSM стверджує лише: вся ця машина вже існує, і
WSM не описав її своєю мовою.

## Чому це не порушує двосторонню дисципліну, а загострює її

Перше враження може бути, що це новий канал контрабанди — той самий
гріх, що й раніше ("машина фізично має множинні комірки, отже WSM має
plurality", атакований і залишений відкритим у
`physical-constants-as-given.md`). Але сам принцип, як сформульовано,
рухається в **протилежному** напрямку: він не каже "апаратура має X,
отже WSM успадковує X". Він каже: **апаратура вже має ADD, branch,
порівняння, послідовність, регістри — і саме тому WSM не має права
мовчки успадкувати жодне з них**, лише тому, що вони фізично присутні.
Це та сама помилка, яку сам виклад називає явно:

```text
x86 має ADD
   ↓
математика вже визначена         ✗
```

Якщо цей принцип тримається, він не дає `wsm` нового матеріалу для
побудови — він **посилює** причину, чому `wsm-os` не сміє винаходити
можливості наперед, і чому `wsm` не сміє імпортувати апаратну
семантику. Це узгоджується з уже записаним правилом
(`handoff-state.md`, "двостороння дисципліна"), не суперечить йому.

## Відкрита атака, ще не проведена

Формулювання "відсутність твердження" замість "відсутність стану" саме
по собі не безкоштовне. Найгостріше питання, яке цей принцип ще не
пережив:

1. **Хто чи що не стверджує?** "WSM не стверджує X" уже передбачає
   суб'єкта, здатного стверджувати — того самого типу проблеми
   "спостерігача", яку `the-observer-gap.md` залишив невирішеною
   (Раунд 6: чесність versus структурна незалежність спостерігача —
   назване, не розв'язане). Чи "відсутність твердження" тихо ввозить
   той самий observer, якого решта проєкту вже намагається явно
   ввести, а не мовчки передбачати?
2. **"Твердження про стан" проти "стан"** — саме розрізнення цих двох
   речей уже вимагає distinction (одна річ ≠ інша річ) — точно той
   примітив, що вже показано можливо co-primitive із `PLURALITY` й не
   зведеним до чогось простішого (`distinction-attacked.md`). Якщо так,
   цей принцип не обходить стоячу циклічність distinction/plurality —
   він лише переформульовує її на новому словнику ("твердження" versus
   "стан"), не вирішуючи.
3. **Чи "відсутність" тут та сама операція**, що вже провалилась в
   `REPEAT`/`BRANCH`/`DISTINCTION` (заперечення, negation)? "Немає
   твердження" — форма заперечення, а заперечення вже explicitly
   провалило власну атаку в `distinction-attacked.md` (вектор
   observer/action) і в найпершому відкинутому кандидаті `first-step-
   candidate.md` (this/not-this уже має negation).

**Не прийнято.** Це кандидат для наступного раунду атаки за тим самим
стандартом, що й усе інше в цій лінії дослідження — гіпотеза, автор
якої не ставить власне найгостріше питання, не заслуговує довіри
незалежно від того, наскільки красиво вона звучить.

---

## `()` means absence of assertion, not absence of state (English, secondary)

Proposed after mapping the owner's real hardware (H170/i5-6400/ME 11,
SMM, HECI — all now source-confirmed in `wsm-os/hardware/CSME-
ARCHITECTURE.md`) onto the `ExitBootServices()` boundary: since the
machine plainly retains hidden state (microcode, ME, SMM, caches, APIC)
after WSM gains control, `()` cannot mean "the machine is physically
empty." Proposed reframing: `()` means the absence of any WSM assertion
about that state, not the absence of the state itself. This sharpens,
rather than violates, the existing two-way discipline — it explicitly
warns against inheriting hardware semantics (ADD, branch) just because
the substrate has them. Not yet attacked: does "WSM does not assert"
smuggle in an observer/subject (unresolved per `the-observer-gap.md`
Round 6)? Does distinguishing "assertion about state" from "state"
itself already require the distinction/plurality pair already found
possibly co-primitive and circular (`distinction-attacked.md`)? Is
"absence" here the same negation operation already broken elsewhere?
Open, not accepted. See the Ukrainian version above for full detail.
