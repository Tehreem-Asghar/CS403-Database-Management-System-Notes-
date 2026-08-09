# CS302 — Digital Logic & Design
## Lecture 23 se 45 tak — Complete Roman Urdu Guide (Exam Prep)

> Ye guide tumhari uploaded handout file se banayi gayi hai. Har lecture ka core concept, important points aur exam-relevant cheezein cover ki hain. Ghabrao mat — chalo shuru karte hain, topic by topic, aasan zaban mein.

---

## Lecture 23 — S-R Latch ki Applications, Edge-Triggered Flip-Flops, Master-Slave FF

### 1. S-R Latch ki Application (Switch Debouncing)
Jab koi mechanical switch (jaise keypad ka button) press karte hain, uske contacts thori der ke liye **vibrate/bounce** karte hain — matlab output voltage 1 aur 0 ke beech thodi der fluctuate karta hai pehle steady hone se pehle. Isko **switch bounce** kehte hain, aur ye digital circuit ko confuse kar sakta hai (ek press ko multiple presses samajh lega).

**Solution:** Switch ko ek **active-low S-R latch** ke through connect kar dete hain. Jab switch bounce ho raha ho, tab S=1, R=1 wali condition ban jati hai jisme latch apni **purani state hold** kar leta hai (change nahi karta) — is tarah bounce ka asar output pe nahi parta.

- **Burglar alarm example:** Jab door khulta hai, latch ka output set ho jata hai aur alarm bajta rehta hai jab tak reset switch dabaya na jaye — chahe door dobara band ho jaye.
- IC example: **74LS279** — isme 4 independent S-R latches hote hain.

### 2. Gated S-R Latch
Isme ek extra input hoti hai **EN (Enable)**. Jab tak EN = 1 na ho, S aur R ka koi asar output pe nahi hota (output apni previous state hold karta hai). EN=1 hone par hi latch normal S-R ki tarah kaam karta hai.

**Truth Table yaad rakho:**
| EN | S | R | Q(t+1) |
|---|---|---|---|
| 0 | x | x | Qt (no change) |
| 1 | 0 | 0 | Qt (no change) |
| 1 | 0 | 1 | 0 (Reset) |
| 1 | 1 | 0 | 1 (Set) |
| 1 | 1 | 1 | Invalid |

### 3. Gated D Latch
Agar S-R ke aage ek NOT gate laga ke S aur R ko aapas mein jod dein, to sirf ek hi input reh jati hai — **D**. Ab invalid state ka masla khatam ho jata hai kyunki S aur R kabhi ek sath 1 nahi ho sakte.
- Q(t+1) = D (jab EN=1)
- IC: **74LS75** (4 D-latches)

### 4. Edge-Triggered D Flip-Flop
Latch level-triggered hota hai (jab tak EN high hai, output change hota rehta hai), lekin **flip-flop sirf clock ke edge (0→1 ya 1→0) par** hi trigger hota hai. Isse timing zyada predictable hoti hai.
- **Positive edge-triggered:** Sirf clock ke low-to-high transition par output update hota hai.
- **Negative edge-triggered:** Sirf high-to-low transition par.

### 5. Edge-Triggered J-K Flip-Flop
J-K flip-flop, S-R jaisa hi hai lekin **invalid state nahi hoti** — jab J=1, K=1 ho to output **toggle** ho jata hai.

**Yaad rakhne wali Truth Table (Positive Edge):**
| J | K | Q(t+1) |
|---|---|---|
| 0 | 0 | Qt (no change) |
| 0 | 1 | 0 (Reset) |
| 1 | 0 | 1 (Set) |
| 1 | 1 | Toggle (Qt ka ulta) |

Ye table **bohat important hai, exam mein zaroor puchi jati hai.**

### 6. Asynchronous PRESET aur CLEAR
Ye inputs **clock signal ke bina hi** flip-flop ko turant ek fixed state mein le jati hain (isliye "asynchronous" kehlati hain — clock pe depend nahi karti).
- **PRE = 0** → Q = 1 (foran set)
- **CLR = 0** → Q = 0 (foran reset)
- Dono ko 1 rakhna zaroori hai normal (synchronous, J-K wale) operation ke liye.
- PRE=0 aur CLR=0 dono ek sath **allowed nahi** (invalid).

IC examples: **74HC74** (Dual D flip-flop), **74HC112** (Dual J-K flip-flop) — dono asynchronous inputs ke sath aate hain.

### 7. Master-Slave Flip-Flop
Purana design, do hisso mein bata hua — **Master** aur **Slave**, dono gated S-R latches hote hain. Master clock ke positive half mein data leta hai, Slave negative half mein output deta hai. Ye **pulse-triggered** hota hai (edge-triggered nahi). Aajkal obsolete hai, edge-triggered FF ne replace kar diya hai.

### 8. Flip-Flop ki Operating Characteristics (Important for MCQs)
1. **Propagation Delay (tPLH, tPHL):** Clock transition se le kar output change hone tak ka time.
2. **Set-up Time:** Clock edge se pehle input ko stable rehna kitni der chahiye.
3. **Hold Time:** Clock edge ke baad input ko stable rehna kitni der chahiye.
4. **Maximum Clock Frequency (fmax):** Sabse tez rate jis par FF reliably kaam kare.
5. **Pulse Width (tw):** Clock, preset, clear signals ki minimum duration.
6. **Power Dissipation:** P = Vcc × Icc

---

## Lecture 24 — Edge-Triggered D Flip-Flop ki Applications

D flip-flop ka use data ko **store** karne aur **format convert** karne ke liye hota hai. Do main applications:

### 1. Data Storage using D Flip-Flop
Jab kisi bus (jaise microprocessor bus) par data thori der ke liye available hota hai aur baad mein change ho jata hai, to us data ko D flip-flop mein **latch/store** kar lete hain taake baad mein use kar sakein.

### 2. Parallel-to-Serial Converter (Multiplexer-based)
Multiple D flip-flops aur ek multiplexer combine kar ke parallel data (jo sab bits ek saath available hain) ko **serial** form mein convert karte hain (ek-ek bit karke bhejna) — ye communication systems mein bohat use hota hai (jaise USB, UART waghera ka basic concept isi se milta julta hai).

---

## Lecture 25 — Asynchronous Preset & Clear Inputs (Detail)

Ye Lecture 23 ke concept ko continue/detail karta hai:

- **Synchronous inputs** (S, R, J, K, D) sirf **clock ke sath** kaam karti hain.
- **Asynchronous inputs** (PRESET, CLEAR) **bina clock ke** foran output change kar deti hain — inka use tab hota hai jab circuit ko ek **known starting state** mein set karna ho (power-on ke waqt).

**Truth Table:**
| PRE | CLR | Q(t+1) |
|---|---|---|
| 0 | 0 | Invalid |
| 0 | 1 | 1 |
| 1 | 0 | 0 |
| 1 | 1 | Normal (clocked) operation |

**Exam tip:** Yaad rakho — PRE aur CLR **active-low** hote hain (0 ka matlab activate).

---

## Lecture 26 — Timing Problems, Clock Skew, Race Condition, Asynchronous (Ripple) Counters

### 1. Timing Problems
Jab do flip-flops ek dusre se connected hote hain aur same clock share karte hain, to agar propagation delay aur hold time sahi match na ho to output unpredictable ho sakta hai.

### 2. Clock Skew
Jab **same clock signal** circuit ke different parts tak **alag-alag time** par pohanchta hai (wiring delay ki wajah se), to flip-flops asynchronously (galat waqt par) switch ho sakte hain — isko **Clock Skew** kehte hain. Solution: clock delays ko equalize karna.

### 3. Race Condition
Jab ek input change hone se **multiple internal signals** ek sath change hoti hain aur unka sequence circuit ke output ko affect karta hai — is se **glitches (short unwanted pulses)** ban sakte hain. Negative-edge triggered FF use kar ke isse avoid kiya ja sakta hai.

### 4. Counters — Introduction
- **Asynchronous (Ripple) Counter:** Sirf pehla flip-flop clock se connect hota hai, baaki flip-flops apna clock **pichle FF ke output se** lete hain. Isliye signal "ripple" (lehar ki tarah) hoti hai FF se FF tak.
- **Synchronous Counter:** Sab flip-flops **ek hi common clock** se connect hote hain — sab ek sath switch hote hain.

**3-bit Asynchronous Up-Counter:** Har FF ke J aur K dono 1 rakhe jate hain (toggle mode). Q output agle FF ke clock se connect hota hai.

**Problem with Ripple counters:** Har FF ka apna propagation delay hota hai, jo add hota jata hai. Zyada bits honge to total delay zyada ho jayega, jo high frequency par masla banata hai.

---

## Lecture 27 — Down Counters

**Up counter** 0 se maximum tak count karta hai, phir wapas 0 ho jata hai.
**Down counter** ulta chalta hai — maximum value se shuru ho kar 0 tak neeche aata hai, phir wapas maximum pe reset hota hai.

Asynchronous down-counter banane ka trick: Up-counter mein har FF ka clock **Q output** se liya jata hai; down-counter mein clock **Q' (complement) output** se liya jata hai. Bas itna hi farq hai!

**Up/Down dono banane ka concept:** Q ya Q' mein se konsa output agle FF ke clock ko chalata hai, ye decide karta hai counter up count karega ya down.

---

## Lecture 28 — Synchronous Decade Counter ka Timing Diagram

**Decade counter** = 0 se 9 tak count kar ke phir 0 pe wapas aa jata hai (Modulus-10, isliye "decade").

Is lecture mein **74x160**-type synchronous decade counter ka timing diagram detail se samjhaya gaya hai:
- Clock ke har positive edge par output change hota hai.
- Jab counter 9 (1001) tak pohanchta hai, ek **RCO (Ripple Carry Out)** signal generate hota hai jo agle counter (multi-digit counters banane ke liye, jaise ke Lecture 30 ke Digital Clock mein use hoga) ko trigger karta hai.
- **ENP/ENT** enable inputs counter ko enable/disable karne ke liye hote hain — cascading ke liye zaroori.

**Exam tip:** RCO ka role samjho — ye multi-digit counters ko connect karne ki key hai.

---

## Lecture 29 — Up/Down Counter

Ye counter ek control input (jaise UP/DOWN signal) ke zariye decide karta hai ke agla count **upar** jayega ya **neeche**.

- Agar UP/DOWN = 1 (Up mode): Q outputs FF ke clock ko drive karte hain.
- Agar UP/DOWN = 0 (Down mode): Q' outputs FF ke clock ko drive karte hain.

Ye do multiplexers (ya AND-OR logic) ke zariye implement hota hai jo select karte hain ke Q ya Q' agle stage ko jayega.

---

## Lecture 30 — Digital Clock

Ye ek **practical application** hai jisme multiple counters combine kiye jate hain ek real digital clock (ghari) banane ke liye:
- **Seconds counter** (00-59), **Minutes counter** (00-59), **Hours counter** (1-12 ya 0-23)
- Har counter apne **RCO (terminal count)** signal se agle counter ko enable karta hai — jaise seconds ka RCO minutes counter ko ek pulse deta hai.
- Units aur Tens counters ek sath mil kar 2-digit decimal number banate hain (jaise "59" seconds).

**Concept samjho:** Ye Lecture 28 ke decade counter aur cascading ka real-world application hai.

---

## Lecture 31 — Next-State Table (Sequential Circuit Design)

Ye **Sequential Circuit Design** ka pehla practical step hai. Design procedure:

1. **State Diagram** banao (problem statement se) — circles = states, arrows = transitions.
2. **Next-State Table** banao — is table mein likha jata hai ke **current state + input** ke hisab se **next state kya hoga**.
3. Is table se aage Boolean equations nikalte hain jo flip-flops ke input logic banane mein use hoti hain.

**Format samjho:**
| Present State | Input | Next State |
|---|---|---|
| S0 | 0 | S0 |
| S0 | 1 | S1 |
| ... | ... | ... |

Ye table **Flip-Flop Excitation Table** ke sath combine ho kar Boolean expressions deti hai (agle lectures mein).

---

## Lecture 32 — D Flip-Flop based Implementation & Flip-Flop Transition Table

Sequential circuit ko **D flip-flops** se implement karne ke liye:

1. **Next-State Table** se maloom karo ke har state variable ko next state mein kya value chahiye.
2. Kyunki **D flip-flop ka rule simple hai: D = Next State value** (D flip-flop apna input hi output bana deta hai next clock pe) — is liye D input equations seedha Next-State Table se nikal aati hain (Karnaugh Map ke zariye simplify kar ke).

**D Flip-Flop Transition Table:**
| Qt | Qt+1 | D |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

(Matlab D hamesha = Qt+1, koi complexity nahi — isiliye D-FF design mein sabse aasan hota hai.)

---

## Lecture 33 — State Assignment

Har state ko ek **unique binary code** dena hota hai (jaise S0=00, S1=01, S2=10...). Isko **State Assignment** kehte hain.

**Important rule:** State assignment aisi choose karo ke **ek state se dusri state jaate waqt kam se kam bits change hon**. Isse:
- Circuit **simpler** ban jata hai (kam gates lagte hain)
- **Glitches** kam hote hain
- Power consumption bhi kam hota hai

Ye ek design choice hai — same problem ko different state assignments se implement kiya ja sakta hai, lekin optimal assignment circuit ko efficient banati hai.

---

## Lecture 34 — Shift Register ki Types

Shift register = flip-flops ki chain jisme data ek FF se dusre FF mein **shift (khisak)** hota hai har clock pulse par. 4 main types:

1. **SISO (Serial In / Serial Out):** Data ek-ek bit karke andar jata hai, aur ek-ek bit karke bahar nikalta hai.
2. **SIPO (Serial In / Parallel Out):** Data serially andar jata hai, lekin sab bits ek sath (parallel) bahar nikaalte hain. IC example: **74HC164**.
3. **PISO (Parallel In / Serial Out):** Sab bits ek sath load hote hain, lekin bahar ek-ek karke serially nikalte hain. IC example: **74HC165** (isme CLK INH signal se shifting ko control karte hain).
4. **PIPO (Parallel In / Parallel Out):** Data parallel andar, parallel bahar.
5. **Bi-directional Shift Register:** Left ya Right dono taraf shift kar sakta hai (control input se select hota hai).

**Yaad rakhne ka tarika:** Naam mein pehla word = kaisay data **andar** ja raha hai, dusra word = kaisay **bahar** aa raha hai.

---

## Lecture 35 — Shift Registers ki Applications

Do main practical applications:

### 1. Parallel-to-Serial / Serial-to-Parallel Conversion
Data communication mein (jaise ek computer se dusre computer ko data bhejna) parallel data ko serial mein convert karke bhejna zaroori hota hai (kam wires lagti hain) — shift register ye kaam karta hai.

### 2. Keyboard Encoder
Shift registers keyboard ke scan/encode circuits mein bhi use hote hain — key presses ko serially read/encode karne ke liye.

---

## Lecture 36 — Example: 3-bit Up/Down Counter (D Flip-Flop based)

Pehle J-K flip-flop se ye counter implement kiya gaya tha (earlier lectures mein), ab **D flip-flop** se implement karna sikhaya gaya hai:

1. **D Input Table** banao (Present State, Next State ko map kar ke — Lecture 32 ka concept use karo).
2. **Karnaugh Map** se har D input ki simplified Boolean expression nikalo.
3. Un expressions se circuit design karo.

Ye pura Lecture 31-33 ke design procedure ka **practical worked example** hai — isko step-by-step samjho, exam mein full numerical question aa sakta hai.

---

## Lecture 37 — Reduced Input Latches (Elevator Controller) + Traffic Light Controller (State Diagram)

### 1. Elevator Controller — Latch Reduction
Elevator system ke sensors (REQ1, FLOOR1, OPEN button waghera) ke inputs ko latch mein store karna hota hai. Agar related signals (jaise floor 1 ke sab buttons) ko **ek hi latch** mein combine kar diya jaye to total latches ki tadaad kam ho jati hai — is se circuit simple aur saste (kam hardware) ban jata hai.

### 2. Traffic Light Controller — State Diagram (ABEL/GAL16V8)
Ye ek **classic exam example** hai — 8 states wala traffic controller (NSG, NSY, NSY2, NSR, EWG, EWY, EWY2, EWR — North-South Green/Yellow/Red aur East-West Green/Yellow/Red).

- State assignment 3 bits se hoti hai, aur **sirf ek bit** change hota hai state-to-state (Lecture 33 wala concept practically apply hua hai).
- **ABEL language** mein State Diagram likhi jati hai jisme `if...then...else goto` type statements hote hain traffic timer (STIME/LTIME) aur sensor inputs (NSSR/EWSR — North-South/East-West sensor request) ke hisab se next state decide karte hain.

**Concept samjho:** Ye real hardware description language (HDL) ka basic idea deta hai — GAL16V8 jaisi programmable chip mein ye logic "burn" (program) ki jati hai.

---

## Lecture 38 — Equation Definition & Characteristic Equations (State Machine Analysis)

### 1. Equation Definition (Traffic Controller continued)
Timer ko reset karne wali equation:
```
TMRST := (TRSTATE == NSY2) # (TRSTATE == EWY2);
```
(`#` ka matlab OR hai ABEL mein). Traffic lamps on/off karne ki equations bhi is tarah likhi jati hain — matlab har output ek Boolean function hai current state ka.

### 2. Characteristic Equations (Bohat Important — MCQs mein aata hai!)
Har latch/flip-flop ki ek "characteristic equation" hoti hai jo uska behavior define karti hai:

| Device | Characteristic Equation |
|---|---|
| S-R Latch | Qt+1 = S + R'Qt |
| D Latch / D Flip-Flop | Qt+1 = D |
| J-K Flip-Flop | Qt+1 = JQt' + K'Qt |

### 3. State Machine Analysis (Design ka ulta process)
- **Design:** Problem se circuit banate hain.
- **Analysis:** Already bane hue circuit se state diagram/table nikalte hain.

Steps: (1) Next-state aur Output functions nikalo (F aur G), (2) State/Output table banao, (3) State diagram draw karo.

---

## Lecture 39 — Memory Basics (RAM), Read/Write Operation, Static Memory Cell

### 1. Memory Organization
Memory ko **rows aur columns** ki grid ki tarah socho — har cell (intersection) ek bit store karti hai. Address do parts mein divide hoti hai jo row aur column select karti hai.

### 2. Read-Write Memory (RAM) ke Important Signals
- **Address lines:** Konsi location access karni hai batati hain.
- **Data lines:** Data read/write karne ke liye.
- **R/W̄ (Read/Write):** 1 = Read, 0 = Write (ya isके opposite, IC ke hisab se).
- **CS (Chip Select):** Chip ko activate karta hai.

### 3. Read Operation
Address diya jata hai → us location ka data DOUT (data output) pe available ho jata hai.

### 4. Write Operation
Address + Data diya jata hai + R/W̄ = Write mode → data us location mein store ho jata hai.

### 5. Static Memory Cell (SRAM)
Har bit ek **flip-flop based cell** mein store hota hai — jab tak power hai, data hold rehta hai (isliye "static"). Ye DRAM se fast hota hai lekin zyada transistors use karta hai (isliye expensive/bara hota hai per bit).

**16K x 8 Static RAM** jaisi chips is concept ka real example hain.

---

## Lecture 40 — Large Memories ko Decode Karna

Bari memory (jaise 16KB) ko access karne ke liye pura address ek sath decode karna practically mushkil hota hai (bohat zyada gates lagenge). Solution:

- Address ko **Row Address** aur **Column Address** mein split kar dete hain.
- **Row Decoder** ek row line ko activate karta hai.
- **Column Decoder** ek column line ko activate karta hai.
- Jahan row aur column dono select hoti hain, wahi memory location access hoti hai — ye ek **2D (two-dimensional) array** ki tarah organize hota hai, linear address ki jagah.

**Faida:** Kam decoding logic lagti hai bari memory ke liye — jaise 2D grid mein sirf N/2 + N/2 lines chahiye instead of N lines directly.

---

## Lecture 41 — Read aur Write Cycles

Bari memories (jinme address multiplexed hoti hai, jaise DRAM) mein 2 signals important hain:

- **RAS (Row Address Strobe):** Pehle row address ko latch karta hai.
- **CAS (Column Address Strobe):** Uske baad column address ko latch karta hai.

**Read Cycle:** RAS aur CAS ek ke baad ek activate hoti hain row/column address latch karne ke liye → phir data DOUT pe available ho jata hai.

**Write Cycle:** Same tarah address latch hoti hai, phir R/W̄ signal activate hoti hai aur data memory mein write ho jata hai (jo microprocessor se input hoti hai).

**Yaad rakho:** RAS pehle, CAS baad mein — is sequence ka order exam mein pucha ja sakta hai.

---

## Lecture 42 — Flash Memory Array

Flash memory bhi **rows aur columns** mein organize hoti hai, lekin har cell **MOS transistor** based hoti hai (floating gate technology — jo power off hone par bhi data hold karti hai, isliye "non-volatile").

- **Row line** har MOS transistor ke **Control Gate** se connected hoti hai.
- Ek byte store karne ke liye 8 aise cells (transistors), ek common row mein, activate hote hain.
- Flash memory ka bara faida: **non-volatile** hai (USB drives, SSDs isi technology pe based hain).

---

## Lecture 43 — LIFO Memory (Stack)

**LIFO = Last In, First Out** — jo data sabse aakhir mein daala jata hai, wahi sabse pehle nikalta hai (plates ke stack jaisa example — sabse upar wali plate pehle uthti hai).

### 1. Shift-Register based Stack
Jab naya data aata hai, purana data **push (neeche shift)** ho jata hai. Read karte waqt data **pull (upar shift)** hota hai.

### 2. RAM-based Stack (zyada practical)
Ek special register — **Stack Pointer Register** — hamesha stack ke **top** ka address store karta hai.
- **Push (write):** Data likho, phir Stack Pointer ko **increment** karo.
- **Pop (read):** Data top se read karo, phir Stack Pointer ko **decrement** karo.

Ye concept **programming/computer architecture** mein bhi bohat important hai (function calls, recursion waghera isi stack se implement hote hain).

### 3. Memory Map
Bari memory (jaise 1 MByte) ko different blocks mein divide kar
