# VW Camping Mode Blueprint for Home Assistant
[![en](https://img.shields.io/badge/lang-en-green.svg)](https://github.com/petr-bartusek/habptest1/blob/master/README.md)
[![cz](https://img.shields.io/badge/lang-cs-green.svg)](https://github.com/petr-bartusek/habptest1/blob/master/README.cs.md)

_Read this in other languages:_ [Czech](https://github.com/petr-bartusek/habptest1/blob/master/README.cs.md)
Home Assistant (HA) blueprint for automatic climate control in Volkswagen vehicles during camping.

## 🚀 Features

- ✅ **Car Climate Control**: 
- ✅ **Smart Battery Management**: Automatic climate control based on battery level
- ✅ **Automatic Restart**: Automatic restart after climate shutoff with configurable delay

## Requirements 

- Supported VW Car (ID.Buzz, ID.3, ID.4, ID.5, ID.7 with ID Software 3.X or newer are supported, but for other models as Passat, Golf, e-Golf, Tiguan, etc. it could be work as well).
- Created [MyVolkswagen/Wolkswagen ID account](https://www.myvolkswagen.net/cz/cs/myvolkswagen.html) and activated [VW Connect service](https://www.volkswagen.cz/technologie/konektivita/vw-connect) in your car.
- Created [GitHub Account](https://github.com/) (required by HACS).
- Home Assistant instalation supporting Add-ons innstalation [HA Documentation](https://www.home-assistant.io/installation/).
- Home Assistant 2024.6.0 or newer.

## Instalation Overview

1. Install and configure HACS to your Home Assistant [GUIDE](https://hacs.xyz/docs/use/).
1. Install [Volkswagen Connect](https://github.com/robinostlund/homeassistant-volkswagencarnet?tab=readme-ov-file#install-with-hacs-recommended) component from HACS dashboard.
1. Configure Volkswagen Connect component and sign by your MyVolkswagen/Wolkswagen ID account.
1. Manually create required HA helper entities (TODO: Link lower to chapter).
1. Import of HA Blueprint for Camping mode UI (TODO: Link lower to chapter).
1. Create Automation
2. (Optional) Install Lovelace card from HACS
3. (Optional) Import Dashboard

## 🔧 Creation of Helper Entities

### Step 1: Navigate to HA helpers entities page 
Pres button below to be redirected to your HA instance
[![Open your Home Assistant instance and show your helper entities.](https://my.home-assistant.io/badges/helpers.svg)](https://my.home-assistant.io/redirect/helpers/)
or go to **Settings** → **Devices & Services** → **Helpers**.

### Step 2 - Option 1: Create helpers from manually

**Add these eight helpers:**
1. Camping Start Time
   - Type: Datum a/nebo čas (Need EN name)
   - Name: Camping Start Time
   - Co chcete zadat: Čas (Need EN name)
2. Camping End Time
   - Type: Datum a/nebo čas (Need EN name)
   - Name: Camping End Time
   - Co chcete zadat: Čas (Need EN name)
3. Auto Camping Mode
   - Type: Přepínač
   - Name: Auto Camping Mode
   - Icon: mdi:air-conditioner
4. Auto Start Mode
   - Type: Přepínač
   - Name: Auto Camping Mode
   - Icon: mdi:clock-start
5. Auto End Mode
   - Type: Přepínač
   - Name: Auto End Mode
   - Icon: mdi:clock-end
6. Battery Limit
   - Type: Číslo
   - Name: Battery Limit
   - Icon: mdi:battery-50
   - Minimální hodnota: 20
   - Maximální hodnota: 80
   - Velikost kroku: 5
   - Měrná jednotka: %
7. xxx
   - Type: Číslo
   - Name: xxx
   - Icon: mdi:timer
   - Minimální hodnota: 15
   - Maximální hodnota: 120
   - Velikost kroku: 15
   - Měrná jednotka: min
8. Camping Delay Timer
   - Type: Časovač
   - Name: Camping Delay Timer
   - Icon: mdi:timer
   - Co chcete zadat: 0:00:00

### Option 2: Create helpers from YAML Configurations 
Add to your `configuration.yaml`:

### Input DateTime Helpers
```yaml
input_datetime:
  camping_start_time:
    name: "Camping Start Time"
    has_date: false
    has_time: true
    
  camping_end_time:
    name: "Camping End Time"
    has_date: false
    has_time: true
```

### Input Boolean Helpers
```yaml
input_boolean:
  auto_camping_mode:
    name: "Auto Camping Mode"
    icon: mdi:air-conditioner
    
  auto_start_mode:
    name: "Auto Start Mode"  
    icon: mdi:clock-start
    
  auto_end_mode:
    name: "Auto End Mode"
    icon: mdi:clock-end
```

### Input Number Helpers
```yaml
input_number:
  battery_limit:
    name: "Battery Limit"
    min: 20
    max: 80
    step: 5
    unit_of_measurement: "%"
    icon: mdi:battery-50
    
  restart_delay:
    name: "Restart Delay"
    min: 15
    max: 120
    step: 15
    unit_of_measurement: "min"
    icon: mdi:timer
```

### Timer Helper
```yaml
timer:
  camping_delay_timer:
    name: "Camping Delay Timer"
    duration: "00:00:00"
    icon: mdi:timer-sand
```

## 📥 Blueprint Installation

### Step 6: Import Blueprint

**⚠️ ONLY import Blueprint AFTER Volkswagen Connect integration from HACS is working! and all helper entities are created!**
[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/petr-bartusek/habptest1/blob/documentation-update/blueprint.yaml)

**⚠️ Complete Steps 1-4 from instalation first! Volkswagen Connect MUST be working!**

1. Go to **Settings** → **Automations & Scenes** → **Blueprints**
2. Click **Import Blueprint**  
3. Enter the blueprint URL: `https://github.com/jhron/habptest1`
4. Or copy the content from `blueprint.yaml`

### Step 7: Create Automation
1. Click **Create Automation** from the imported blueprint
2. **Configure vehicle entities** (selectors will show only VW Car-Net entities):
   - **Battery sensor**: Blueprint will show only VW battery sensors
   - **Climate device**: Select your VW ID.Buzz device from VW integration
   - **Climate entity**: Blueprint will show only VW climate controls
3. **Configure helper entities** (created in Step 5)
4. Set your preferred times and battery limits
5. Save and test!

## 🔍 Troubleshooting

### VW Car-Net Integration Issues:
- **No entities**: Check VW account credentials
- **Authentication failed**: Try re-entering password
- **Entities unavailable**: Vehicle might be sleeping, try remote unlock
- **Climate not working**: Check if climatisation is available in VW app

### Blueprint Issues:
- **Import fails**: Verify all helper entities exist
- **Automation not triggering**: Check entity states in Developer Tools
- **Climate not starting**: Verify VW integration entities are working

## 🔄 How It Works

1. **Start Time**: Climate automatically starts at configured time if battery is sufficient and auto start mode is enabled
2. **End Time**: Climate stops at configured end time if auto end mode is enabled  
3. **Battery Protection**: Climate stops immediately if battery drops to the battery limit
4. **Manual Override**: If climate is turned off manually, it restarts after delay if auto start mode is still active
5. **Smart Recovery**: After delay, climate restarts if conditions are still met and auto start mode is active

## 📝 License

MIT License - Feel free to modify and share!

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Test with Home Assistant 2025.1+
4. Submit a pull request

## 📞 Support

For issues or questions:
1. Check the logbook for detailed error messages
2. Verify all helper entities are created correctly
3. Ensure your VW integration is working properly
4. Open an issue
