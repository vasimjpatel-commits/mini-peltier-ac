# Mini Peltier Air Conditioner - Design Blueprint

A complete DIY guide to building a mini air conditioner using Peltier thermoelectric cooling modules (TEC).

## 📋 Project Overview

This project provides detailed design specifications, circuit diagrams, thermal calculations, and assembly instructions for constructing a compact cooling system using Peltier modules. Perfect for cooling small spaces, computer cases, or personal cooling applications.

## 🎯 Features

- ✅ Complete circuit design with safety components
- ✅ Detailed BOM (Bill of Materials)
- ✅ Thermal calculations and efficiency analysis
- ✅ Assembly instructions with step-by-step guides
- ✅ Optional temperature control using microcontrollers
- ✅ Troubleshooting and optimization tips
- ✅ Multiple design variants (basic to advanced)

## 📁 Repository Structure

```
mini-peltier-ac/
├── README.md                           # Project overview
├── DESIGN_BLUEPRINT.md                 # Detailed design specifications
├── CIRCUIT_DIAGRAMS.md                 # Circuit schematics and wiring
├── BOM.csv                             # Bill of Materials
├── ASSEMBLY_INSTRUCTIONS.md            # Step-by-step assembly guide
├── THERMAL_CALCULATIONS.md             # Thermal analysis and performance
├── TROUBLESHOOTING.md                  # Common issues and solutions
├── schematics/                         # Circuit diagram files
│   ├── basic-circuit.txt
│   ├── control-circuit.txt
│   └── fritzing-layout.txt
├── cad-models/                         # 3D design files (future)
├── firmware/                           # Microcontroller code (Arduino, etc.)
│   └── peltier-thermostat.ino
└── resources/                          # Additional references and datasheets
    └── TEC1-12706-datasheet.txt
```

## 🔧 Quick Start

### Basic System Components

| Component | Model | Qty |
|-----------|-------|-----|
| Peltier Module | TEC1-12706 | 1-2 |
| Power Supply | 12V/15A PSU | 1 |
| Heatsink + Fan (Hot) | CPU Cooler | 1 |
| Heatsink (Cold) | 60x60mm | 1 |
| Thermal Paste | Arctic Silver | 1 |
| Insulating Foam | Polystyrene | As needed |
| Temperature Controller | W1209 (optional) | 1 |

### Basic Assembly

1. **Prepare Chamber**: Insulate with foam, seal gaps
2. **Attach Heatsinks**: Apply thermal paste to all TEC contact surfaces
3. **Mount Fans**: Position hot-side fan for maximum airflow
4. **Wire Circuit**: Connect power → fuse → switch → TEC → ground
5. **Test System**: Verify cooling performance

## 📊 Design Specifications

- **Input Voltage**: 12V DC
- **Power Consumption**: 60-100W (depending on configuration)
- **Cooling Capacity**: 10-50W (depending on ambient temperature)
- **Target Temperature Drop**: 10-25°C below ambient
- **Operating Efficiency**: 30-50% (Peltier technology)

## 🔌 Circuit Design

### Basic Circuit
```
12V DC Power Supply → Fuse (10A) → Switch → TEC Module → Ground
                                         ↓
                                    Fans (parallel)
```

### Advanced Circuit (with Temperature Control)
```
Temperature Sensor → Microcontroller → MOSFET/Relay → TEC Power Control
```

## 📚 Documentation Files

- **DESIGN_BLUEPRINT.md**: Complete technical specifications
- **CIRCUIT_DIAGRAMS.md**: Detailed electrical schematics
- **BOM.csv**: Component list with sourcing information
- **ASSEMBLY_INSTRUCTIONS.md**: Step-by-step assembly guide
- **THERMAL_CALCULATIONS.md**: Performance analysis and calculations
- **TROUBLESHOOTING.md**: Problem-solving guide

## ⚠️ Safety Considerations

- Use proper fuses and circuit protection
- Ensure adequate ventilation for hot-side heatsink
- Monitor for condensation and moisture management
- Verify power supply capacity before operation
- Always use thermal paste between components
- Allow for proper heat dissipation

## 🎓 Technical Concepts

### How Peltier Cooling Works

The Peltier effect (Seebeck effect in reverse) uses the movement of electrons to transfer heat from one side of a semiconductor junction to the other when DC current is applied.

**Key Points:**
- One side becomes cold (endothermic)
- One side becomes hot (exothermic)
- Efficiency depends on heat dissipation
- Power consumption is relatively high

### Optimal Operating Conditions

- **Hot side temperature**: 45-60°C (active cooling required)
- **Cold side temperature**: 5-25°C (below ambient)
- **Thermal paste quality**: Critical for performance
- **Airflow**: Minimum 50 CFM on hot side

## 🚀 Advanced Features (Optional)

1. **Temperature Control**: Automatic on/off based on setpoint
2. **PWM Control**: Variable cooling power
3. **Display**: Real-time temperature monitoring
4. **Humidity Sensor**: Condensation management
5. **Multiple Modules**: Increased cooling capacity

## 📖 How to Use This Repository

1. **Read** DESIGN_BLUEPRINT.md for complete specifications
2. **Review** CIRCUIT_DIAGRAMS.md for electrical design
3. **Gather** components using BOM.csv
4. **Follow** ASSEMBLY_INSTRUCTIONS.md for building
5. **Reference** THERMAL_CALCULATIONS.md for performance expectations
6. **Consult** TROUBLESHOOTING.md if issues arise

## 🔗 External Resources

- [TEC Thermoelectric Cooler Basics](https://en.wikipedia.org/wiki/Thermoelectric_cooling)
- [Peltier Module Datasheets](./resources/)
- [DIY Electronics Community](https://electronics.stackexchange.com/)
- [Arduino Microcontroller Projects](https://www.arduino.cc/)

## 💡 Design Variants

This repository includes designs for:

- **Basic Setup**: Simple on/off cooling (minimal components)
- **Controlled Setup**: Automatic temperature regulation
- **Multi-Module Setup**: Increased cooling capacity
- **Water-Cooled Setup**: Advanced heat dissipation (experimental)

## 🤝 Contributing

Contributions welcome! Areas for improvement:

- CAD 3D models
- PCB design files
- Firmware improvements
- Performance optimizations
- Additional design variants

## 📝 License

This project is provided as educational and personal use documentation.

## 👤 Author

**vasimjpatel-commits** - Mini Peltier AC Design Project

## 📞 Support

For questions or issues:
- Check TROUBLESHOOTING.md first
- Review related documentation files
- Consult external datasheets and resources

---

**Last Updated**: May 2026  
**Status**: Design Blueprint Complete ✅

---

### Quick Links

- [Design Blueprint](./DESIGN_BLUEPRINT.md)
- [Circuit Diagrams](./CIRCUIT_DIAGRAMS.md)
- [Bill of Materials](./BOM.csv)
- [Assembly Guide](./ASSEMBLY_INSTRUCTIONS.md)
- [Thermal Analysis](./THERMAL_CALCULATIONS.md)
- [Troubleshooting](./TROUBLESHOOTING.md)
