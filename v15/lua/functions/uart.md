---
title: "UART"
slug: "uart"
description: "List of UART Lua functions in FarmBot OS"
---

# uart.list()

Returns a list of UART devices.

```lua
uart_list = uart.list()

for _number, device_path in ipairs(uart_list) do
  send_message("debug", inspect(device_path), {"toast"})
end
```

# uart.open(path, baud)

Open a UART device (typically, via USB) for reading and writing. Please note that the UART devices must be connected to the Raspberry Pi, not the Arduino.

```lua
-- device name, baud rate:
my_uart, error = uart.open("ttyAMA0", 115200)

if error then
    send_message("error", inspect(error), "toast")
    return
end

if my_uart then
    -- Wait 60s for data...
    string, error2 = my_uart.read(15000)
    if error2 then
        send_message("error", inspect(error2), "toast")
    else
        send_message("info", inspect(string), "toast")
    end

    error3 = my_uart.write("Hello, world!")

    if error3 then
        -- Handle errors etc..
    end

    my_uart.close()
end
```

# uart.read()

See documentation for `uart.open()`.

# uart.write()

See documentation for `uart.open()`.

# uart.close()

See documentation for `uart.open()`.