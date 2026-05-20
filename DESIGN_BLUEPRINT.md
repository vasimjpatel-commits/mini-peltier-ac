# Mini Peltier AC - Detailed Design Blueprint

## 1. System Overview

A mini air conditioner system using thermoelectric Peltier modules (TEC) for compact cooling applications. The system consists of power management, thermal transfer components, and optional temperature control.

## 2. Component Specifications

### 2.1 Peltier Module (TEC1-12706)

**Electrical Specifications:**
- Operating Voltage: 12V DC
- Maximum Current: 6A
- Maximum Power: 60W
- Resistance: ~2Ω

**Thermal Specifications:**
- Hot Side Maximum Temperature: 80°C
- Cold Side Minimum Temperature: -30°C (theoretical)
- Maximum ΔT: 65°C
- Cooling Capacity (Qc): 50W (at optimal conditions)

**Physical Specifications:**
- Dimensions: 40mm × 40mm × 3.8mm
- Weight: ~45g
- Material: Bismuth Telluride (Bi₂Te₃) semiconductor

### 2.2 Power Supply

**Specifications:**
- Input: AC 100-240V (or DC source)
- Output: 12V DC
- Minimum Current Rating: 15A (for 2× TEC modules + fans)
- Maximum Power: 180W
- Type: Switch-mode PSU (recommended)

### 2.3 Heatsinks & Thermal Management

#### Hot Side Heatsink

**Specifications:**
- Type: Aluminum CPU cooler with active fan
- Dimensions: 100mm × 100mm × 70mm (approx.)
- Fan: 80-120mm, 50-80 CFM
- Thermal Resistance: < 0.5°C/W (with fan)

**Recommended Models:**
- Intel LGA1150/1151 stock cooler
- Arctic Cooling Freezer series
- Be Quiet! Silent Wings
- Noctua NH-D14/D15

#### Cold Side Heatsink

**Specifications:**
- Type: Aluminum or copper block
- Dimensions: 60mm × 60mm × 20mm
- Thermal Resistance: ~1°C/W
- Optional: Small 40mm fan for air circulation

### 2.4 Thermal Interface Materials (TIM)

**Thermal Paste (Compound):**
- Recommended: Arctic Silver 5, Thermal Grizzly Kryonaut
- Application: 1-2mm pea-sized dots on each TEC face
- Thermal Conductivity: > 3 W/m·K

### 2.5 Insulation (Cooling Chamber)

**Material Selection:**
- Primary: Polystyrene foam (white expandable foam)
- Alternative: Polyurethane (PU) foam
- Thickness: 2-4 cm

**Thermal Resistance (R-value):**
- Polystyrene: R-1.4 per cm
- Polyurethane: R-2.5 per cm

## 3. Electrical Circuit Design

### 3.1 Basic Circuit

```
12V DC Power Supply
        │
      [10A Fuse]
        │
    [Toggle Switch]
        │
     ┌──┴──┐
     │     │
    TEC  Fans
  Module (Parallel)
     │     │
     └──┬──┘
        │
       GND
```

**Component Details:**

| Component | Specification | Function |
|-----------|---------------|----------|
| Fuse | 10A, 250V | Short circuit protection |
| Switch | 20A Toggle | Manual on/off control |
| TEC | 12V, 6A | Thermoelectric cooler |
| Fans | 12V, 0.2-0.5A | Heat dissipation |
| Wiring | 14 AWG (2.1mm²) | Main power |

### 3.2 Advanced Circuit (with Temperature Control)

```
Temperature Sensor (DS18B20)
        │ (1-Wire/Digital)
        ↓
Microcontroller (Arduino Nano)
  Logic 5V
        │ (Digital Output)
        ↓
MOSFET Gate (IRF520N)
(Logic Level)
        │
12V Power Rail
        │
    [Fuse 10A]
        │
  [MOSFET Drain]
        │
  [TEC Module]
        │
       GND
```

### 3.3 PWM Control (Variable Cooling)

For variable cooling power, use PWM (Pulse Width Modulation):

- 30% Duty: Light cooling (15W)
- 50% Duty: Medium cooling (30W)
- 100% Duty: Maximum cooling (60W)

## 4. Mechanical Assembly

### 4.1 Chamber Construction

```
Front View:
┌────────────────────────┐
│  Foam Insulation       │
│  ┌──────────────────┐  │
│  │ Cooled Chamber   │  │
│  │  (Interior)      │  │
│  │  20-50 liters    │  │
│  │                  │  │
│  │   Cold Air Out → │  │
│  │  ←─ Air Return   │  │
│  └──────────────────┘  │
└────────────────────────┘

Back View (Components):
┌────────────────────────┐
│ [Hot Heatsink + Fan]   │ ↑ Heat Exhaust
│                        │
│ [TEC Module]           │
│                        │
│ [Cold Heatsink]        │
│                        │
│ [Insulated Chamber] → || → Cooled Air
└────────────────────────┘
```

### 4.2 Assembly Steps

**Step 1: Prepare Heatsinks**
- Clean all surfaces with isopropyl alcohol
- Wipe with lint-free cloth
- Allow to dry completely

**Step 2: Mount Peltier Module**
- Apply thermal paste to hot side
- Press TEC firmly onto hot-side heatsink
- Secure with thermal adhesive or mechanical clamp

**Step 3: Mount Cold Side**
- Apply thermal paste to cold side of TEC
- Mount cold block with mechanical clamp
- Ensure firm contact (critical for performance)

**Step 4: Install Fans**
- Mount hot-side fan on heatsink
- Orient fan for outward airflow
- Secure with vibration dampeners

**Step 5: Wire Electrical System**
- Connect 12V positive to fuse
- Connect fuse to switch
- Connect switch to TEC positive terminal
- Connect TEC negative to ground
- Connect fans in parallel to 12V rail

**Step 6: Insulate Chamber**
- Cut foam pieces to size
- Glue foam around cooling chamber
- Seal all gaps with expanding foam or tape
- Ensure cold block is accessible inside chamber

**Step 7: Testing & Validation**
- Power on system
- Verify hot side reaches 50-60°C
- Verify cold side drops to 10-20°C
- Check for condensation
- Monitor power consumption

## 5. Performance Specifications

### 5.1 Cooling Capacity

| Current | Power | Cooling Power | ΔT Achieved |
|---------|-------|---------------|------------|
| 2A | 24W | 15W | 8°C |
| 3A | 36W | 35W | 15°C |
| 4A | 48W | 45W | 22°C |
| 5A | 60W | 50W | 28°C |
| 6A | 72W | 48W | 30°C |

**Optimal Operating Point:** ~5A, ~60W

### 5.2 Heat Dissipation Requirements

**Hot Side Heat Load:**
```
Q_hot = Q_cold + P_input
Q_hot = 50W + 60W = 110W (at optimal)
```

**Target Temperatures:**
- Ambient: 30°C
- Hot side heatsink: 45°C (with active cooling)
- TEC hot side: 45°C
- TEC cold side: 20°C (target)
- Cold chamber interior: 15°C final

## 6. Thermal Calculations

### 6.1 Steady-State Heat Flow

**Thermal Resistance Network:**

```
Ambient (30°C)
      ↓
[R_heatsink = 0.5°C/W]
      ↓
[R_TEC_junction ≈ 0.2°C/W]
      ↓
[Peltier Effect = ΔT]
      ↓
[R_TEC_junction ≈ 0.2°C/W]
      ↓
[R_cold_block = 1°C/W]
      ↓
[R_chamber_insulation ≈ 2°C/W]
      ↓
Cold Interior (~15°C)
```

### 6.2 Energy Balance

**Power Flow:**
```
Input Electrical Power: 60W
  ↓
TEC Module Conversion:
  - Cooling generated: 50W (endothermic side)
  - Heat generated: 70W (exothermic side)
  - Efficiency: 83% (of input becomes cooling)
```

**Coefficient of Performance (COP):**
```
COP = Q_cold / P_input
COP = 50W / 60W = 0.83

Compared to:
- Ideal refrigeration (Carnot): COP = 10-15
- Real compressor AC: COP = 2-4
- Peltier module: COP = 0.5-1.0
```

## 7. Design Variants

### 7.1 Variant A: Minimal Setup

**Use Case:** Spot cooling, small desk space

**Components:**
- 1× TEC1-12706
- 1× Small heatsink + 40mm fan (hot)
- 1× Cooling block (cold)
- Simple on/off switch
- Basic insulation (1-2cm foam)

**Performance:** ΔT ~ 12°C, Power ~ 60W

### 7.2 Variant B: Standard Setup (Recommended)

**Use Case:** Personal cooling, small room

**Components:**
- 2× TEC1-12706 (in parallel)
- 2× CPU coolers (hot sides)
- 2× Cooling blocks (cold sides)
- Temperature controller (W1209)
- Good insulation (3-4cm foam)

**Performance:** ΔT ~ 20°C, Power ~ 120W

### 7.3 Variant C: Advanced Setup

**Use Case:** High-performance cooling, room AC

**Components:**
- 4-6× TEC modules
- Water cooling loop on hot side
- Arduino-based PWM controller
- Humidity sensor & drainage system
- Heavy insulation (4-6cm foam)

**Performance:** ΔT ~ 25°C, Power ~ 240-360W

## 8. Safety & Protection

### 8.1 Electrical Safety

- **Fuse Rating**: 10A (fast-blow recommended)
- **Wire Gauge**: 14 AWG minimum (2.1mm²)
- **Connector Type**: Proper terminals, no exposed contacts
- **Insulation**: All live wires must be insulated

### 8.2 Thermal Safety

- **Temperature Monitoring**: Optional but recommended
- **Over-temperature Shutdown**: Cut power if T > 70°C
- **Hot Surface Warning**: Label hot-side heatsink
- **Condensation Management**: Drain holes, moisture barriers

### 8.3 Power Safety

- **Voltage Check**: Verify 12V ± 0.5V
- **Current Limits**: Don't exceed 6A per TEC
- **Reverse Polarity Protection**: Use diode or connector polarity key

## 9. Testing & Validation

### 9.1 Pre-Operation Checks

- [ ] Verify 12V DC at power supply terminals
- [ ] Check continuity of all connections
- [ ] Ensure proper thermal paste application
- [ ] Verify fan orientation (exhaust away from chamber)
- [ ] Confirm insulation sealing

### 9.2 Initial Power-On Test

1. **No-Load Test** (just power, no TEC):
   - Verify 12V at switch output
   - Check current draw of fans alone (~0.5A)

2. **TEC Load Test** (TEC + fans):
   - Observe current draw (should be 6-8A)
   - Monitor hot-side temperature rise
   - Measure cold-side temperature drop
   - Check for unusual noise or vibration

3. **Thermal Validation**:
   - Hot side should reach 45-60°C within 5 minutes
   - Cold side should drop to 15-25°C within 10 minutes
   - Interior chamber should cool within 15-20 minutes

### 9.3 Performance Metrics

- **Cooling Power**: Measure actual ΔT achieved
- **Power Consumption**: Check current draw
- **Efficiency**: Calculate COP
- **Response Time**: Measure cool-down rate
- **Steady-State**: Verify stable operation for 30 minutes

## 10. Maintenance & Troubleshooting

### 10.1 Regular Maintenance

- **Weekly**: Check fan operation, inspect for dust
- **Monthly**: Clean heatsink fins, verify all connections
- **Quarterly**: Replace thermal paste if needed, inspect for corrosion
- **Annually**: Full system inspection, thermal resistance re-measurement

### 10.2 Common Issues

| Issue | Symptom | Solution |
|-------|---------|----------|
| **No cooling** | Cold side = Ambient | Check polarity, verify TEC connection |
| **Weak cooling** | ΔT < 8°C | Improve heatsink contact, clean fins |
| **Excessive heat** | Hot side > 70°C | Increase fan speed, improve airflow |
| **Condensation** | Water inside chamber | Improve insulation, add drainage |
| **High power draw** | >10A at 12V | Reduce voltage or add resistor |

---

**Document Version**: 1.0  
**Last Updated**: May 2026
