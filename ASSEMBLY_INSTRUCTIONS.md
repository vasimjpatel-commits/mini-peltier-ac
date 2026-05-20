# Mini Peltier AC - Step-by-Step Assembly Guide

## Phase 1: Preparation & Planning

### 1.1 Tools & Equipment Required

**Electrical Tools:**
- Soldering iron (30-40W)
- Solder (rosin-core 60/40)
- Wire strippers (16-24 AWG)
- Crimpers for terminals
- Multimeter (for testing)
- Heat shrink tubing (various sizes)

**Mechanical Tools:**
- Phillips screwdriver
- Flathead screwdriver
- Wrench/socket set (for heatsink mounting)
- Thermal paste application tool or plastic spreader
- Drill (if custom mounting needed)

**Safety Equipment:**
- Safety glasses
- Work gloves
- Soldering fume extractor
- Fire extinguisher (nearby)

### 1.2 Workspace Setup

- Clean, well-lit work area
- Anti-static mat (optional but recommended)
- Component organization (resistors, diodes, wires)
- Good ventilation for soldering fumes
- Temperature-controlled room (~20-25°C)

### 1.3 Component Verification

Before starting, verify all components:
- [ ] Peltier module (TEC1-12706) - 1-2 units
- [ ] 12V power supply (verified 12V output)
- [ ] CPU cooler with fan (hot side)
- [ ] Aluminum heatsink (cold side)
- [ ] Thermal paste (Arctic Silver or equivalent)
- [ ] Fuse (10A) and fuse holder
- [ ] Toggle switch (20A rated)
- [ ] Electrical wire (14 AWG main, 18 AWG signal)
- [ ] Crimp terminals and connectors
- [ ] Foam insulation (5cm thick minimum)

---

## Phase 2: Thermal Interface Preparation

### 2.1 Heatsink Cleaning

**Hot Side Heatsink:**
1. Inspect for factory protective coating
2. Wipe base with clean cloth (remove dust)
3. Clean with isopropyl alcohol (IPA) on lint-free cloth
4. Allow to air dry completely (5 minutes)
5. Do NOT touch base with bare hands after cleaning

**Cold Side Heatsink/Block:**
1. Repeat cleaning procedure as above
2. Ensure all fins are clean
3. Check for bent fins (straighten if needed)

### 2.2 Peltier Module Inspection

1. Visual inspection:
   - Check for cracks or damage
   - Verify no solder on pins
   - Confirm dimensions (40×40×3.8mm)

2. Pin verification:
   - Red wire: Positive (+12V)
   - Black wire: Negative (GND)
   - Wires should be intact and insulated

3. Do NOT touch the module surfaces (oils cause poor contact)

### 2.3 Thermal Paste Application Technique

**Correct Method:**
```
1. Take pea-sized amount of thermal paste
2. Place on TEC hot side surface
3. Gently spread using plastic spreader or cardboard
4. Thin, even layer (~0.5mm) across entire surface
5. Do NOT over-apply (excess reduces performance)

Paste Coverage:
┌──────────────────┐
│  Pea-sized dots  │  → Spread evenly
│   (3-5 dots)     │
└──────────────────┘
     ↓
┌──────────────────┐
│  Thin layer      │  Perfect
│  (~0.5mm)        │
└──────────────────┘
```

**Application Tips:**
- Too much paste: Reduces heat transfer, wastes paste
- Too little paste: Creates air gaps, causes hot spots
- Uneven coverage: Creates thermal resistance variations

---

## Phase 3: Heatsink Assembly

### 3.1 Hot Side Heatsink Assembly

**Step 1: Apply Thermal Paste to TEC Hot Side**
- Apply thin, even layer as described above
- Cover entire surface
- DO NOT apply paste to TEC cold side yet

**Step 2: Mount Heatsink to Peltier**
- Place heatsink base on TEC hot side
- Press down with firm, even pressure
- Use mounting brackets/clamps if available
- Verify heatsink is level and flat contact
- Tighten any mounting screws gradually (avoid over-tightening)

**Step 3: Install CPU Cooler Fan**
- Mount fan to heatsink (typically with push-pins or screws)
- Verify fan orientation: airflow should point AWAY from TEC
- Check for proper clearance (no wire interference)
- Secure all fasteners

### 3.2 Cold Side Block Installation

**Step 1: Apply Thermal Paste to TEC Cold Side**
- Apply pea-sized amount to TEC cold side surface
- Spread evenly across surface
- This will contact the cold block

**Step 2: Mount Cold Block**
- Place cold block on TEC cold side
- Press down gently but firmly
- Use thermal clamp or C-clamp for secure contact
- Ensure flush, level contact
- Tighten clamp gradually (avoid over-tightening)

**Step 3: Verify Thermal Contact**
- Check for gaps between surfaces
- Confirm no rocking or movement
- Thermal paste should squeeze out slightly at edges

---

## Phase 4: Electrical Wiring

### 4.1 Power Supply Connections

**Step 1: Prepare Wire Ends**
- Strip 6mm insulation from wire ends
- Tin wire ends with solder (dip in solder)  
- Inspect for clean connection

**Step 2: Connect 12V Main Rail**
- Route red wire from PSU 12V output
- Connect to fuse positive terminal (solder or crimp)
- Use 14 AWG wire for this connection
- Verify secure connection (gentle tug test)

**Step 3: Connect Ground Rail**
- Route black wire from PSU ground
- Solder to central ground bus or directly to components
- Use 14 AWG wire
- This is the return path for ALL circuits

### 4.2 Fuse Installation

**Step 1: Mount Fuse Holder**
- Secure fuse holder to panel or enclosure
- Use plastic clamps or small bracket

**Step 2: Install Fuse**
- Insert 10A fast-blow fuse into holder
- Ensure proper orientation (fuse sits flush)
- Test that fuse is removable (in case of replacement)

**Step 3: Test Fuse Protection**
- Verify fuse holder makes good contact
- No loose connections that could cause resistance

### 4.3 Switch Installation

**Step 1: Mount Switch**
- Secure toggle switch to enclosure or panel
- Use M12 connector or screw mounting
- Ensure switch is accessible

**Step 2: Wire Switch**
- Connect fuse positive output to switch input (one contact)
- Connect switch output to TEC positive terminal
- Use 14 AWG wire
- Secure with solder or crimped terminals

**Step 3: Test Switch Operation**
- Toggle switch smoothly on/off
- No grinding or rough feel
- Contacts make positive engagement

### 4.4 TEC Module Connections

**Step 1: Connect TEC Positive**
- Route red wire from TEC to switch output
- Solder connection securely
- Use heat shrink tubing to insulate
- Verify polarity before powering on

**Step 2: Connect TEC Negative**
- Route black wire from TEC to ground rail
- Solder to ground bus
- Use heat shrink tubing
- Confirm secure connection

**Step 3: Dress Wires**
- Route wires neatly to avoid tangles
- Use cable ties or spiral wrap
- Keep signal wires away from power wires (if applicable)
- Avoid sharp bends that could break wires

### 4.5 Fan Connections

**Step 1: Connect Hot-Side Fan**
- Connect red wire to 12V main rail
- Connect black wire to ground rail
- Use 16 AWG wire (sufficient for fan current)
- Secure with solder or crimp terminals

**Step 2: Connect Optional Cold-Side Fan**
- Same as above (parallel to main power)
- Both fans draw from same 12V rail
- No additional control needed (always on when powered)

---

## Phase 5: Insulation & Chamber Assembly

### 5.1 Foam Cutting & Preparation

**Step 1: Measure Chamber Dimensions**
- Determine desired cooling volume (20-50L recommended)
- Measure width, length, height
- Account for heatsink placement

**Step 2: Cut Foam Pieces**
- Use hot-wire foam cutter or serrated knife
- Cut 5cm (2 inch) thick foam slabs
- Aim for snug fit (slightly compressed is OK)
- Protect work surface (foam bits scatter)

**Step 3: Assembly**
- Glue foam sheets together using spray foam adhesive or hot glue
- Build box shape around cooling volume
- Leave access openings for:
  - Air intake (cold side air distribution)
  - Air return vents
  - Drain holes (for condensation)

### 5.2 Sealing & Insulation

**Step 1: Seal Gaps**
- Use expanding foam or duct tape to seal any gaps
- Ensure no air leaks around chamber
- Compress foam slightly as it expands

**Step 2: Thermal Testing**
- Check for cold spots (indicates air leakage)
- Feel for temperature variations around chamber
- Reseal any problem areas

**Step 3: Condensation Management**
- Drill small drainage holes in bottom of chamber
- Use small tube to direct condensation to collection point
- Optional: Install small dehumidifier cartridge

---

## Phase 6: Testing & Validation

### 6.1 Pre-Power Checks

**Step 1: Visual Inspection**
- [ ] All connections are soldered/crimped securely
- [ ] No bare wires exposed
- [ ] Fuse installed and accessible
- [ ] Switch in OFF position
- [ ] Heatsinks mounted firmly
- [ ] Thermal paste visible but not excessive
- [ ] Fans spin freely by hand
- [ ] All insulation in place

**Step 2: Continuity Testing (Multimeter)**
- Set multimeter to continuity mode (Ω)
- Test 12V rail: Should read ~0Ω end-to-end
- Test GND rail: Should read ~0Ω end-to-end
- Test TEC connections: Red to 12V = ~0Ω, Black to GND = ~0Ω
- Test switch: OFF = ∞, ON = ~0Ω

**Step 3: Voltage Verification**
- Set multimeter to DC voltage (20V range)
- Measure 12V rail: Should read 12.0 ± 0.5V
- Measure GND rail: Should read 0V (reference)
- Test switch: OFF = 0V at output, ON = 12V at output

### 6.2 First Power-On (No-Load Test)

**Step 1: Initial Connection**
- Connect PSU to AC mains (110-240V)
- PSU LED should light (if equipped)
- NO components powered yet

**Step 2: Monitor PSU Output**
- Measure output voltage: Should be 12.0V
- Measure output current: Should be < 0.1A (no load)
- Listen for any unusual sounds

**Step 3: Switch ON (Fans Only)**
- Turn toggle switch to ON position
- Observe fans spinning
- Fans should run smoothly at constant speed
- Current draw should be ~0.5-1.0A
- No unusual vibration or noise

**Step 4: Hold Test (5 minutes)**
- Keep system running for 5 minutes
- Monitor current (should remain stable)
- Check for any overheating smells
- Verify no warning signs

### 6.3 Full Load Test

**Step 1: System Ready**
- TEC module connected and thermal interfaces applied
- Both heatsinks mounted securely
- All wiring complete
- Insulation in place

**Step 2: First Power-On with TEC**
- Turn switch ON
- Monitor current draw: Should be 6-8A
- Current should stabilize within 10 seconds

**Step 3: Thermal Monitoring**
- Measure hot-side heatsink temperature with IR thermometer
- Target: 45-60°C within 5 minutes
- If exceeding 70°C: STOP and investigate fan operation

**Step 4: Cold Side Verification**
- Measure cold block temperature with IR thermometer
- Target: 15-25°C within 10 minutes
- If not cooling: Check thermal paste application and TEC polarity

**Step 5: Interior Chamber Temperature**
- Use thermometer inside chamber
- Should cool to 10-15°C within 20 minutes
- Rate of cooling indicates system efficiency

### 6.4 Extended Runtime Test

**Step 1: 30-Minute Stability Test**
- Run system for 30 minutes continuously
- Record temperature every 5 minutes:
  - Hot side heatsink
  - Cold side block
  - Interior chamber
  - Ambient room temperature

**Step 2: Steady-State Analysis**
- Temperatures should stabilize after 15-20 minutes
- Plot temperature graph (optional)
- Calculate ΔT (interior - ambient)
- Compare against design target

**Step 3: Safety Shutdown**
- Turn switch OFF
- Allow system to cool for 5 minutes
- Measure cool-down rate
- Inspect for any damage or concerns

---

## Phase 7: Optimization & Fine-Tuning

### 7.1 Performance Optimization

If cooling is weak:
1. Increase insulation (add extra foam)
2. Improve hot-side airflow (increase fan speed if possible)
3. Check thermal paste coverage (may need reapplication)
4. Ensure cold block contact is firm

If power consumption is high:
1. Reduce insulation thickness slightly (trade-off)
2. Check for air leaks (reseal if found)
3. Operate at lower duty cycle (if using PWM)

If excessive noise:
1. Add vibration dampeners under heatsink
2. Reduce fan speed (if adjustable)
3. Check for loose components

### 7.2 Optional: Temperature Controller Installation

If adding automatic control:
1. Install DS18B20 sensor on cold block (solder terminals)
2. Program Arduino with control logic (see firmware section)
3. Mount MOSFET on heatsink
4. Connect PWM signal to MOSFET gate
5. Test temperature setpoint control

---

## Phase 8: Final Assembly & Documentation

### 8.1 Enclosure (Optional)

1. Mount all components in plastic/aluminum enclosure
2. Drill holes for:
   - Power connector
   - Switch
   - Sensor display (if applicable)
   - Ventilation (hot side exhaust)

3. Route wires internally
4. Label all connections

### 8.2 Labeling & Documentation

1. Label power switch: ON/OFF
2. Label power connector: +12V, GND
3. Mark hot/cold sides clearly
4. Include warning labels (HOT SURFACE)
5. Create system diagram reference inside enclosure

### 8.3 Operational Manual

Create user guide including:
- Power requirements
- Operating temperature range
- Maintenance schedule
- Troubleshooting quick reference
- Safety warnings

---

## Assembly Checklist

- [ ] All components verified and present
- [ ] Thermal paste applied correctly
- [ ] Heatsinks mounted securely
- [ ] All electrical connections soldered/crimped
- [ ] Fuse installed (10A)
- [ ] Switch mounted and operational
- [ ] Wiring insulated and organized
- [ ] Foam insulation installed
- [ ] Pre-power tests completed
- [ ] Initial power-on successful
- [ ] Thermal performance validated
- [ ] 30-minute stability test passed
- [ ] System labeled and documented
- [ ] User manual created

---

**Assembly Guide Version**: 1.0  
**Last Updated**: May 2026
