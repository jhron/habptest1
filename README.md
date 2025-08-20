# VW ID.Buzz Camping Mode Blueprint

Home Assistant blueprint for automatic climate control in VW ID.Buzz vehicles during camping.

## 🚀 Features

- ✅ **Smart Battery Management**: Automatic climate control based on battery level
- ✅ **Automatic Restart**: Automatic restart after climate shutoff with configurable delay

## 🔧 Required Entities

Before importing this blueprint, create these helper entities in Home Assistant:

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
    
  camping_mode_active:
    name: "Camping Mode Active"
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

## 📥 Installation

1. Copy the required helper entities to your `configuration.yaml` or create them manually over the UI.
2. Restart Home Assistant to load the helpers
3. Import the blueprint:
   - Go to **Settings** → **Automations & Scenes** → **Blueprints**
   - Click **Import Blueprint**
   - Enter the blueprint URL or copy the content from `blueprint.yaml`

## 🔄 How It Works

1. **Start Time**: Climate automatically starts at configured time if battery is sufficient and mode is active
2. **End Time**: Climate stops at configured end time if automatic off switch is enabled
3. **Battery Protection**: Climate stops immediately if battery drops to the battery limit
4. **Manual Override**: If climate is turned off manually or automatically after 30 min, it restarts after delay
5. **Smart Recovery**: After delay, climate restarts if conditions are still met

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
