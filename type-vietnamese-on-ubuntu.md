# Gõ Tiếng Việt trong Linux

Ghi chú cách dùng IBus Bamboo để gõ Tiếng Việt mà không bị lỗi gạch chân như các bộ gõ khác.

## Cài đặt

```bash
sudo add-apt-repository ppa:bamboo-engine/ibus-bamboo
sudo apt-get update
sudo apt-get install ibus ibus-bamboo --install-recommends
ibus restart
env DCONF_PROFILE=ibus dconf write /desktop/ibus/general/preload-engines "['BambooUs', 'Bamboo']" && gsettings set org.gnome.desktop.input-sources sources "[('xkb', 'us'), ('ibus', 'Bamboo')]"
```

Các distro khác Ubuntu, vui lòng xem tại [BambooEngine/ibus-bamboo](https://github.com/BambooEngine/ibus-bamboo).

## Cấu hình

### GNOME

1. Vào **Settings > Keyboard > Input Sources**.
2. Thêm **English (US)** và **Vietnamese (Bamboo)**.
3. Trong **Options** bật **Allow different sources for each window** để tự chuyển khi đổi app.

### Môi trường Desktop khác

```bash
sudo im-config -s ibus
```

1. Tìm **Ibus Preferences** hoặc chạy:
   ```bash
   ibus-setup
   ```
2. Tab **Input Method > Add**, chọn Vietnamese - Bamboo.
3. Khởi động lại IBus:
   ```bash
   ibus restart
   ```

## Cách tự động chuyển Terminal sang Tiếng Anh khi mở

1. Tạo script:

```bash
nano ~/.config/ibus-switch-to-english.sh
```

2. Thêm nội dung:

```bash
#!/bin/bash
ibus engine xkb:us::eng
```

3. Cấp quyền:

```bash
chmod +x ~/.config/ibus-switch-to-english.sh
```

4. Thêm vào cuối `~/.bashrc` hoặc `~/.zshrc`:

```bash
~/.config/ibus-switch-to-english.sh
```

5. Tải lại:

```bash
source ~/.bashrc
# hoặc nếu dùng zsh
source ~/.zshrc
```

## Sử dụng

Khi bật bộ gõ, mở menu **vi**, kiểm tra phím tắt và bật **Shift + ~** để chuyển chế độ gõ.

> Đây là tính năng nổi bật của IBus Bamboo giúp không bị gạch chân.

### Các ứng dụng hỗ trợ tốt chế độ không gạch chân:

- **Terminal** (trừ Surrounding Text)
- **Chrome / Electron apps (VSCode)**: dùng ForwardKeyEvent
- **Firefox**: DevTools cần bật chế độ Forward as Commit
- **LibreOffice / Pidgin / Sublime Text**: OK
- **Steam**: không hỗ trợ IBus, dùng workaround khác

### Lưu ý

- Phím tắt đổi en-vi mặc định: `Win + Space`
- Tránh XTestFakeKeyEvent vì dễ lỗi
- Một số web/app yêu cầu dùng chế độ có gạch chân (ví dụ CodeMirror, Select2)
- Steam/Spotify không hỗ trợ IBus → Bamboo cũng không dùng được

## Elementary OS

1. Bật ibus:
```bash
sudo im-config -s ibus
```

2. Thêm vào startup:
```bash
ibus-daemon -drx
```

3. Cài đặt và cấu hình như hướng dẫn trên.

4. Không có icon tray → chỉnh config thủ công:
```bash
xdg-open ~/.config/ibus-bamboo/ibus-bamboo.config.json
```

Ví dụ chỉnh kiểu gõ:

```json
"InputMethod": "VNI"
```

Phím tắt chuyển en-vi mặc định của eOS: `Ctrl + Space`.

## Ngoài lề

IBus Bamboo đang là bộ gõ tiếng Việt chất lượng nhất cho Linux nhờ khả năng tắt gạch chân. Tuy nhiên vẫn còn vài lỗi nhỏ như không nhận search box.

Xem thêm: [https://github.com/BambooEngine/ibus-bamboo](https://github.com/BambooEngine/ibus-bamboo)