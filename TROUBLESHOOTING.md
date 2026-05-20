# Mini Peltier AC - Troubleshooting Guide

## Quick Diagnosis Table

| Symptom | Likely Cause | Fix | Priority |
|---------|-------------|-----|----------|
| No cooling (interior = ambient) | Reversed polarity, thermal paste, contact issue | Check polarity, reapply paste | 🔴 HIGH |
| Weak cooling (ΔT < 8°C) | Poor heatsink contact, blocked fins, weak fan | Clean fins, increase fan airflow | 🟡 MEDIUM |
| Excessive heat (hot side > 70°C) | Inadequate heat dissipation | Add extra fan, improve airflow | 🔴 HIGH |
| High power consumption (>8A) | Thermal paste over-applied, component damage | Reduce paste, check TEC | 🟡 MEDIUM |
| Condensation inside chamber | Poor insulation sealing | Seal gaps, add drainage | 🟡 MEDIUM |
| Module won't turn on | Power connection issue, fuse blown | Check wiring, test fuse | 🔴 HIGH |
| Unusual noise | Loose components, fan vibration | Tighten fasteners, add dampers | 🟢 LOW |
| System shuts down suddenly | Thermal protection, power issue | Check temperature, PSU | 🔴 HIGH |

---

## Problem 1: No Cooling Achieved

### Symptoms
- Interior temperature equals ambient temperature
- Cold block remains at room temperature
- No temperature drop over 30+ minutes

### Diagnosis Steps

**Step 1: Verify Power Connection**
```
Multimeter Test:
1. Measure voltage at TEC positive terminal (switch ON)
   Expected: 12V ± 0.5V
   If 0V: Check switch, fuse, wiring
   If 12V: Continue to step 2

2. Measure voltage at TEC negative terminal
   Expected: 0V (reference to ground)
   If not 0V: Check ground connection
```

**Step 2: Verify Current Draw**
```
Multimeter Test (Ammeter mode):
1. Place ammeter in series with fuse
2. Turn switch ON
3. Expected reading: 6-8A
   If 0A: TEC not drawing current → open circuit
   If < 2A: Low current → possible open internal connection
   If > 10A: Over-current → short circuit (STOP, check for damage)
```

**Step 3: Check Polarity**
```
Visual Inspection:
1. Locate TEC module red and black wires
2. Red wire = Positive (+12V)
3. Black wire = Ground (0V)

If reversed:
- Red connected to ground
- Black connected to 12V
- Module runs backwards (hot and cold sides swap)
- Result: no noticeable cooling (heat is pumped UP, not down)

Fix: Disconnect TEC power, swap connections
```

**Step 4: Check Thermal Interface**
```
Visual Inspection:
1. Remove heatsink (carefully)
2. Inspect TEC hot side for thermal paste
   - Excessive: Large globules, paste squeezed out
   - Insufficient: Bare spots visible
   - Correct: Thin, even coverage

3. Check cold block contact
   - Any gaps visible = poor contact
   - Paste dried or absent = reapplication needed

Fix: Clean surfaces with IPA, reapply thermal paste
```

### Solutions

**If Polarity is Wrong:**
1. Turn OFF and unplug PSU
2. Wait 30 seconds for discharge
3. Swap red and black wires at TEC terminals
4. Verify connections with multimeter
5. Power ON and test

**If Thermal Paste is Poor:**
1. Turn OFF system
2. Allow to cool (30 minutes)
3. Remove heatsink carefully
4. Clean TEC and heatsink bases:
   - Wipe with isopropyl alcohol
   - Use lint-free cloth
   - Air dry completely
5. Reapply thermal paste (thin, even layer)
6. Reinstall heatsink with firm, even pressure
7. Test system

**If Connection is Loose:**
1. Check all solder joints with multimeter (continuity test)
2. Resolder any cold joints
3. Verify no broken wires
4. Test system

---

## Problem 2: Weak Cooling (ΔT < 8°C)

### Symptoms
- System cools but very slowly
- Final interior temperature only 5-8°C below ambient
- Takes > 30 minutes to reach steady state

### Diagnosis Steps

**Step 1: Check Heatsink Condition**
```
Visual Inspection:
1. Look at heatsink fins (both sides)
2. Check for dust accumulation
3. Feel for clogged fins (should feel open)
4. Listen to fan noise (should be audible)

Expected:
- Fins should be visible between layers
- Minimal dust
- Smooth airflow
- Fan spinning at constant speed
```

**Step 2: Measure Hot-Side Temperature**
```
IR Thermometer Test:
1. Wait for system to run 10 minutes
2. Measure heatsink base temperature
   Expected: 45-60°C
   If < 40°C: Fan working too well (unusual) or low current
   If > 70°C: Inadequate cooling → see Problem 3
```

**Step 3: Check Fan Operation**
```
Visual/Audio Test:
1. Listen for fan noise (should hear slight hum)
2. Place hand near fan outlet (should feel strong breeze)
3. Verify fan speed hasn't decreased
4. Check for vibration or unusual sounds

If fan not running:
- Check 12V connection to fan terminals
- Test fan in isolation (connect directly to PSU)
- If fan still won't spin: replace fan
```

**Step 4: Verify Insulation Effectiveness**
```
Temperature Test:
1. Run system 20 minutes to reach steady state
2. Measure interior temperature
3. Measure exterior foam temperature at multiple points
4. If exterior is warm (> 25°C): insulation is leaking
5. Mark warm spots on foam

Heat leakage indicates:
- Gaps in foam coverage
- Poor foam density
- Air circulation path
```

### Solutions

**If Heatsink is Dirty:**
1. Power OFF system and unplug
2. Use compressed air to blow out dust from fins
   - Hold nozzle perpendicular to fins
   - Use short bursts (avoid liquid discharge)
3. Use soft brush if compressed air insufficient
4. Test cooling performance

**If Heatsink Contact is Poor:**
1. Remove heatsink
2. Inspect cold side TEC contact
3. Reapply thermal paste (see Problem 1 solution)
4. Ensure heatsink sits flush
5. Test with multimeter (zero resistance between hot side surfaces)

**If Fan Speed is Low:**
1. Check fan voltage (should be 12V)
2. If voltage is low (< 10V): power supply issue
3. If voltage is correct but fan slow: replace fan

**If Insulation is Leaking:**
1. Identify warm spots (exterior temperature > 25°C)
2. These indicate foam gaps or voids
3. Add more foam to these areas
4. Seal with expanding foam or tape
5. Reseal all edges and corners

---

## Problem 3: Excessive Heat (Hot Side > 70°C)

### Symptoms
- Hot-side heatsink very hot to touch (> 65°C)
- Potential thermal runaway
- Fan working hard but can't cool down
- Possible smell of burning

### **⚠️ CRITICAL: Safety Issue**

This indicates inadequate heat dissipation and risk of TEC module damage.

### Immediate Actions

1. **TURN OFF SYSTEM IMMEDIATELY**
2. Allow 10 minutes to cool
3. Inspect for:
   - Blocked heatsink fins
   - Non-functioning fan
   - Thermal paste issues
4. Address issue before restarting

### Diagnosis Steps

**Step 1: Verify Fan is Running**
```
Visual Test:
1. With system OFF, spin fan blade by hand
   - Should rotate freely
   - If stuck: replace fan
   - If stiff: bearing damage

2. Power ON and listen
   - Should hear fan immediately
   - If no sound: fan not receiving power
   - Check 12V connection

3. Place hand near fan output
   - Should feel strong airflow
   - Weak flow: fan failing
```

**Step 2: Check Ambient Temperature**
```
Environmental Test:
1. Measure room temperature with thermometer
2. Note if room is particularly warm (> 35°C)
3. If room is hot, system performance decreases
4. Improvement: Use AC in room or relocate system
```

**Step 3: Inspect Heatsink Mounting**
```
Physical Test:
1. Gently push on heatsink (power OFF)
   - Should not move or rock
   - Any movement = loose fasteners
2. Check all mounting screws (power OFF)
   - Should be snug (not over-tight)
   - Tighten if loose
3. Verify no gaps between heatsink and TEC
```

### Solutions

**If Fan is Not Running:**
1. Check 12V connection at fan terminals
   - Measure voltage (should be 12V)
   - If 0V: check wiring, fuse, connection
2. Resolder connections if needed
3. Test fan by connecting directly to PSU (verify fan works)
4. If fan still won't run: **replace fan**

**If Heatsink is Dirty:**
1. Power OFF, wait to cool completely (15+ minutes)
2. Use compressed air to clean fins thoroughly
3. Check for clogs (use soft brush if needed)
4. Ensure airflow path is clear
5. Test cooling performance

**If Heatsink Contact is Loose:**
1. Power OFF, cool completely
2. Locate heatsink fasteners
3. Check each one:
   - Quarter-turn tighter if loose
   - Do NOT over-tighten (can crack TEC)
4. Verify firm, even contact all around
5. Test system

**If Thermal Paste is Applied Incorrectly:**
1. Power OFF, cool completely
2. Remove heatsink carefully
3. Inspect paste application
4. If over-applied: remove excess with card
5. If under-applied: reapply with thin layer
6. Reinstall heatsink

**If System is Inadequately Designed:**
1. Upgrade to larger/higher-performance heatsink
2. Add secondary fan to heatsink
3. Consider water cooling for hot side
4. Reduce TEC current (lower duty cycle if using PWM)

---

## Problem 4: Condensation/Water Inside Chamber

### Symptoms
- Droplets forming inside cooling chamber
- Water pooling at bottom
- Moisture on cold block
- Possible interior damage from water

### Physics Explanation

```
At 15°C interior temperature:
Saturation humidity drops significantly

Warm ambient air (30°C, normal humidity 60%)
  Contains: 15.4g water vapor per m³

Cooled to 15°C
  Saturation: 6.4g water vapor per m³
  Excess: 15.4 - 6.4 = 9g/m³ condenses as liquid

Result: Water droplets form on cold surfaces
```

### Solutions

**Option 1: Add Drainage (Recommended)**
1. Drill small hole (6-8mm) at lowest point of chamber
2. Insert small tube (silicone or plastic)
3. Route tube to collection container outside chamber
4. Test by introducing moisture
5. Verify water drains properly

**Option 2: Improve Sealing**
1. Reduce air infiltration (less warm moist air enters)
2. Check foam insulation for gaps
3. Seal with foam sealant or duct tape
4. Reduce condensation rate
5. Note: Still need drainage for residual moisture

**Option 3: Dehumidification**
1. Place silica gel packets inside chamber
2. Replace packets when saturated
3. Alternative: small battery-powered dehumidifier
4. Monitor and maintain

**Option 4: Reduce Cooling (Trade-off)**
1. Raise setpoint temperature (e.g., 18°C instead of 15°C)
2. Reduces condensation rate
3. Trade-off: Less cooling
4. Only if critical issue

### Maintenance

**Weekly:**
- Check for water accumulation
- Empty collection container if used

**Monthly:**
- Clean silica gel (dry in oven) or replace
- Inspect for mold growth

---

## Problem 5: System Won't Power On

### Symptoms
- No lights on PSU
- System completely dead
- No fans running

### Diagnosis Steps

**Step 1: Check AC Power**
```
Electrical Test:
1. Plug AC cable into different outlet
2. Use multimeter to verify outlet has power
3. Check if outlet is controlled by a switch (turned off?)
4. If no power at outlet: electrical issue (not system)
```

**Step 2: Test PSU**
```
Multimeter Test:
1. Unplug AC from PSU
2. Wait 30 seconds
3. With multimeter set to DC voltage
4. Connect probes to PSU 12V output terminals
5. Plug in AC
6. Expected reading: 12V
   - If 0V: PSU defective → replace
   - If 12V: Continue to step 3
```

**Step 3: Check Fuse**
```
Visual/Multimeter Test:
1. Locate fuse in circuit
2. Visual inspection:
   - Good fuse: visible metal filament
   - Blown fuse: filament appears broken/melted
3. Multimeter test (ohm mode):
   - Good: shows 0Ω
   - Blown: shows infinite Ω (no continuity)
4. If blown: replace with new 10A fuse
```

**Step 4: Check Switch**
```
Multimeter Test:
1. Measure voltage before switch (should be 12V with no load)
2. Measure voltage after switch
   - Switch OFF: should be 0V
   - Switch ON: should be 12V
   - If both 0V: switch may be stuck OFF
3. Toggle switch back and forth several times
4. Verify it clicks and engages
```

### Solutions

**If Outlet Has No Power:**
- Use different outlet
- Check circuit breaker
- Call electrician if unsure

**If PSU is Defective:**
- Replace PSU with equivalent 12V/15A unit
- Verify polarity before connecting

**If Fuse is Blown:**
1. Remove blown fuse carefully
2. Note current rating (should be 10A)
3. Insert new 10A fast-blow fuse
4. Power ON and test
5. If new fuse blows immediately: short circuit problem
   - Do NOT keep replacing fuses
   - Investigate short (check wiring)

**If Switch is Faulty:**
- Replace toggle switch with equivalent 20A-rated
- Verify connections before powering on

---

## Problem 6: System Shuts Down Unexpectedly

### Symptoms
- System runs for few minutes then stops
- PSU might reset/cycle
- Fans suddenly stop

### Likely Causes

1. **Thermal Overload Protection**
   - Hot-side temperature exceeds limit (usually 75-80°C)
   - PSU has built-in thermal protection
   - Solution: See Problem 3 (excessive heat)

2. **Over-current Protection**
   - Current draw exceeds PSU limit
   - PSU shuts down to protect
   - Solution: Check for short circuit

3. **Loose Connection**
   - Intermittent contact causing arcing
   - Creates resistance → overheating
   - Solution: Resolder all connections

### Diagnosis

**Step 1: Check Operating Temperature**
- Measure hot-side temperature before shutdown
- If > 75°C: thermal protection tripped
- Solution: Improve heat dissipation (see Problem 3)

**Step 2: Monitor Current Draw**
- Measure current while system is on
- Should be steady 6-8A
- If spiking or climbing: short circuit risk
- Solution: Check for loose/corroded connections

**Step 3: Listen for Arcing**
- During operation, listen carefully
- Any buzzing/crackling = arcing sound
- Indicates electrical problem
- Solution: Find and resolder loose joint

### Solutions

**If Thermal Overload:**
1. See Problem 3 solutions
2. Improve hot-side cooling
3. Clean heatsink
4. Replace with better fan
5. Add extra cooling capacity

**If Over-Current:**
1. Power OFF immediately
2. Inspect for shorts (exposed wires touching)
3. Check soldered connections for bridges
4. Verify no accidental connections
5. Resolder if needed
6. Test with multimeter before powering on

---

## Advanced Troubleshooting

### Thermal Imaging (if IR camera available)

```
Useful for identifying:
- Localized hot spots (poor thermal contact)
- Uneven heatsink temperatures (airflow issue)
- Cold spots in chamber (insulation failure)
- Case temperatures (safety check)
```

### Current Signature Analysis

```
Normal:
  - Steady 6-8A (TEC operating normally)
  - Minor ripple < 0.5A

Abnormal Signatures:
  - Climbing current: Indicates increasing resistance (connection degrading)
  - Oscillating current: Possible thermal oscillation or arcing
  - Dropping current: Possible overheating, TEC resistance increasing
```

---

## Testing Checklist

- [ ] Verified AC power at outlet
- [ ] Measured PSU output (12V ± 0.5V)
- [ ] Checked fuse integrity
- [ ] Verified switch operation
- [ ] Measured current draw (6-8A)
- [ ] Confirmed TEC polarity
- [ ] Inspected thermal paste coverage
- [ ] Cleaned heatsink fins
- [ ] Verified fan operation
- [ ] Measured hot-side temperature
- [ ] Measured cold-side temperature
- [ ] Checked insulation integrity
- [ ] Tested chamber temperature
- [ ] Verified steady-state behavior

---

**Troubleshooting Guide Version**: 1.0  
**Last Updated**: May 2026
