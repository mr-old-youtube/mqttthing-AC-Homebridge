# mqttthing-AC-Homebridge
Code dieu khien ac qua homebridge

{
            "type": "heaterCooler",
            "name": "Kitchen AC",
            "url": "192.168.68.120:1883",
            "topics": {
                "setActive": {
                    "topic": "cmnd/tasmota_F7DA8B/IRhvac",
                    "apply": "state.global.HVAC = state.global.HVAC || {}; state.global.HVAC.Power = message; state.global.HVAC.Protocol = 'MITSUBISHI_HEAVY_152'; return (JSON.stringify(state.global.HVAC));"
                },
                "getActive": {
                    "topic": "tele/tasmota_F7DA8B/RESULT",
                    "apply": "return JSON.parse(message).IrReceived.IRHVAC.Power === 'On' ? true : false;"
                },
                "getCurrentHeaterCoolerState": {
                    "topic": "stat/tasmota_F7DA8B/RESULT",
                    "apply": "var mode = JSON.parse(message).IRHVAC.Mode.toLowerCase();               if (mode === 'cool') {                   return 'COOLING';               } else if (mode === 'heat') {                   return 'HEATING';               } else {                   return 'INACTIVE';               }"
                },
                "setTargetHeaterCoolerState": {
                    "topic": "cmnd/tasmota_F7DA8B/IRhvac",
                    "apply": "state.global.HVAC = state.global.HVAC || {}; state.global.HVAC.Mode = message; return (JSON.stringify(state.global.HVAC));"
                },
                "getTargetHeaterCoolerState": {
                    "topic": "stat/tasmota_F7DA8B/RESULT",
                    "apply": "return JSON.parse(message).IRHVAC.Mode;"
                },
                "getCurrentTemperature": {
                    "topic": "tele/tasmota_ble/ATCf2d27d",
                    "apply": "return JSON.parse(message).Temperature;"
                },
                "setCoolingThresholdTemperature": {
                    "topic": "cmnd/tasmota_F7DA8B/IRhvac",
                    "apply": "state.global.HVAC = state.global.HVAC || {}; state.global.HVAC.Temp = message; return (JSON.stringify(state.global.HVAC));"
                },
                "getCoolingThresholdTemperature": {
                    "topic": "tele/tasmota_F7DA8B/RESULT",
                    "apply": "return JSON.parse(message).IrReceived.IRHVAC.Temp;"
                },
                "setHeatingThresholdTemperature": {
                    "topic": "cmnd/tasmota_F7DA8B/IRhvac",
                    "apply": "state.global.HVAC = state.global.HVAC || {}; state.global.HVAC.Temp = message; return (JSON.stringify(state.global.HVAC));"
                },
                "getHeatingThresholdTemperature": {
                    "topic": "tele/tasmota_F7DA8B/RESULT",
                    "apply": "return JSON.parse(message).IrReceived.IRHVAC.Temp;"
                },
                "setTemperatureDisplayUnits": {
                    "topic": "cmnd/tasmota_F7DA8B/IRhvac",
                    "apply": "state.global.HVAC = state.global.HVAC || {}; state.global.HVAC.Econo = message; return (JSON.stringify(state.global.HVAC));"
                },
                "getTemperatureDisplayUnits": "<topic used to report 'temperature display units'>",
                "setRotationMode": {
                    "topic": "cmnd/tasmota_F7DA8B/IRhvac",
                    "apply": "state.global.HVAC = state.global.HVAC || {}; state.global.HVAC.Temp = message; return (JSON.stringify(state.global.HVAC));"
                },
                "getRotationMode": "<topic used to report 'rotation mode' (optional)>",
                "setSwingMode": {
                    "topic": "cmnd/tasmota_F7DA8B/IRhvac",
                    "apply": "state.global.HVAC = state.global.HVAC || {}; state.global.HVAC.SwingV = message; return (JSON.stringify(state.global.HVAC));"
                },
                "getSwingMode": "<topic used to report 'swing mode' (optional)>",
                "setRotationSpeed": {
                    "topic": "cmnd/tasmota_F7DA8B/IRhvac",
                    "apply": "state.global.HVAC = state.global.HVAC || {};              var speed = isNaN(parseInt(message)) ? state.rotationSpeed : Math.round(parseInt(message) / 20);              state.global.HVAC.FanSpeed = speed.toString();              return JSON.stringify(state.global.HVAC);"
                },
                "getRotationSpeed": {
                    "topic": "tele/tasmota_F7DA8B/RESULT",
                    "apply": "return JSON.parse(message).IrReceived.IRHVAC.FanSpeed;"
                }
            },
            "accessory": "mqttthing",
            "temperatureDisplayUnitsValues": [
                "off",
                "on"
            ],
            "swingModeValues": [
                "off",
                "on"
            ],
            "targetHeaterCoolerValues": [
                "Auto",
                "Heat",
            ],
            "restrictHeaterCoolerState": [
                1,
                2
            ]
        }
