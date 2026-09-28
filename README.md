# Automatic-phase-selector
# Automatic Phase Selector

MIN_VOLTAGE = 200
MAX_VOLTAGE = 250

print("==============================")
print("    AUTOMATIC PHASE SELECTOR")
print("==============================")

r = float(input("Enter R phase voltage (V): "))
y = float(input("Enter Y phase voltage (V): "))
b = float(input("Enter B phase voltage (V): "))

phases = {
    "R": r,
    "Y": y,
    "B": b
}

# Find healthy phases
healthy_phases = {
    phase: voltage
    for phase, voltage in phases.items()
    if MIN_VOLTAGE <= voltage <= MAX_VOLTAGE
}

if healthy_phases:
    # Select the phase with voltage closest to 230 V
    selected_phase = min(
        healthy_phases,
        key=lambda phase: abs(healthy_phases[phase] - 230)
    )

    print("\n🟢 Healthy phases:", list(healthy_phases.keys()))
    print("⚡ Selected Phase:", selected_phase)
    print("Voltage:", healthy_phases[selected_phase], "V")
    print("✅ Load connected to selected phase")

else:
    print("\n🔴 No healthy phase available")
    print("⚠️ Load disconnected for protection")
