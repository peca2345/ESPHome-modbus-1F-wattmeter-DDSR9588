# ESPHome modbus - 1F Wattmeter DDSR9588 RS485

## Components:
1F DIN WATTMETER DDSR9588 : [SHOP](https://www.aliexpress.com/i/4001201973679.html) 

## ESPHome code:
```
uart:
  id: mod_bus
  rx_pin: GPIO32
  tx_pin: GPIO33
  baud_rate: 9600
  stop_bits: 1
  parity: EVEN

modbus:
  send_wait_time: 200ms
  id: rs485

modbus_controller:
  - id: wattmeter_klima
    address: 21
    modbus_id: rs485
    setup_priority: -10
    # update_interval: 5s

sensor:
  - platform: modbus_controller
    modbus_controller_id: wattmeter_klima
    name: "klima_power"
    id: "klima_power"
    address: 0x0012
    register_count: 2
    unit_of_measurement: "W"
    value_type: FP32
    register_type: read

  - platform: modbus_controller
    modbus_controller_id: wattmeter_klima
    name: "klima_energy"
    id: "klima_energy"
    address: 0x0100
    register_count: 2
    unit_of_measurement: "kWh"
    value_type: FP32
    register_type: read
    accuracy_decimals: 2
```    
