# pin-base
MPF Base Pinball: a Mission Pinball Framework (0.81) starter game for a CobraPin controller.

## Requirements
- **Python 3.10 – 3.14** (this project uses 3.13). Python 3.15 is *not* supported: Pillow has
  no prebuilt wheel for it, so `pip install mpf` fails trying to build Pillow from source.
- CobraPin board (OPP gen2 firmware), connected over USB.
- Media (display/sound): Godot + the MPF-GMC plugin. Not set up yet.

## Setup (Windows / PowerShell)
```powershell
py -3.13 -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\Activate.ps1      # then `mpf` is on PATH
mpf --version
```

## Running
```powershell
mpf game -x -b      # virtual hardware, no media controller (config check / logic testing)
mpf game -b         # real CobraPin hardware, no media controller
mpf monitor         # switch/coil/light monitor GUI (run in a second terminal)
```

## Layout
- `config/config.yaml`: OPP platform + COM ports, switches, coils, flippers, playfield
- `modes/attract`, `modes/base`: starter modes from `mpf init`

## Bringing up the CobraPin
1. Plug in and power the board, then find its two COM ports in Device Manager > Ports
   (or run `[System.IO.Ports.SerialPort]::GetPortNames()`).
2. Put them in `config/config.yaml` under `opp: ports:`.
3. Flippers (dual-wound, J6 Bank A), slings (coils only) and flipper buttons (J1) are mapped
   to the real wiring. The plunger lane switch (`0-0-3`) is still a placeholder.
4. Run `mpf game -b` and use `mpf monitor` to check each switch.

Docs: https://missionpinball.org/latest/hardware/opp/cobrapin/
