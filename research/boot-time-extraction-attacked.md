# Якщо не константи — що взагалі залізо може дати WSM на самому початку?

**Статус: ВІДКРИТО, атаковано нижче.** Продовжує пряме питання
Volodymyr: константи відкладено ("в моїй мові будуть обов'язково, але
це відкладем") — питання загострилось до "якщо не константи, то що
взагалі моє залізо може витягнути з реального світу, на самому початку
запуску?" Це не нова гілка досліджень — це питання, поставлене напряму
до вже реально збудованого й перевіреного апаратного шару `wsm-os`, не
до гіпотетичного заліза.

## Учасники

```text
Автор:    Volodymyr
Роль:     власник проєкту WSM
Внесок:   питання -- якщо не константи, що можна витягнути на самому
          початку запуску

Автор:    Claude Sonnet 5 (Anthropic)
Роль:     дослідницький партнер WSM Foundations Research
Внесок:   інвентаризація реально доступного на цьому залізі, атака на
          кожен кандидат, інформаційно-теоретичний закриваючий
          аргумент; реальне читання TSC у handoff-probe.c, що
          перетворило аргумент про TSC на виміряний факт
```

## Реальна інвентаризація — що фактично досяжне на самому початку, без вигадок

Не гіпотетично — усе нижче вже реально `LIVE-CONFIRMED` чи
`STATIC-CONFIRMED` пробами цього репозиторію (`wsm-os/probe/`,
`wsm-os/hardware/bios-f22e/`), не список бажаного:

```text
1. Регістри CPU (CR0/CR3/CR4/EFER/RFLAGS/GDTR/RSP)  -- handoff-probe.c
2. Ревізія завантаженого мікрокоду (C2 статично, D6 живо)  -- BINARY-ANALYSIS.md
3. Карта фізичної пам'яті (121 реальний дескриптор)  -- handoff-probe.c
4. ACPI root, SMBIOS, GOP framebuffer  -- handoff-probe.c
5. RDSEED/RDRAND -- сирий апаратний шум ентропії  -- entropy-source-probe.c
6. CPUID: vendor string, family/model/stepping, сигнатура 0x000506E3 -- FIT-AND-STRUCTURE-ANALYSIS.md
7. Лічильник тактів TSC (RDTSC) -- реально прочитано, LIVE-CONFIRMED (нижче)
```

**Оновлення, того самого дня**: TSC реально дочитано —
`handoff-probe.c` тепер читає його двічі, з виміряною паузою між
читаннями (`Stall(100000)`, 100мс), і друкує дельту. Реальний,
зафіксований вивід під QEMU/OVMF/TCG (`wsm-os/probe/README.md`):

```text
TSC (RDTSC)    = t1=0x00000002D799C4D0 t2=0x00000002E7CD9A61 delta=271832465 cycles / 100ms
  implied rate = 2718 MHz-equivalent
```

Це не просто закриває прогалину в інвентаризації — це перетворює
структурний аргумент нижче (Кандидат "TSC") із чистого міркування на
реально виміряний факт: **одне сире значення TSC саме по собі нічого
не означає** — лише дельта між двома читаннями, що вже вимагає
sequence (два моменти) і порівняння (віднімання), дає щось
інтерпретоване (тут — приблизну тактову частоту). Застереження: цей
конкретний "2718 МГц" — таймінг емуляції TCG, не реальна частота
кремнію (хоч і підозріло близький до реальних ~2.7 ГГц i5-6400
власника) — див. `wsm-os/probe/README.md` для повного розбору, чому
цей збіг не варто читати як підтвердження.

Усе інше (SMM, ME/CSME, HECI) реально існує, але структурно недосяжне
для WSM з боку хоста, як уже задокументовано в
`wsm-os/hardware/CSME-ARCHITECTURE.md` — не тому, що WSM могло б це
прочитати й вирішило не читати, а тому що це окремий обчислювальний
домен.

## Атака: кожен кандидат, по черзі, тим самим стандартом

Не "чи цікаве це значення", а "чи можна його *отримати*, не імпортуючи
distinction/plurality/sequence, уже показані зламаними чи
co-primitive в `distinction-attacked.md` і `hypothesis-a-repetition.md`".

**Один сирий біт з фіксованої адреси (найменш, здавалось би, вимогливий
кандидат)**: щоб прочитати біт, потрібні (а) адреса — конкретна
локація, вирізнена з-поміж усіх інших можливих локацій = вже plurality
й distinction одночасно; (б) сам акт читання — подія, що відбувається
"тепер", після "до" = sequence; (в) результат — 0 чи 1 = вже дві
розрізнені можливості. **Найпростіший можливий вимір вимагає
distinction, plurality і sequence одночасно** — точно ту саму
комбінацію, що зламала і `REPEAT`, і `BRANCH`.

**TSC / лічильник тактів**: це буквально `REPEAT` уже реалізований у
кремнії — тally-конструкція, що інкрементується щотакт. Уже зламана в
Раунді 1 `hypothesis-a-repetition.md` (потребує індивідуації,
послідовності, і фатально ніколи не термінується без рішення-зупинки,
якого лічильник сам не вводить). Читання його поточного значення
додатково вимагає порівняння ("це значення пізніше за те") — теж уже
зламане. **Тепер емпірично підтверджено, не лише аргументовано**: див.
"Оновлення" вище — реальний прочитаний TSC на цьому залізі підтвердив
рівно це: одне значення саме по собі порожнє, лише дельта між двома
читаннями (sequence + порівняння) дає щось інтерпретоване.

**CPUID vendor string / сигнатура моделі**: найближче до "статичного
факту", не процесу — жодного лічення, жодного очікування. Але це
рядок — послідовність байтів, що вже вимагає (а) plurality (кілька
позицій байтів), (б) якийсь порядок між ними (навіть без часового
очікування, позиційна послідовність — все одно форма sequence), (в)
розрізнення між різними значеннями байтів. Розглядання його як ОДНОГО
цілого, не розкладеного на байти, зводиться до "цей конкретний
патерн присутній" — але навіть це твердження вимагає відрізнити цей
патерн від того, чим він НЕ є (усіх інших можливих патернів) — та сама
проблема relata/plurality, що майже фатально зламала `DISTINCTION` у
`distinction-attacked.md`.

**RDSEED-семпл сирого теплового шуму**: найбільш "фізично сирий" у
одному сенсі (справжній квантовий/тепловий шум, не обчислений), але
витягнення одного біта чи байта все одно вимагає тієї самої структури
адреса/читання/результат, що й Кандидат 1. Інтерпретація його як
"ентропії" чи "випадковості" додатково вимагає ймовірнісної рамки —
вже позначено як імпорт математики в `hardware-native-constants.md`.

**Сам факт "виконання відбувається"** (не конкретне значення, а гола
тривала подія, що CPU досі виконує наступну інструкцію): це не читання
значення взагалі — це найближче до того, чим WSM уже *є*, не до нового
факту, який WSM могло б *отримати*. `handoff-state.md` уже записав, що
"WSM починається після handoff" — сам факт виконання не новина, яку
треба видобути, це передумова того, що WSM взагалі існує в цій точці.
Це не п'ятий кандидат — це визнання, що бути `()`, яке вже отримало
керування, і "видобути новий факт із реальності" — різні категорії
питання.

## Закриваючий аргумент: інформаційно-теоретичний, не лише структурний

Є точніший спосіб сказати те саме, що вже виринало структурно в
кожному кандидаті вище. За означенням інформації Шеннона (1948) —
твердження несе інформацію (вміст, `content`) лише відносно розподілу
ймовірностей над **більш ніж одним** можливим результатом; подія з
єдиним можливим наслідком несе нуль інформації (`H = 0`), за
визначенням, не через якусь недосконалість виміру.

**Це означає, що сам пошук "змістовного апаратного видобутку без
plurality" логічно суперечливий, не просто емпірично важкий**: щоб
видобутий факт узагалі щось *значив* — відрізнявся від "нічого не
видобуто" — мусить існувати щонайменше дві розрізнювані можливості, з
яких сталася саме ця. Вимога "уникнути plurality" і вимога "отримати
щось змістовне" **несумісні за визначенням змісту**, не лише за
випадковим збігом усіх атакованих досі кандидатів.

## Вердикт

Це не "ми ще не знайшли правильний апаратний факт" — це радше
підтвердження, гостріше сформульоване: **проблема ніколи не була в
тому, ЩО видобувати із заліза** — константу, біт, такт, рядок CPUID,
семпл шуму. Проблема — сам акт видобутку будь-чого змістовного, для
будь-якої мети, вимагає точно тих самих примітивів
(distinction/plurality/sequence), які вже показано зламаними чи
co-primitive у `distinction-attacked.md` й `hypothesis-a-repetition.md`
задовго до того, як залізо взагалі увійшло в це дослідження.

Це не новий глухий кут — це підтвердження того самого, єдиного
відкритого питання, яке `handoff-state.md` вже тримає як єдине відкрите
з самого початку: "який найменший додатковий крок після `()`" — і
`unclaimed-state-not-void.md` уже назвав ту саму причину, чому WSM не
сміє мовчки успадкувати жодну апаратну семантику. Це дослідження не
знаходить нового шляху в обхід — воно показує, чому обхідного шляху,
ймовірно, не існує: кожна спроба видобутку, незалежно від цілі,
впирається в той самий, ще не розв'язаний примітив.

**Не прийнято як остаточне** — за тим самим стандартом, що й усе
попереднє: це не доведення неможливості (`proven minimal/impossible`
у драбині статусів `distinction-attacked.md`), лише атака на всі
конкретні кандидати, знайдені досі. Відкрите для контратаки: чи існує
форма "видобутку", що справді уникає всіх трьох одночасно, ще не
знайдена тут.

---

## If not constants, what can real hardware extract at all, at the very start? (English, secondary)

Direct follow-up to Volodymyr's question after constants were shelved
for the language itself. Real inventory of what's actually available at
early boot on this hardware (all already LIVE/STATIC-CONFIRMED
elsewhere in this repo): CPU registers, microcode revision, memory map,
ACPI/SMBIOS, RDSEED entropy, CPUID signature, TSC. TSC has since been
actually read, live, twice with a measured delay between reads
(`handoff-probe.c`, real output in `wsm-os/probe/README.md`) —
confirming empirically, not just structurally, that a single raw TSC
value is meaningless and only the delta (requiring sequence +
comparison) yields anything interpretable. Attacked each: a
single raw bit already requires address (plurality+distinction) +
read-event (sequence) + binary result (plurality) simultaneously — the
exact combination that broke both REPEAT and BRANCH. TSC is literally
REPEAT already implemented in silicon, already broken. CPUID string
still requires positional plurality and distinguishing this pattern
from all others it is not — the same relata/plurality problem that
nearly killed DISTINCTION. RDSEED shares the same address/read/result
structure, plus imports probability to call it "entropy." The bare fact
of ongoing execution isn't a new fact to extract at all — it's what WSM
already is at this point, not something it obtains. Closing argument:
by Shannon's own definition, information requires more than one
possible outcome — a "contentful extraction without plurality" is
logically incoherent, not just empirically hard, given what "content"
means. Verdict: the problem was never *what* to extract from hardware —
it's that extracting anything meaningful, for any target, requires
exactly the primitives (distinction/plurality/sequence) already found
broken or co-primitive well before hardware entered this research. Not
proof of impossibility — open to counter-attack. See the Ukrainian
version above for full detail.
