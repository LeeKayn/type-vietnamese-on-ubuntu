# Gõ Tiếng Việt trong Ubuntu

Ghi chú cách dùng IBus Bamboo để gõ Tiếng Việt mà không bị lỗi gạch chân như các bộ gõ khác.

## Cài đặt

Chi tiết cài đặt đã ghi rõ tại [BambooEngine/ibus-bamboo](https://github.com/BambooEngine/ibus-bamboo).

```bash
sudo add-apt-repository ppa:bamboo-engine/ibus-bamboo
sudo apt install ibus-bamboo
ibus restart
```

## Cấu hình

1. Truy cập cấu hình bộ gõ **Settings > Region & Language > Input Sources**.
2. Thiết lập 2 bộ gõ gồm **English (US)** và **Vietnamese (Bamboo)**.
3. Trong mục **Options** chọn **Allow different sources for each window** để tự chuyển đổi bộ gõ khi vào các ứng dụng khác nhau.

## Sử dụng

Khi bật bộ gõ lên, mở menu **vi**, kiểm tra mục **Phím tắt** và bật **Chuyển chế độ gõ `Shift + ~`** _(nếu chưa bật)_.

> Phím tắt này rất quan trọng, nó giúp chọn đúng chế độ gõ **không gạch chân** phù hợp với ứng dụng. Đây cũng làm điểm làm **IBus Bamboo** vượt trội so với các bộ gõ Tiếng Việt khác.
>
> Nếu bạn dùng qua các bộ gõ khác trên Ubuntu _(hay các distro khác)_ như **IBus Unikey**, **IBus Teni**, **Fcitx Unikey**, ... thì tất cả chúng chỉ có tùy chọn duy nhất là chế độ **có gạch chân** _(pre-edit)_ xấu xí:
>
> - Thường bị chữ đang gõ lệch ra ngoài input.
> - Mất chữ khi chưa commit _(bằng dấu cách, dấu chấm, Ctrl, ...)_.
> - Không thể đặt lại dấu cho chữ đã commit.
> - Không hoặc kém đáp ứng với các ứng dụng có gợi ý theo từ đang gõ _(autocomplete)_.
>
> **IBus Bamboo** khắc phục tất cả nhược điểm trên khi chạy ở chế độ **không gạch chân**.
>
> Trong menu **vi** có tùy chọn **Cấu hình khác > Sửa lỗi gạch chân** có thể bật nhanh chế độ này, nhưng đáng tiếc là nó không hoạt động đúng với tất cả ứng dụng. Có thể xuất hiện lỗi gõ xong không xóa được hay thậm chí là không gõ được. Đây cũng là lý do mình viết ghi chú này.

### Các ứng dụng phổ biến

1. **Terminal**: trừ chế độ Surrounding Text ra.
2. Các ứng dụng xây dựng từ **Chromium** hoặc **Electron**: ForwardKeyEvent I _(hoặc II)_.
3. **Firefox**: Tất cả chế độ không gạch chân. Trong Dev Tools thì chỉ có chế độ Forward as commit hỗ trợ autocomplete.
4. **LibreOffice**: Tất cả chế độ không gạch chân.
5. **Pidgin**: Tất cả chế độ không gạch chân.
6. **Steam**: [_Không thể chạy Ibus trong Steam_](https://github.com/ValveSoftware/steam-for-linux/issues/781), vì thế để nhắn tin Tiếng Việt bạn cần dùng Pidgin và cài thêm plugin [Steam IM](https://github.com/EionRobb/pidgin-opensteamworks).
7. **TeamViewer**: Surrounding Text.
8. _...cần bổ sung thêm_

## Lưu ý

- Phím tắt chuyển đổi bộ gõ **en-vi** mặc định là `Win+space`. Bạn có thể thay đổi trong **Settings > Devices > Keyboard Shortcuts > Typing**.
- Tránh dùng chế độ XTestFakeKeyEvent vì nó khá chậm, thường bị mất dấu.
- Trong các website mà input có chức gợi ý, tự động sửa như Select2, CodeMirror, ... thì có thể phải thay đổi chế độ gõ khác hoặc buộc phải dùng chế độ **có gạch chân**.
- Một số ứng dụng như Steam, Teamviewer, Spotify, ... không hỗ trợ Ibus thì **IBus Bamboo** cũng bó tay.

### Ngoài lề

**IBus Bamboo** hiện tại khá tốt nhưng vẫn còn nhiều lỗi. Cơ chế gõ không gạch chân này cũng từng được **IBus Teni** đề cập trong lộ trình phát triển v2 nhưng không hiểu sao lại ngừng và bỏ luôn dự án.

## Elementary OS

**eOS** hỗ trợ ibus rất kém, không có icon trên status bar, không tự thêm ibus vào startup nên bạn cần phải tự chỉnh thủ công.

1. Kích hoạt ibus:

       sudo im-config

    Chọn `ibus` từ bảng cấu hình.
1. Thêm vào startup **System Settings > Applications > Startup**:

       ibus-daemon -drx

1. Cài đặt **Ibus Bamboo** như trên.
1. Cấu hình bộ gõ **System Settings > Keyboard > Layout > Input Method Settings**.
1. Đăng xuất.

Sau khi đăng nhập trở lại bạn có thể gõ Tiếng Việt với **IBus Bamboo**.
Tuy nhiên do không có icon trên status bar nên bạn phải đổi kiểu gõ thủ công từ tệp cầu hình.

    nano ~/.config/ibus-bamboo/ibus-bamboo.config.json

Thay đổi kiểu gõ trong `InputMethod` và lưu lại. Nếu bạn gõ mặc định kiểu **Telex** thì không cần làm bước này. Ví dụ:

    "InputMethod": "VNI"

Lưu ý phím tắt chuyển đổi bộ gõ **en-vi** mặc định của **eOS** là `Ctrl+space`.