# VW ID.Buzz Camping Mode Blueprint

Home Assistant blueprint for automatic climate control in VW ID.Buzz vehicles during camping.

## 🚀 Features

- ✅ **Smart Battery Management**: Automatic climate control based on battery level
- ✅ **Automatic Restart**: Automatic restart after climate shutoff with configurable delay

## 🔧 Required Entities

**⚠️ ONLY import Blueprint AFTER VW Car-Net integration is working! and all helper entities are created!**
**🔗 VW Integration required:** https://github.com/robinostlund/homeassistant-volkswagencarnet

### Method 1: UI Creation (Recommended)
Go to **Settings** → **Devices & Services** → **Helpers** and create:

### Method 2: YAML Configuration  
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
    
  delay_minutes:
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
  camping_delay:
    name: "Camping Delay Timer"
    duration: "00:00:00"
    icon: mdi:timer-sand
```

## 📥 Blueprint Installation

### Step 6: Import Blueprint
**⚠️ Complete Steps 1-5 first! VW Car-Net MUST be working!**

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
