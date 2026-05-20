# Mini Peltier AC - Circuit Diagrams & Schematics

## 1. Basic On/Off Circuit

### Circuit Diagram (Text Format)

```
┌─────────────────────────────────────────────────────────┐
│ AC Mains (110-240V)                                     │
└────────┬────────────────────────────────────────────────┘
         │
      [PSU 12V/15A]
         │
    ┌────┴────┐
    │          │
   GND        12V Out
    │          │
    └────┬─────┘
         │
      [Fuse]
       10A
         │
    ┌────┴──────────────┐
    │                   │
 [Switch]          [Fans in Parallel]
    │                   │
    │              ┌────┴────┐
    │              │         │
    │          [12V]      [12V]
    │           Fan1       Fan2
    │              │         │
    ├──────────────┴────┬────┘
    │                   │
  [+]                  [-]
   │                    │
[Peltier Module]        │
   │                    │
  [-]                   │
   │                    │
   └────────────────────┘
                │
               GND
```

### Component Connections

**Power Supply Side:**
- AC Input: 100-240V (PSU handles conversion)
- DC Output: 12V (red wire), GND (black wire)

**Protection:**
- Fuse: 10A fast-blow (between PSU and main circuit)
- Switch: Rated for 20A at 12V DC

**Peltier Module:**
- Positive (Red): Connected to switch output
- Negative (Black): Connected to GND/Ground rail

**Fans (Parallel Connection):**
- Both connected to 12V and GND rail
- Current drawn by fans: ~0.5A each
- Faster than Peltier on/off, always runs when power on

---

## 2. Advanced Circuit with Temperature Control

### Circuit Diagram

```
┌─────────────────────────────────────────────────────────┐
│ Temperature Sensor (DS18B20)                            │
│ Mounted on cold side                                    │
│ 3-Pin: GND | Data | 5V                                 │
└──────────────┬────────────────────────────────────────┘
               │ (One-Wire Digital Signal)
               │
        ┌──────┴──────┐
        │             │
      5V           Data Pin
        │             │ (GPIO3)
        │    ┌────────┘
        │    │
    ┌───┴────┴────────┐
    │ Arduino Nano    │ (ATmega328P)
    │ 5V Microcontroller
    │                 │
    │ PWM Output 3    │
    │ (Digital Pin 9) │
    └────────┬────────┘
             │ (PWM Signal ~1kHz)
             │
    ┌────────┴────────┐
    │  Gate Resistor  │
    │     10kΩ        │
    └────────┬────────┘
             │
    ┌────────┴────────┐
    │ MOSFET Gate     │
    │ (IRF520N)       │
    └────────┬────────┘
             │ (Logic Level)
             │
         [Drain]
          (Cathode)
             │
    ┌────────┴────────┐
    │  12V Power Rail │
    │    (from PSU)   │
    └────────┬────────┘
             │
          [Fuse]
           10A
             │
         [Fans]
          (Parallel)
             │
    ┌────────┴────────┐
    │ Peltier Module  │
    │   Positive      │
    │    Terminal     │
    └────────┬────────┘
             │
             │ (Source to GND)
    ┌────────┴────────┐
    │ MOSFET Source   │
    │  (Connected to  │
    │   GND through   │
    │   module ground)│
    └────────┴────────┘
             │
    ┌────────┴────────┐
    │ Peltier Module  │
    │   Negative      │
    │    Terminal     │
    └────────┬────────┘
             │
            GND
             │
    ┌────────┴────────┐
    │ Common Ground   │
    │ (PSU, Arduino,  │
    │  MOSFET, Circuit)
    └─────────────────┘
```

### Pin Connections

**Arduino Nano to Sensor (DS18B20):**
- Pin 1 (GND): Arduino GND
- Pin 2 (Data): Arduino GPIO3 (with 4.7kΩ pull-up to 5V)
- Pin 3 (VCC): Arduino 5V

**Arduino to MOSFET:**
- PWM Output (Pin 9): 10kΩ resistor → MOSFET Gate
- Arduino GND: MOSFET Source → Common GND

**MOSFET (IRF520N) to Peltier:**
- Gate: From Arduino PWM (via 10kΩ resistor)
- Drain: 12V rail (positive side)
- Source: Peltier negative (through positive terminal)
- Body Diode: Provides reverse current protection

---

## 3. PWM Control Circuit

### PWM Signal Overview

```
Duty Cycle 30%:
  ┌─┐   ┌─┐   ┌─┐
  │ │   │ │   │ │
  │ └─┬─┘ └─┬─┘ └─
  │   │     │
  └───────────── 

Period = 1ms (1kHz)
ON time = 0.3ms (30%)
OFF time = 0.7ms (70%)
Average voltage = 3.6V (30% of 12V)

Duty Cycle 50%:
  ┌───┐   ┌───┐
  │   │   │   │
  │   └─┬─┘   └─
  │     │
  └─────────────

Period = 1ms (1kHz)
ON time = 0.5ms (50%)
OFF time = 0.5ms (50%)
Average voltage = 6V (50% of 12V)

Duty Cycle 100%:
  ┌──────────────
  │
  │
  │
  └──────────────

Period = 1ms
ON time = 1.0ms (100%)
OFF time = 0ms
Average voltage = 12V (100% of 12V)
```

### MOSFET Switching Characteristics

| Duty Cycle | ON Time | Peltier Power | Cooling Output | ΔT Achieved |
|-----------|---------|---------------|----------------|------------|
| 20% | 0.2ms | 12W | 8W | 5°C |
| 30% | 0.3ms | 18W | 12W | 7°C |
| 50% | 0.5ms | 30W | 22W | 15°C |
| 70% | 0.7ms | 42W | 32W | 22°C |
| 100% | 1.0ms | 60W | 50W | 28°C |

---

## 4. Detailed Wiring Diagram

### Power Distribution

```
12V PSU Output
      │
      ├─ [Fuse 10A] ─┬─────────┬──────────────┐
      │              │         │              │
     GND            12V       12V            12V
                     │         │              │
                  [Fan1]   [Fan2]      [MOSFET Drain]
                     │         │              │
                     └────┬────┴──────────────┤
                          │                  │
                         GND             [TEC +]
                                            │
                                       [TEC -]
                                            │
                                           GND
```

### Full Circuit Connectivity

```
Component        Wire Color   Connection To   Wire Gauge
─────────────────────────────────────────────────────
PSU +12V         Red          Fuse (+)        14 AWG
PSU Ground       Black        Common GND      14 AWG
Fuse +           Red          Switch/Rail     14 AWG
Fuse -           Black        GND             14 AWG
Switch +         Red          Peltier +       14 AWG
Switch -         Black        GND             14 AWG
Fan1 +           Red          12V Rail        16 AWG
Fan1 -           Black        GND             16 AWG
Fan2 +           Red          12V Rail        16 AWG
Fan2 -           Black        GND             16 AWG
MOSFET Drain     Red          12V Rail        14 AWG
MOSFET Source    Black        Peltier -       14 AWG
TEC +            Red          Switch/MOSFET   14 AWG
TEC -            Black        GND             14 AWG
Arduino +5V      Red          Sensor +        18 AWG
Arduino GND      Black        Common GND      18 AWG
Arduino GPIO3    Orange       Sensor Data     18 AWG
Arduino PWM9     Green        MOSFET Gate     18 AWG
Sensor +         Red          Arduino +5V     18 AWG
Sensor GND       Black        Arduino GND     18 AWG
Sensor Data      Yellow       Arduino GPIO3   18 AWG
```

---

## 5. Safety Circuit Elements

### Fuse Protection

```
      12V PSU
         │
    [Fast-Blow]
     10A Fuse
         │
    (Breaks on >10A
     current draw)
         │
    Main Power Rail
```

**Fuse Calculation:**
- Max TEC current: 6A
- Max fan current: 1A
- Buffer: 3A
- **Total: 10A rating** ✓

### Reverse Polarity Protection (Optional)

```
        12V PSU
           │
      [Diode]
      1N4007
    (Anode to +)
         │
    ┌────┴────┐
    │          │
   GND    Main Rail
```

**Alternative: Correct Connector Polarity**
- Use keyed connectors (e.g., 5.5mm/2.1mm barrel with polarity key)
- Prevents accidental reverse connection

---

## 6. Temperature Control Logic

### Arduino Control Algorithm

```
SETUP:
├─ Initialize DS18B20 sensor on pin 3
├─ Configure PWM output on pin 9
├─ Set target temperature (default: 15°C)
├─ Set hysteresis: ±1°C
└─ Start serial monitor for debugging

LOOP (every 1 second):
├─ Read current temperature from sensor
├─ Display temperature on LCD (optional)
├─ Compare to setpoint
│
├─ IF (Temperature > Setpoint + 1°C)
│  └─ Increase PWM duty cycle (up to 100%)
│
├─ ELSE IF (Temperature < Setpoint - 1°C)
│  └─ Decrease PWM duty cycle (down to 0%)
│
└─ OUTPUT: PWM signal to MOSFET gate
```

### Setpoint Adjustment

```
Current Temp    Setpoint    ΔT      PWM Action
─────────────────────────────────────────────────
25°C            15°C        +10°C   Turn ON 100% (max cooling)
20°C            15°C        +5°C    Turn ON 70% (moderate cooling)
16°C            15°C        +1°C    Turn ON 30% (light cooling)
15°C            15°C        0°C     Standby/Hold current PWM
14°C            15°C        -1°C    Turn OFF 0% (stop cooling)
```

---

## 7. Multiple TEC Module Configuration

### Two TEC Modules in Parallel

```
        12V PSU
           │
        [Fuse]
           │
    ┌──────┴──────┐
    │             │
  [TEC1]        [TEC2]
    │             │
    ├─────┬───────┤
          │
    [Fans in Parallel]
          │
         GND
```

**Electrical Characteristics:**
- Both TECs receive full 12V
- Current from PSU: ~12A (6A per TEC)
- Cooling capacity doubles (combined)
- Total power: ~120W

### Multiple TEC Modules in Series

```
        12V PSU
           │
    [TEC1 +]
        │
    [TEC1 -]
        ├─[TEC2 +]
        │
    [TEC2 -]
        │
       GND
```

**Electrical Characteristics:**
- Each TEC receives ~6V
- Current from PSU: ~6A
- Cooling capacity reduced
- **Not recommended for this application**

---

## 8. Thermal Design Considerations

### Peltier Module Orientation

```
     Correct Installation:
     
         HOT SIDE (50-60°C)
              ↓
      ┌──────────────┐
      │  Heatsink    │
      │  + Fan       │
      └──────┬───────┘
             │
      [Thermal Paste]
             │
      ┌──────┴───────┐
      │   TEC Module │
      │   40×40×3.8  │
      └──────┬───────┘
             │
      [Thermal Paste]
             │
      ┌──────┴───────┐
      │ Cold Block   │
      │ Aluminum     │
      └──────┬───────┘
             │
        COLD SIDE (10-20°C)
             ↓
      [Insulated Chamber]
```

### Heat Flow Path

```
Hot Ambient Air (30°C)
        ↓
    [Air Flow]
        ↓
   [Heatsink Fins]
        ↓
  [Thermal Paste]
        ↓
   [TEC Hot Side]
      [Junction]
   [TEC Cold Side]
        ↓
  [Thermal Paste]
        ↓
   [Cold Block]
        ↓
    [Cooled Air] (15°C)
        ↓
  [Foam Insulation]
        ↓
  [Cooling Chamber Interior]
```

---

## 9. Soldering & Assembly Notes

### Critical Connections

1. **12V Power Rail**: Use 14 AWG wire, solder all components securely
2. **Ground Rail**: Use heavy ground buses for parallel returns
3. **TEC Connections**: Solder directly or use high-quality terminals
4. **PWM Signal**: Keep wires short and shielded to avoid noise

### Flux & Solder

- Use rosin-core solder (60/40 or lead-free equivalent)
- Apply flux for better wetting
- Clean excess flux with isopropyl alcohol
- Verify no cold joints or bridges

---

**Circuit Documentation Version**: 1.0  
**Last Updated**: May 2026
