# RMT-BIDSHOT-COMPONENTS

High-performance 4-channel bidirectional DShot component for ESP-IDF.

## Features

- Fixed 4-channel fast path
- RMT `TX_DONE` ISR arms RX immediately
- Previous frame is captured and decoded before the next TX
- Dedicated TX/RX memory blocks per channel
- Compile-time fallback when `SOC_RMT_SUPPORT_TX_SYNCHRO` is unavailable
- Minimal public API: `init`, `send`, `send_raw`, `receive`

## Layout

- `bidir_dshot.c`: component implementation
- `include/bidir_dshot.h`: public API
- `CMakeLists.txt`: ESP-IDF component registration
- `examples/basic`: minimal example project

## API

```c
esp_err_t bidir_dshot_init(const bidir_dshot_config_t *config);
esp_err_t bidir_dshot_send(const uint16_t values[4]);
esp_err_t bidir_dshot_send_raw(const uint16_t values[4], bool request_telemetry);
esp_err_t bidir_dshot_receive(bidir_dshot_reply_t replies[4], esp_err_t results[4]);
```

## Example

```c
bidir_dshot_config_t config = BIDIR_DSHOT_DEFAULT_CONFIG();
uint16_t throttle[4] = {0, 0, 0, 0};
bidir_dshot_reply_t replies[4];
esp_err_t results[4];

ESP_ERROR_CHECK(bidir_dshot_init(&config));
ESP_ERROR_CHECK(bidir_dshot_send(throttle));
ESP_ERROR_CHECK(bidir_dshot_receive(replies, results));
```
