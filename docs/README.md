<div align="center">

# Nhật ký thay đổi</div>

<div align="center" style="font-size:xx-small">(✨: Tính năng, chức năng mới. 🐛: Chỉnh lỗi. ☑: Giải quyết công việc, issue) </div>

#

## [v.3.26.0514.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32605140-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32605140-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32605140-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32605140-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32605140-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32605140-NasDHSolutions.json)</sup></sup></sub>
- ✨: Yêu cầu: Bổ sung màu đối thuốc cần lưu ý thi ra toa #752
	
	- Cập nhật: MEDICINE
		- Cập nhật script:

	![](https://i.vgy.me/QTY4zE.png)

		```sql
		DO $$
		BEGIN
			IF NOT EXISTS (
				SELECT 1
				FROM information_schema.columns
				WHERE table_schema = 'current'
				  AND table_name = 'dmthuoc'
				  AND column_name = 'color_luuy'
			) THEN
				ALTER TABLE current.dmthuoc
				ADD COLUMN color_luuy VARCHAR;
			END IF;
			COMMENT ON COLUMN current.dmthuoc.color_luuy
			IS 'Màu thuốc cần lưu ý khi ra toa';
		END
		$$;
		```
	- Mở danh mục thuốc: menu `Danh mục/Thuốc, hóa chất, VTTH, .../Thuốc`

	- Thao tác cập nhật thêm màu: `Chỉnh` chọn màu cần thêm --> `Lưu`

	![](https://i.vgy.me/8SV658.png)

	- Thao tác bỏ thêm màu: `Chỉnh` chọn màu `Transparent` --> `Lưu`

	![](https://i.vgy.me/nGK9Wd.png)

	Lưu ý: 
		- Thao tác thêm màu sẽ cập nhật lại tất cả thuốc đã thêm màu trước đó (nếu có)
		- Thao tác bỏ thêm màu: chỉ bỏ màu của thuốc được chọn

- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/752

## [v.3.26.0429.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32604290-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32604290-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32604290-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32604290-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32604290-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32604290-NasDHSolutions.json)</sup></sup></sub>
- 🐛: Lỗi - Medicine: Lỗi đồng bộ chứng từ nhập nhà thuốc lên Misa (Phúc Gia Khang)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/835

- 📕: Nguyên nhân : Đồng bộ hàng hoá thiếu trước khi gửi chứng từ nhập kho
- 📕: Xử lý : Do ban đầu hệ thống MISA hạn chế lượt gọi kết nối nên thống bỏ bước đồng bộ hàng hoá trước khi gửi chứng từ nhập kho.
=> Mở lại chức năng đồng bộ hàng hoá trước khi gửi chứng từ nhập kho. Nếu sử dụng chức năng đồng bộ hàng loạt thì đồng bộ mỗi 3 chứng từ sẽ delay 2 giây 

![](https://i.vgy.me/qJAZm8.png)

## [v.3.26.0318.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32603180-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32603180-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32603180-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32603180-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32603180-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32603180-NasDHSolutions.json)</sup></sup></sub>

- 🐛: Sửa lỗi Nhập chứng từ không lưu được khi chỉnh giá xuất.
![](https://lh3.googleusercontent.com/pw/AP1GczPH59sDXiWNaXA4XUvIOU7YAspC0ZPr6Pn-ErVQax7l4ZzSQbNEOnm1PcXROIUZq5nopStgANVWHNXo4iLR6IJ1pGez75TlLIBJcnnJeEp3VhldyLDGkx3PmZf90RKPDk7wgEDC8HvFHU9pflRqBVoW=w1654-h879-s-no-gm?authuser=0)
![](https://lh3.googleusercontent.com/pw/AP1GczODylJhis1_1Y-RbZqMfb8LCgvlwW6sZw1G0I0uolV3EPIJnVgTx5j9BuDBO9389IHaJP_kJBA5QtPUoBvEM8Df1jHXIQaGe6oLFWYsGRSj1ERkLU87qGBoEhRLZMyFnH3UKkNHBeJjTA6_ba_3smNh=w1654-h879-s-no-gm?authuser=0)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/792

## [v.3.26.0130.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601300-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601300-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601300-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601300-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601300-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601300-NasDHSolutions.json)</sup></sup></sub>
- 🐛: Khi chọn thuốc nhập số lượng tối đa nhưng không check Giới tính báo lỗi
![](https://i.vgy.me/IZQJQX.gif)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/645

## [v.3.26.0121.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601210-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601210-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601210-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601210-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601210-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601210-NasDHSolutions.json)</sup></sup></sub>
- ✨: Yêu cầu - Prescription bổ sung cảnh báo hoặc chặn thuốc vượt quá số lượng trên toa và theo giới tính theo từng loại thuốc #645
[Mô tả](https://github.com/dhhiswork/Mo-ta-he-thong/blob/main/Thong-mo-ta-chuc-nang-canh-bao-vuot-qua-so-luong-thuoc-va-gioi-tinh-su-dung.md)
![](https://i.vgy.me/ZGBeka.png)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/645

## [v.3.26.0119.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601190-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601190-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601190-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601190-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601190-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601190-NasDHSolutions.json)</sup></sup></sub>
- ✨: Yêu cầu - Prescription bổ sung cảnh báo hoặc chặn thuốc vượt quá số lượng trên toa và theo giới tính theo từng loại thuốc #645
[Mô tả](https://github.com/dhhiswork/Mo-ta-he-thong/blob/main/Thong-mo-ta-chuc-nang-canh-bao-vuot-qua-so-luong-thuoc-va-gioi-tinh-su-dung.md)
![](https://i.vgy.me/Lg8rMG.png)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/645

## [v.3.26.0115.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601150-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601150-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601150-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601150-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601150-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601150-NasDHSolutions.json)</sup></sup></sub>

- ✨: Danh mục thuốc => Cập nhật `[Nguồn quỹ BHYT]` không phụ thuộc `[Nguồn khác]`.
![](https://lh3.googleusercontent.com/pw/AP1GczMrxrqkiYjTi_0RppPx2_RDLv5xddc6CbFIvjkg6NOcci5gDsyNKnJ4P9crZ3FJMGXLVbiXpmDyAJUS9lALYjmu1Ku1CvOCVJc9mLXWI8TKz-yeMXFo5YRY0K6lillcft0a4nsEE9ZZJX4z1sx6BqSm=w1316-h879-s-no-gm?authuser=0)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/611

## [v.3.26.0111.1]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601111-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601111-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601111-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601111-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601111-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601111-NasDHSolutions.json)</sup></sup></sub>

- 🐛: Sửa lỗi chức năng nhập chứng từ hiển thị sai Tổng tiền hóa đơn nhập hàng khi có chiết khấu.
![](https://lh3.googleusercontent.com/pw/AP1GczPXG80JDuGFaavG9wdMcOfYtAN_GTcEvfxT7OWPYrVmhvWfIHuatOYecUAHgJwfKLkW22CHDSAzvnVTn9NViF_3VwLEiTWQzaf47pkx-aEb6xZxovfLWqZo564AE9tI9uF60qDWn77xXWMgc1BTV5sJ=w1654-h879-s-no-gm?authuser=0)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/688

## [v.3.26.0111.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601110-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601110-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601110-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601110-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601110-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601110-NasDHSolutions.json)</sup></sup></sub>

- ✨: Bổ sung chức năng không chọn loại toa thuốc trên danh mục thuốc.
![](https://lh3.googleusercontent.com/pw/AP1GczPP-GpNDS0NOPOYv081KRN0aqJGAeyq2vKgW5C52Hn5sc0FZs8rpn2yijT872S3vzZbqNpPYA5uIMbfgIDAiVFwf87ubKrYxSXQi9lLJaWzoUmvb14Jq2Wapj74trAEuLlhOoTYmsPMxmDZQRnbRZ5l=w1314-h879-s-no-gm?authuser=0)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/595

## [v.3.26.0109.1]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601091-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601091-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601091-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601091-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601091-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601091-NasDHSolutions.json)</sup></sup></sub>

- ✨: Cập nhật tiêu đề `Tách riêng mỗi thuốc 1 toa` -> `Tách toa`.
![](https://lh3.googleusercontent.com/pw/AP1GczMIQ0ekH2Ixv-opiyRbhWpVeyB9bsuwrZH_y9ZciQkVe58KB3PGX99k6ma_g5PKX5DBKbO-BG4OBAKybRJBzii-sCvrQZFVvrHchw_M-PpZXXVIN0DDhCeKMg2LcmAKpU8TaKeCNsaVTasJhAJsFXj1=w1324-h879-s-no-gm?authuser=0)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/595

## [v.3.26.0109.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601090-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601090-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601090-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601090-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601090-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32601090-NasDHSolutions.json)</sup></sup></sub>

- ✨: Bổ sung loại toa thuốc theo mô tả: [ARV/Thuoc-ARV-quy-toan-cau.md](https://github.com/dhhiswork/Mo-ta-he-thong/blob/main/ARV/Thuoc-ARV-quy-toan-cau.md).
![](https://lh3.googleusercontent.com/pw/AP1GczMdaYmMm7qMpf-Con5twZSsDoHxp4XvYPMkeWoV_ZKYrGZ1PV19lnsguHU-yWAQEFWNr_SsfzbSEMJjcP5iPqs7fzkKVEhZUMnLwMBdAEpe971x1oM3PNhe1N1TFTTVZegDbPeSGKXvMUdSCbycXr-b=w1324-h879-s-no-gm?authuser=0)
![](https://lh3.googleusercontent.com/pw/AP1GczNTaEYB8ZL13PbJsFklAf8Q1HwVLrHh97T_Qpe_jHx43zpP9O0E4SPiPxcf3f3G95KlkKlONaCfdlqPfz-bggsQLn8HRdVqsjihBeY_HJ47MZlKaX5-jmmOVeWWunhU63qjFM_uSE4gYDUgzQj2XX-z=w1324-h879-s-no-gm?authuser=0)
![](https://lh3.googleusercontent.com/pw/AP1GczMGGUEvkgbwRKkgP8UHB9DAO9NwGKNlCUM9dtVfpwx6tJt4U-u5_5vwCP2ZAiHY-btzkpl_YQleGdgbjGGqwU_PqZepldWojLbmZ8MN-lAhIfH5yzrUxYuGnoVXMlv2LI4_n-gXrpZ7irk-tRBmYy33=w1324-h879-s-no-gm?authuser=0)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/595

## [v.3.25.1224.1]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512241-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512241-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512241-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512241-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512241-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512241-NasDHSolutions.json)</sup></sup></sub>
- ✨: Yêu cầu - Medicine: Hiển thị đầy đủ tên bệnh viện trên các mẫu báo cáo #618
	- Cập nhật: hiển thị đầy đủ tên đơn vị 
	
	![](https://i.vgy.me/ohd8h6.png)
	![](https://i.vgy.me/OdUXbS.png)
	![](https://i.vgy.me/ejNlpa.png)
	![](https://i.vgy.me/I4XEc1.png)
	
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/618

## [v.3.25.1224.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512240-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512240-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512240-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512240-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512240-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512240-NasDHSolutions.json)</sup></sup></sub>
- ✨: Yêu cầu - Medicine: Hiển thị đầy đủ tên bệnh viện trên các mẫu báo cáo #618
	- Cập nhật: hiển thị đầy đủ tên đơn vị
	
	![](https://i.vgy.me/ohd8h6.png)
	![](https://i.vgy.me/OdUXbS.png)
	![](https://i.vgy.me/ejNlpa.png)
	![](https://i.vgy.me/I4XEc1.png)
	
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/618

## [v.3.25.1216.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512160-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512160-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512160-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512160-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512160-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512160-NasDHSolutions.json)</sup></sup></sub>
- 🐛: Lỗi - Medicine, SecondStore Phiếu xuất kho nội bộ sai thông tin
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/664

![](https://i.vgy.me/3Itf6p.png)
![](https://i.vgy.me/vEPyS0.png)

## [v.3.25.1209.1]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512091-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512091-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512091-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512091-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512091-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512091-NasDHSolutions.json)</sup></sup></sub>

- 🐛: Sửa lỗi xuất hư hỏng thiếu thông tin mẫu tự thiết kế nội bộ.
![](https://lh3.googleusercontent.com/pw/AP1GczPXq0khW52drNfLF1wok7nb-72R6QXd7DUPLzylDqA9kfSTzG3xwO687ERiBFjtypOxHZQDQURRqwFv1AId_lxyIVYGq94dIW7lv_uiSEKFuhQ9-mk1658UtKm9L8U5mhaVJrA_t13Q6LU_OoKJMKj4=w1006-h731-s-no-gm?authuser=0)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/657

## [v.3.25.1209.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512090-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512090-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512090-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512090-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512090-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32512090-NasDHSolutions.json)</sup></sup></sub>

- 🐛: Sửa lỗi xuất hư hỏng thiếu thông tin mẫu tự thiết kế nội bộ (điều chỉnh mẫu lại theo như hình bên dưới).
![](https://lh3.googleusercontent.com/pw/AP1GczOeUmQ0-e-RzkfycsmgDB_pqXKYPe-eKq5JE8ej7h35UmXO7Y-Qv67JVZvqSBBTzSmV_otwmib1HM6OwHijK3jr0M65DJTGEX4vALmjzyznsxPIfiejVFJCWpMihFfIN7jnUbtSsdyf0It5TQTl_fHm=w1654-h879-s-no-gm?authuser=0)
![](https://lh3.googleusercontent.com/pw/AP1GczONtvtO3A491suNAgZk855w_AyU57oGQf6GZQNNyNUBRrPCUZfeR23lePs523KaCsdJ_2DqzkVVonPVVjfgnLjWW4L9eFAoFUJDsYIZ1_C-pgdhWX346I-SNoePdmeZM44SiCTt6TuF68CX48-pxpkQ=w1020-h728-s-no-gm?authuser=0)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/657

## [v.3.25.1118.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511180-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511180-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511180-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511180-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511180-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511180-NasDHSolutions.json)</sup></sup></sub>

- ✨: Form tồn kho Frozen tới cột tên hàng hóa.

## [v.3.25.1114.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511140-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511140-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511140-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511140-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511140-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511140-NasDHSolutions.json)</sup></sup></sub>

- ✨: Bổ sung chức năng in tem tại form báo cáo tồn kho.
![](https://lh3.googleusercontent.com/pw/AP1GczPJjcV-2i6j4ZAe2M2Tf8zTsRYBg8_L__lH_88Fr8vw-IVqx1g0t8_xwTgp0Fjr-cfpw5cvFk6FJESRbmLImx2fCYeAUvH1K05f59TgrxtsVGBC31bhEcXYUzr-1uBTRvVLsYmcugC0-sNbBXix2zQi=w1654-h879-s-no-gm?authuser=0)
![](https://lh3.googleusercontent.com/pw/AP1GczOhFKX6hRpHs9RmhoChSZP3PylKqb8Ck9O03oYBHKCLKjO0q_ko78S3105GkHlvbkAfK7kFwImJ5UOsab1w59kCKyE4Nq2Ai1erh3h6d6tNC5uAjkWuYskRRgOOy7p7IDi0DYX7yvxrxmfUHNaQ9l68=w894-h137-s-no-gm?authuser=0)

- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/564

## [v.3.25.1113.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511130-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511130-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511130-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511130-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511130-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32511130-NasDHSolutions.json)</sup></sup></sub>

- ✨: Bổ sung chức năng cảnh báo phiếu xuất chưa được nhận (nếu có) khi xem báo cáo nhập xuất tồn tổng hợp.
![](https://lh3.googleusercontent.com/pw/AP1GczP6o-35mafipC4GJVkF5REFI7Yq4P7mMCmpVaEk314le5uoiiEy5WlFdiTYE-LATqaX4o0xHMrpvgZN5kcF6X5vJoJpnefB6n45I6yqOtZRyr7vFnMcq6RXmIGfII2oizpOtVHTQfltoVJ89qx9Awre=w1654-h879-s-no-gm?authuser=0)

- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/615

## [v.3.25.1020.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510200-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510200-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510200-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510200-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510200-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510200-NasDHSolutions.json)</sup></sup></sub>

- ✨: Chặn/không cho phép thêm mới kho chẵn nhà thuốc hoặc cập nhật kho chẵn hiện tại về kho chẵn nhà thuốc (nếu đã tồn tại kho chẵn nhà thuốc).
![](https://lh3.googleusercontent.com/pw/AP1GczORY7W2BefTnCFR7eOm7pG-LWnBapvSp_wJ7tYdxYr4isPABb6xkOJN3nJMxU9axv3LrBN96u4weSFS1y1XXBxzSgJFS5X_ROvKZ2FCaZJoZwvQ1K1SO59mLShgMotVR1a01h8p80Z7R2pWQtZbXk7I=w1654-h879-s-no-gm?authuser=0)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/507

## [v.3.25.1019.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510190-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510190-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510190-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510190-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510190-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510190-NasDHSolutions.json)</sup></sup></sub>

- 🐛: Mẫu nghiện, hướng thần không lấy được số tiền Tổng cộng
![](https://lh3.googleusercontent.com/pw/AP1GczPNf2XKTVsSDZ2xGfaHd5ShFdDGpBaX4na-sWkuU0RhsrbZOECl2V_qceeNftLYcEBXPPPRu2s0Wdtt3fXZK0s_lNkoA8lD1i3FcXKWICNhKsuDSghlQ4A2nDgNYB-1U4G9OTOtgENTClRVH22YHU6l=w1017-h801-s-no-gm?authuser=1)
![](https://lh3.googleusercontent.com/pw/AP1GczM0FFoQC0ku5mSGSb8y9Rk7tof_kx9eKQPw_w3R9HGd-TS_h3zGJVlVCyzvNE4CIlwThYPRL_P-6sjBMCFbgrHDOQ1dcR_HuR3xXKvrruR49OOcW1tIMnqbmbfwoxLIe5OqevYgOg783hDq0wDjTP7J=w1015-h768-s-no-gm?authuser=1)

- 🐛: Mẫu C21, C31 thiếu Tổng số khoản
![](https://lh3.googleusercontent.com/pw/AP1GczN-weuh_5EE2jl4C5MgtEDnKiCuuZ3EziN-wLYrvij48qiuOTBS4yLHPcupDa5PkU2FpSZPwpWk8pjF96jaNAPp0n1riYwwfpqtnyY25LG072e_weimEF-XSqeh_CsFiJRS6B2j5YFRdPw7EeoQKR5w=w1008-h641-s-no-gm?authuser=1)
![](https://lh3.googleusercontent.com/pw/AP1GczPzJ7kygLGYY5zGBw9wkf4Ci_mxjFd3Tel_JWn50q-7JQeMdE7vqHSZ54rm1P44uCWSK3gMLoXfG6IEA-_c4hD1VY-KMzOO_6IRiVMqeoZa3k9w5WkpHQfsyHN2_lJQp6qCn6VAWOODzF76wmakbDkc=w1019-h652-s-no-gm?authuser=1)

- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/263

## [v.3.25.1016.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510160-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510160-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510160-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510160-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510160-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510160-NasDHSolutions.json)</sup></sup></sub>

- 🐛: Sửa lỗi các mẫu in tổng hợp phiếu lĩnh
=> Tổng hợp phiếu lĩnh chức năng In và In NB khi in phiếu nghiện - hướng thần thì mất tiêu đề cột Tên thuốc,...
![](https://lh3.googleusercontent.com/pw/AP1GczMoSE7_LF1ruPn9SkYRCG0vvmIlctXZGjJQAYMkFUOUyiYQAV16KnhCRyDt4TUR50pyxa2OnLs1G1ehusvB92hmY9ex7lTJTQVmb661XJmwQOdajmAaZdREd5O-1NyOFIFvGJxbtY-PL_bzi49sMkxJ=w988-h778-s-no-gm?authuser=1)
![](https://lh3.googleusercontent.com/pw/AP1GczM3UsYMt_dIDPjR-Nc-uyf1gyb1HLHYAwHq5RxMVWuEphdEnY7d1ipkNPkSAmhbskVQCsongSP69i3KUi8J9oIExxOBzyqWtrfGT_8CnMdb1m5PoA8M-MYgTwjnjMqRzAWc6vpz6seVQZaOeBKC8xtS=w972-h719-s-no-gm?authuser=1)

=> Tổng hợp phiếu lĩnh chức năng In và In NB khi in các mẫu phiếu lĩnh thuốc , nghiện, hướng thần, truyền đạm thì không tìm thấy para ghi số chứng từ thuốc `Từ số ... đến số...`
![](https://lh3.googleusercontent.com/pw/AP1GczPyVssnSGgsJPnu2M7F4cDiSuapjrC2gK-qLc0VpxD1uO5f052Rh_tmgu4UAG81VxWGf1iQbCZ8Dec0tEDfYGAi8PCkJqyY_UxvdJC0_oAZjf9yFFg9FFyJwU4zPrUMyfYxbxHDfbEeB6M7ztpHK9fC=w972-h730-s-no-gm?authuser=1)
![](https://lh3.googleusercontent.com/pw/AP1GczMUkMYnRQ0PpVvTkb_hu_IRGoL-gyICmG0jKUAT6SWoc9AXX2IHdE6kF5ooKklyZTrPGa8OWEvDy-_8D-tkweR_OY1eUJJjzmXIM-vvYcL_k3r8Vd92LgzDXxt5K9uBkUGLgtzMEsDFuKECMt8Jkard=w1083-h879-s-no-gm?authuser=1)

=> Mẫu C21 và C31 thiếu tên các group hàng hóa như thuốc, VTYT,... và chưa có tổng từng group, qua trang thì có thể bị lỗi , thiếu ngày tháng năm ở phần ký tên (lấy ngày lập phiếu)
![](https://lh3.googleusercontent.com/pw/AP1GczO-Fvl82Gab_RMjmfuk-OhwYo5ghYTocQRXhKyBLaxm9FyRGpSNehy2AFodZOrcDl52FIOH83XbJrPwM_tcZcVRLTWM06PUkhXxzcsYAdPmd-ojZ_Qu1d-OyhZBVzAQdin1yEYUdVFO8r1Cqu8O6p1i=w1017-h685-s-no-gm?authuser=1)
![](https://lh3.googleusercontent.com/pw/AP1GczMqam9hPPrFp9WE4TtgZXKkuGUa5a-2gjqoWOuK91aGRAx0gyWM2Kd8oyNJQgjIcwVjuxxYcsXhrHWbzgLDDiBsWFVBUR_vVL4HiHU_q9aTYq75M7Y9z1ceu9fGeQNdBrweLFPD9Y7dtuobr9Z4lf57=w1030-h685-s-no-gm?authuser=1)

=> Mẫu nghiện , hướng thần, truyền đạm , phiếu lĩnh thuốc,... khác tiêu đề ký tên và cách lấy ngày ký (phần mềm cũ lấy ngày lập phiếu phần mềm mới lấy ngày hiện tại), Tên khoa, mẫu mới thiếu tổng chi phí,....
`Phản hồi: Cách làm này đối với mẫu không tự thiết được. Mẫu tự thiết kế đã có footer chữ ký sẵn, đơn vị cần thì có thể tự điều chỉnh lại.`

- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/263

## [v.3.25.1015.1]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510151-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510151-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510151-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510151-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510151-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510151-NasDHSolutions.json)</sup></sup></sub>

- 🐛: Sửa lỗi mẫu in C21, C31 mặc định Tiêu đề cột B thiếu chữ `phẩm chất`: Medicine và SecondStore
![](https://lh3.googleusercontent.com/pw/AP1GczOsxGd5C4S5anmAfV2bINNHmdWkpBsQ0DBoUepLhr5Z7IJWFH8ozKYZQDhItUUJhtzgH7NGVKmyZfQEe-ENYsbUCHi9sA8EfndH9FN8I39x4ww4GqsWjAMKw6lIzUoBARoGFXlQ61zg1jz2RaqjUdUH=w921-h879-s-no-gm?authuser=1)

- 🐛: Sửa lỗi mẫu in N-HT sẽ báo lỗi ở lần in mẫu hướng thần nếu chọn khoa mà không chọn phiếu xuất cụ thể khi in N-HT ở Xuất tủ trực và Xuất khoa phòng. Medicine và SecondStore
![](https://lh3.googleusercontent.com/pw/AP1GczOR4UaEDLOWIP967d5osQRFfYcJv8EX1d-C36JZmeFZESGpmYwAibaOhkudfDUHsL-ahCHOZB3wKnk6AYQGxBPQY6Pllgp-T5rHgeSUqdRSxj8MalMeJxZ3KJ_NPlAfr_VYU54kUFbRh5qmf0giu_7a=w1654-h879-s-no-gm?authuser=1)

- 🐛: Sửa lỗi in mẫu C21, C31 trong tổng hợp phiếu lĩnh báo lỗi ở Medicine và SecondStore
![](https://lh3.googleusercontent.com/pw/AP1GczNdh4WJwR7L9sQqJto7Jeol1Cn11tzgq8XivNT1hYGpIGqKgf8G0dJAnQLmWF-nCSOQZtqfYQbnlOHCwfnMlCLWTMhOgfe4z-hhgNcGOi85mDSzIZWcFDZQCcxXpuMyNFNbynRptOFMQQMxQvdt4yRS=w1649-h879-s-no-gm?authuser=1)
![](https://lh3.googleusercontent.com/pw/AP1GczNA9Z8JE0Rayer-CUPBNzTNVw-kHjv1mkT-t2OBTnVw9EEbTyoUo9z5KeLukJVg6LVNFeGqJtqMmk3xspQYzOiRhDaD4QVZQpxR2KG1q7xPIQoGUF4sIuF72YX7tqilD8rGUnDKmc7gEeM1LkPNzh61=w1654-h879-s-no-gm?authuser=1)

- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/263

## [v.3.25.1015.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510150-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510150-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510150-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510150-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510150-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510150-NasDHSolutions.json)</sup></sup></sub>

- 🐛: Sửa lỗi mẫu in C21, C31 mặc định Tiêu đề cột B thiếu chữ `phẩm chất`: Medicine và SecondStore
![](https://lh3.googleusercontent.com/pw/AP1GczOsxGd5C4S5anmAfV2bINNHmdWkpBsQ0DBoUepLhr5Z7IJWFH8ozKYZQDhItUUJhtzgH7NGVKmyZfQEe-ENYsbUCHi9sA8EfndH9FN8I39x4ww4GqsWjAMKw6lIzUoBARoGFXlQ61zg1jz2RaqjUdUH=w921-h879-s-no-gm?authuser=1)

- 🐛: Sửa lỗi mẫu in N-HT sẽ báo lỗi ở lần in mẫu hướng thần nếu chọn khoa mà không chọn phiếu xuất cụ thể khi in N-HT ở Xuất tủ trực và Xuất khoa phòng. Medicine và SecondStore
![](https://lh3.googleusercontent.com/pw/AP1GczOR4UaEDLOWIP967d5osQRFfYcJv8EX1d-C36JZmeFZESGpmYwAibaOhkudfDUHsL-ahCHOZB3wKnk6AYQGxBPQY6Pllgp-T5rHgeSUqdRSxj8MalMeJxZ3KJ_NPlAfr_VYU54kUFbRh5qmf0giu_7a=w1654-h879-s-no-gm?authuser=1)

- 🐛: Sửa lỗi in mẫu C21, C31 trong tổng hợp phiếu lĩnh báo lỗi ở Medicine và SecondStore
![](https://lh3.googleusercontent.com/pw/AP1GczNdh4WJwR7L9sQqJto7Jeol1Cn11tzgq8XivNT1hYGpIGqKgf8G0dJAnQLmWF-nCSOQZtqfYQbnlOHCwfnMlCLWTMhOgfe4z-hhgNcGOi85mDSzIZWcFDZQCcxXpuMyNFNbynRptOFMQQMxQvdt4yRS=w1649-h879-s-no-gm?authuser=1)
![](https://lh3.googleusercontent.com/pw/AP1GczNA9Z8JE0Rayer-CUPBNzTNVw-kHjv1mkT-t2OBTnVw9EEbTyoUo9z5KeLukJVg6LVNFeGqJtqMmk3xspQYzOiRhDaD4QVZQpxR2KG1q7xPIQoGUF4sIuF72YX7tqilD8rGUnDKmc7gEeM1LkPNzh61=w1654-h879-s-no-gm?authuser=1)

- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/263

## [v.3.25.1014.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510140-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510140-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510140-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510140-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510140-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510140-NasDHSolutions.json)</sup></sup></sub>

- 🐛: Sửa lỗi Xuất điều về: In -> chưa chuyển sang mẫu tự thiết kế:
![](https://lh3.googleusercontent.com/pw/AP1GczMtOjDG64JmLqBuDQACuyRXkLNp9PWgFQxrRRoGN7uTtvV1Cay--noELMSPlZxMw-UDAuSaSo5H0jGNZmSxRcadJeykWZlxsy2VK3xJ3oKT8mYMEsJu09-o2g6M9NqU_xHKUD9pghZeon9_6FkGvYwN=w1021-h717-s-no-gm?authuser=1)
- 🐛: Sửa lỗi tất cả các mẫu in phiếu xuất mẫu C21, C31 đều chỉ in được 1 thuốc đầu tiên và STT của mẫu C21 bắt đầu bằng số 0:
![](https://lh3.googleusercontent.com/pw/AP1GczNhC2HygA9a7RHg-mrYVMARwDGlJamGLif-3_UB4GWG0L8YSBsLY1oVnq0DHAFB6Od8B1LUk1x4l6SJfZaKAHFwaqX56-2W8WTighbxiQsbi70GWmepuCLHyv-WzpAkygGm7oVLzhVO3sD0f9oRznqc=w1119-h879-s-no-gm?authuser=1)
![](https://lh3.googleusercontent.com/pw/AP1GczPJo2rvs8Y08I58Iw7blr3h4vtZTPO9sKBM1bMEKwwyJKvugLNzUYD2ncXOjUJrJnc0H4zHhO7y-C33QtcsCsVECX1hf3GzOAZOYGc0U0isz2mz7mE94GUYaTRItxpeHFJNyy_tihcrEEE7nMRaeLVj=w1119-h879-s-no-gm?authuser=1)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/263

## [v.3.25.1009.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510090-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510090-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510090-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510090-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510090-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510090-NasDHSolutions.json)</sup></sup></sub>

- ✨: Bổ sung các mẫu tự thiết kế.
 + Xuất kho lẻ: In NB
 + Xuất tủ trực: In NB
 + Xuất khoa phòng: In NB
 + Xuất trạm xã: In NB, In N-HT
 + Xuất trả nhà CC: In, In N-HT
 + Xuất hư hỏng: In BB, In N-HT
 + Xuất khác: In NB, In N-HT
 + Xuất điều chuyển nội bộ: In NB
 + Tổng hợp phiếu lĩnh: In, In NB, In C21, In C31
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/263

## [v.3.25.1003.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510030-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510030-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510030-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510030-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510030-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32510030-NasDHSolutions.json)</sup></sup></sub>
- ✨:  Yêu cầu - Medicine Bổ sung tham số nhập chứng cho chọn hạn dùng thuốc có Ngày/tháng/năm - YEUCAU - dh-issue- #493
- ✨:  ***Bổ sung tham số `duoc.handung.theongay (0: Không sử dụng, 1: Sử dụng)` để sử dụng chức năng.*** ![](https://i.vgy.me/MPZwam.png) ![](https://i.vgy.me/a97cmh.png)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/493

## [v.3.25.0926.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32509260-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32509260-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32509260-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32509260-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32509260-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32509260-NasDHSolutions.json)</sup></sup></sub>
- 🐛: Lỗi - Thêm mã hàng hóa mới danh mục thuốc (BV Tim Mạch CT)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/514

![](https://i.vgy.me/MHpXZn.gif)

## [v.3.25.0905.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32509050-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32509050-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32509050-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32509050-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32509050-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32509050-NasDHSolutions.json)</sup></sup></sub>
- 🐛: Lỗi - Medicine chức năng ra toa nội trú (BV Ô Môn)
![](https://i.vgy.me/6cY2Pu.gif)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/449

## [v.3.25.0829.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32508290-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32508290-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32508290-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32508290-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32508290-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32508290-NasDHSolutions.json)</sup></sup></sub>
- ✨: Yêu Cầu - Medicine: Không cập nhật VAT khi nhập chứng từ vào danh mục thuốc của Nhà thuốc
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/344

- Theo mô tả : [BO_SUNG_THAM_SO_VA_OPTION_CHO_VAT_NHAP.md](https://github.com/dhhiswork/Mo-ta-he-thong/blob/main/FEES/BO_SUNG_THAM_SO_VA_OPTION_CHO_VAT_NHAP.md)

- Chỉnh thao tác chỉnh sửa thông tin thuốc sẽ lưu thêm dmthuoc.vatnhap nếu có thay đổi

![](https://i.vgy.me/3cBZXy.png)

- Nhập chứng từ kiểm tra theo tham số nhapkho.capnhatvat để cập nhật lại dmkho.vat_nhap và dmthuoc.vatnhap

![](https://i.vgy.me/1LKX9T.png)

## [v.3.25.0814.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32508140-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32508140-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32508140-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32508140-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32508140-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32508140-NasDHSolutions.json)</sup></sup></sub>
- 🐛: Lỗi - Chức năng xuất trạm xã (BV Thanh Bình)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/431

- Fix không khoá phiếu xuất khi in Phiếu xuất kho

![](https://i.vgy.me/ZIrKtP.png)

## [v.3.25.0714.1]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507141-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507141-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507141-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507141-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507141-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507141-NasDHSolutions.json)</sup></sup></sub>
 ✨: Yêu cầu - Bổ sung chức năng Chặn hoặc Cảnh báo khi sử dụng 1 vài thuốc đặc thù (có quy định số ngày tối thiểu khi sử dụng)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/249

- Điều chỉnh cho phép nhập 3 chữ số đối với songaytoithieu

![](https://live.staticflickr.com/65535/54653822938_228749bb20_b.jpg)

## [v.3.25.0714.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507140-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507140-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507140-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507140-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507140-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507140-NasDHSolutions.json)</sup></sup></sub>
- ✨: Yêu cầu - Bổ sung chức năng Chặn hoặc Cảnh báo khi sử dụng 1 vài thuốc đặc thù (có quy định số ngày tối thiểu khi sử dụng)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/249

- Theo mô tả [THUOC_SONGAYTOITHIEU.md](https://github.com/dhhiswork/Mo-ta-he-thong/blob/main/THAM_SO_HE_THONG/THUOC_SONGAYTOITHIEU.md)
- Thêm thông tin dmthuoc.songaytoithieu lên form

![](https://live.staticflickr.com/65535/54653822938_228749bb20_b.jpg)

## [v.3.25.0710.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507100-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507100-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507100-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507100-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507100-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507100-NasDHSolutions.json)</sup></sup></sub>
- 🐛:  Lỗi - Cập nhật sai giá xuất khi chỉnh chứng từ Xuất Khác - LOI - dh-issue- #357
- 🐛:  ***Chỉnh lỗi không lấy thành tiên theo tham số xuatkhac.thanhtien.*** ![](https://live.staticflickr.com/65535/54644900221_7a447e262c_b.jpg)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/357

## [v.3.25.0704.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507040-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507040-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507040-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507040-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507040-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32507040-NasDHSolutions.json)</sup></sup></sub>
- 🐛:  Lỗi - Cập nhật sai giá xuất khi chỉnh chứng từ Xuất Khác - LOI - dh-issue- #357
- 🐛:  ***Xử lý khi chỉnh chứng từ xuất khác theo tham số: xuatkhac.thanhtien=0 lấy giavat, ngược lại lấy giá xuất.*** ![](https://live.staticflickr.com/65535/54631919154_906ff198f4_b.jpg)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/357

## [v.3.25.0626.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32506260-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32506260-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32506260-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32506260-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32506260-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32506260-NasDHSolutions.json)</sup></sup></sub>
- 🐛: Yêu cầu - Medicine & SecondStore Cập nhật nội dung parameters pdonvinhan khi tùy chọn khoa thống kê -> phiếu xuất kho C31
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/288

## [v.3.25.0521.1]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505211-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505211-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505211-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505211-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505211-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505211-NasDHSolutions.json)</sup></sup></sub>
- 🐛: Lỗi - BV Phụ Sản: Key còn hạn nhưng phiếu xuất kho tự thiết kế C21, C31 báo phiên bản không hỗ trợ
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/311
- 🐛: Lỗi: Medice Phiếu xuất kho mẫu C31 và C21 hiển thị phiên bản không hỗ trợ
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/307

## [v.3.25.0521.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505210-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505210-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505210-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505210-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505210-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505210-NasDHSolutions.json)</sup></sup></sub>
- 🐛: Lỗi - BV Lai Vung: Lỗi in biên bản kiểm nhập TT22 (nghiện/hướng thần) #300
	- Cập nhật:
		![](https://i.ibb.co/7trVDfb5/Hospital-Medicine-m-Gx-LGGc-TUh.png)
		![](https://i.ibb.co/d4YST5pH/Hospital-Medicine-etti-Go-Kzy-E.png)

- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/300

## [v.3.25.0514.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505140-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505140-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505140-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505140-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505140-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505140-NasDHSolutions.json)</sup></sup></sub>
- 🐛: Lỗi - Medicine chức năng xuất tủ trực lấy số lượng từ phiếu dự trù (BV Phụ Sản)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/281

- Khoá phiếu dự trù tủ trực khi chọn chứng từ để cấp phát

![](https://i.imgur.com/qNYC3Jd.gif)

## [v.3.25.0511.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505110-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505110-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505110-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505110-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505110-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505110-NasDHSolutions.json)</sup></sup></sub>
- 🐛: Lỗi - Medicine chức năng xuất tủ trực lấy số lượng từ phiếu dự trù (BV Phụ Sản)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/281 

- Kiểm tra trạng thái phiếu dự trù đang chỉnh khi chọn và lưu 

![](https://i.imgur.com/YhwzDRW.png)

## [v.3.25.0509.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505090-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505090-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505090-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505090-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505090-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32505090-NasDHSolutions.json)</sup></sup></sub>
- ✨: Yêu cầu: Medicine, SecondStore tự thiết kế mẫu Phiếu xuất kho C31 (Thống kê -> Xuất kho -> Khoa phòng)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/195

- Cập nhật đồng bộ cho mẫu C21 và C31

![](https://i.imgur.com/rcmsGtO.png)
![](https://i.imgur.com/JkCly2f.png)
<<<<<<< HEAD

## [v.3.25.0509.0]()
- ✨: Yêu cầu: Medicine, SecondStore tự thiết kế mẫu Phiếu xuất kho C31 (Thống kê -> Xuất kho -> Khoa phòng)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/195

- Cập nhật đồng bộ mẫu C21 và C31
![](https://i.imgur.com/rcmsGtO.png)
![](https://i.imgur.com/JkCly2f.png)
=======

## [v.3.25.0429.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504290-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504290-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504290-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504290-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504290-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504290-NasDHSolutions.json)</sup></sup></sub>
- 🐛:  Lỗi - Medicine: Không in - xuất file được Sổ kiểm nhập (IN BB TT22 - Mẫu tự thiết kế) - LOI - dh-issue- #248
- 🐛:  ***Xử lý nút in trên biên bản kiểm nhập.*** ![](https://i.imgur.com/gQ7AaNF.png)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/248

## [v.3.25.0423.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504230-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504230-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504230-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504230-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504230-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504230-NasDHSolutions.json)</sup></sup></sub>
- ✨: Hỗ trợ mở chức năng ghi nhận thuốc thực phẩm chức năng (51219- PK Minh Quang)

## [v.3.25.0422.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504220-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504220-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504220-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504220-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504220-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504220-NasDHSolutions.json)</sup></sup></sub>

- ✨:  TK - Triển khai 12 trạm xã Châu Thành - Đồng Tháp - TRIENKHAI - dh-issue- #12
- ✨:  ***Bổ sung key bản quyền theo danh sách.***
- ☑: https://i.dh-his.com/hdhiswork/TRIENKHAI/issues/12

## [v.3.25.0418.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504180-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504180-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504180-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504180-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504180-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504180-NasDHSolutions.json)</sup></sup></sub>
- 🐛: Lỗi - Medicine: Không in, xuất file được Sổ kiểm nhập (IN BB TT22 - Mẫu tự thiết kế)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/248

![](https://i.imgur.com/sIilGQc.png)

## [v.3.25.0416.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504160-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504160-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504160-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504160-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504160-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32504160-NasDHSolutions.json)</sup></sup></sub>
- 🐛: Lỗi - Medicine: Mẫu C30, C20 không hiển thị thông tin Số chứng từ kèm theo
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/244

- Fix lỗi thiếu thông tin số chứng từ kèm theo trên C20 và C30 tự thiết kế

![](https://i.imgur.com/CI2RIZT.png)
![](https://i.imgur.com/OwsMWqo.png)

## [v.3.25.0325.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503250-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503250-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503250-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503250-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503250-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503250-NasDHSolutions.json)</sup></sup></sub>

- ✨: Bổ sung mẫu tự thiết kế khi in mẫu xuất thuốc `Nghiện/Hướng thần/Tiền chất`.
![](https://i.imgur.com/BadYQQZ.png)
![](https://i.imgur.com/KI4hrSd.png)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/106

## [v.3.25.0309.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503090-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503090-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503090-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503090-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503090-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503090-NasDHSolutions.json)</sup></sup></sub>
- ✨: Tích hợp với hệ thống MISA - PHÚC GIA KHANG Bổ sung trường giá trị nhập kho cho phiếu mua hàng
- ☑: https://i.dh-his.com/hdhiswork/DUAN/issues/2

![](https://i.imgur.com/g3801VD.png)

## [v.3.25.0306.6]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503066-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503066-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503066-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503066-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503066-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503066-NasDHSolutions.json)</sup></sup></sub>
- ✨: Tích hợp với hệ thống MISA - PHÚC GIA KHANG - gửi chứng từ nhập kho bỏ giá trị cột thuế GTGT
- ☑: https://i.dh-his.com/hdhiswork/DUAN/issues/2

![](https://i.imgur.com/tzX96Xm.png)
![](https://i.imgur.com/Ftu2cUT.png)

## [v.3.25.0306.5]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503065-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503065-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503065-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503065-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503065-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503065-NasDHSolutions.json)</sup></sup></sub>
- ✨: Tích hợp với hệ thống MISA - PHÚC GIA KHANG - Bổ sung Form gửi chứng từ nhập kho hàng loạt
- ☑: https://i.dh-his.com/hdhiswork/DUAN/issues/2

![](https://i.imgur.com/C5LQHTi.png)

## [v.3.25.0306.4]()
- ✨: Tích hợp với hệ thống MISA - PHÚC GIA KHANG - Bổ sung Form gửi chứng từ nhập kho hàng loạt
- ☑: https://i.dh-his.com/hdhiswork/DUAN/issues/2

![](https://i.imgur.com/C5LQHTi.png)

## [v.3.25.0306.3]()
- ✨: Tích hợp với hệ thống MISA - PHÚC GIA KHANG - Bổ sung Form gửi chứng từ nhập kho hàng loạt
- ☑: https://i.dh-his.com/hdhiswork/DUAN/issues/2

![](https://i.imgur.com/C5LQHTi.png)

## [v.3.25.0306.2]()
- ✨: Tích hợp với hệ thống MISA - PHÚC GIA KHANG - Bổ sung Form gửi chứng từ nhập kho hàng loạt
- ☑: https://i.dh-his.com/hdhiswork/DUAN/issues/2

![](https://i.imgur.com/C5LQHTi.png)

## [v.3.25.0306.1]()
- ✨: Tích hợp với hệ thống MISA - PHÚC GIA KHANG - Bổ sung Form gửi chứng từ nhập kho hàng loạt
- ☑: https://i.dh-his.com/hdhiswork/DUAN/issues/2

![](https://i.imgur.com/C5LQHTi.png)

## [v.3.25.0303.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503030-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503030-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503030-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503030-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503030-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32503030-NasDHSolutions.json)</sup></sup></sub>

- 🐛: Form `[BC sử dụng thuốc, hóa chất, VTTH] => Tab [BC sử dụng thuốc, hóa chất, VTTH theo nhóm điều trị] => Tab [Theo thành tiền]`: Sửa lỗi sai cột `[Đơn giá]`.
![](https://i.imgur.com/RCqDzFY.png)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/100

## [v.3.25.0226.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502260-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502260-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502260-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502260-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502260-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502260-NasDHSolutions.json)</sup></sup></sub>

- 🐛: Form `[Xuất kho] => [Xuất kho lẻ]`: Sửa lỗi in phiếu (ra máy in) không khóa phiếu.
![](https://i.imgur.com/Tli3ofU.png)
- 🐛: Form `Nhập kho] => [Nhập chứng từ]`: Sửa lỗi cột `[Mã số]` không tự ghép các giá trị sau thành 1 chuỗi khi in.
![](https://i.imgur.com/Bgnufai.png)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/93

## [v.3.25.0225.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502250-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502250-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502250-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502250-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502250-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502250-NasDHSolutions.json)</sup></sup></sub>

- ✨: Tại form `[Tiện ích] => [Biên bản kiểm nhập]` bổ sung control hỗ trợ người dùng lọc các chứng từ có mặt hàng `[Tiện ích]`. Theo [Mô tả [DỰ ÁN] tách hàng hóa [Tiện ích] kho nhà thuốc](https://github.com/dhhiswork/Mo-ta-he-thong/blob/main/M%C3%B4%20t%E1%BA%A3%20%5BD%E1%BB%B0%20%C3%81N%5D%20t%C3%A1ch%20h%C3%A0ng%20h%C3%B3a%20%5BTi%E1%BB%87n%20%C3%ADch%5D%20kho%20nh%C3%A0%20thu%E1%BB%91c.md).
![](https://i.imgur.com/CBQOQSX.png)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/67

## [v.3.25.0224.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502240-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502240-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502240-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502240-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502240-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502240-NasDHSolutions.json)</sup></sup></sub>

- 🐛: Sửa lỗi phiếu trả thuốc/VTYT,... tự thiết kế bị thiếu thông tin.
![](https://i.imgur.com/c5RP2qA.png)
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/87

## [v.3.25.0220.1]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502201-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502201-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502201-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502201-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502201-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502201-NasDHSolutions.json)</sup></sup></sub>
- ✨: Yêu cầu: Hỗ trợ mẫu tự thiết kế phiếu nhập kho và xuất kho trên Medicine và trên SecondStore - Fix lỗi lấy thiếu số HĐ của phiếu xuất kho
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/49

![](https://i.imgur.com/NDmQrxe.png)

## [v.3.25.0220.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502200-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502200-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502200-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502200-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502200-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502200-NasDHSolutions.json)</sup></sup></sub>
- ✨: Yêu cầu: Hỗ trợ mẫu tự thiết kế phiếu nhập kho và xuất kho trên Medicine và trên SecondStore
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/49

![](https://i.imgur.com/7GM89xG.png)
![](https://i.imgur.com/MMefKpc.png)

## [v.3.25.0218.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502180-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502180-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502180-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502180-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502180-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502180-NasDHSolutions.json)</sup></sup></sub>

- 🐛: `Form [Xuất khác]`: Sửa lỗi khi thực hiện in ra máy in, nhưng không khóa phiếu xuất.
- ☑: https://i.dh-his.com/hdhiswork/LOI/issues/78

## [v.3.25.0215.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502150-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502150-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502150-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502150-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502150-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32502150-NasDHSolutions.json)</sup></sup></sub>

- ✨: Bổ sung mẫu in tự thiết kế chức năng tổng hợp phiếu trả toa nội trú.
➡️ Phiếu tự thiết kế trang in [Tổng hợp phiếu trả]
![](https://i.imgur.com/ZPE2FG8.png)
➡️ Phiếu tự thiết kế trang in [Tổng hợp phiếu trả Nghiện/Hướng thần/Tiền chất]
![](https://i.imgur.com/e6ikk7q.png)
➡️ Kết quả [Phiếu trả lại thuốc]
![](https://i.imgur.com/rRTGngd.png)
➡️ Kết quả [Phiếu trả lại máu]
![](https://i.imgur.com/ja55dzy.png)
➡️ Kết quả [Phiếu trả lại VTYT tiêu hao]
![](https://i.imgur.com/B4obAx7.png)
➡️ Kết quả [Phiếu trả lại hóa chất]
![](https://i.imgur.com/bCvTc4d.png)
➡️ Kết quả [Phiếu trả lại dịch truyền]
![](https://i.imgur.com/8Pgl1WZ.png)
➡️ Kết quả [Phiếu trả lại dược liệu]
![](https://i.imgur.com/HQPtKYu.png)
➡️ Kết quả [Phiếu trả lại thuốc gây nghiện]
![](https://i.imgur.com/VHUXnql.png)
➡️ Kết quả [Phiếu trả lại thuốc hướng tâm thần (tiền chất)]
![](https://i.imgur.com/OlRZn6L.png)
- ☑: https://i.dh-his.com/hdhiswork/YEUCAU/issues/52

## [v.3.25.0122.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32501220-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32501220-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32501220-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32501220-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32501220-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32501220-NasDHSolutions.json)</sup></sup></sub>

- 🐛: Sửa lỗi Form [Xuất kho] => [Xuất bán lẻ]: Chức năng [In phiếu thu] chưa tách phiếu hàng hóa tiện ích. Lưu ý: tham số `ntbanle.sobanin`
![](https://i.imgur.com/e4bpKpa.png)
- ☑: https://i.dh-his.com/hdhiswork/DUAN/issues/3

## [v.3.25.0119.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32501190-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32501190-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32501190-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32501190-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32501190-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32501190-NasDHSolutions.json)</sup></sup></sub>

- ✨: Bổ sung chức năng quản lý và báo cáo/thống kê hàng hóa tiện ích. Theo [Mô tả [DỰ ÁN] tách hàng hóa [Tiện ích] kho nhà thuốc](https://github.com/dhhiswork/Mo-ta-he-thong/blob/main/M%C3%B4%20t%E1%BA%A3%20%5BD%E1%BB%B0%20%C3%81N%5D%20t%C3%A1ch%20h%C3%A0ng%20h%C3%B3a%20%5BTi%E1%BB%87n%20%C3%ADch%5D%20kho%20nh%C3%A0%20thu%E1%BB%91c.md)
![](https://i.imgur.com/PSRzIdx.png)
![](https://i.imgur.com/aKyZnKK.png)
![](https://i.imgur.com/Zy10X1W.png)
![](https://i.imgur.com/NI7cKWE.png)
![](https://i.imgur.com/lMk5sIW.png)
![](https://i.imgur.com/i106ch4.png)
- ☑: https://i.dh-his.com/hdhiswork/DUAN/issues/3

## [v.3.24.1230.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412300-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412300-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412300-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412300-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412300-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412300-NasDHSolutions.json)</sup></sup></sub>
- ✨: Yêu cầu - Yêu cầu tích hợp với hệ thống MISA - PHÚC GIA KHANG (xử lý lại)
- ☑: https://github.com/dhhiswork/YeuCau/issues/65

![](https://i.imgur.com/qvdd6nt.png)

## [v.3.24.1227.1]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412271-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412271-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412271-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412271-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412271-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412271-NasDHSolutions.json)</sup></sup></sub>
- ✨: Yêu cầu - Các module add mã chính thức 96176 Phòng khám đa khoa Y Đức Sài Gòn - YEUCAU
- ☑: https://i.dh-his.com/test/YEUCAU/issues/4

## [v.3.24.1227.0]()
- ✨: Yêu cầu - Các module add mã chính thức 96176 Phòng khám đa khoa Y Đức Sài Gòn - YEUCAU
- ☑: https://i.dh-his.com/test/YEUCAU/issues/4

## [v.3.24.1223.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412230-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412230-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412230-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412230-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412230-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412230-NasDHSolutions.json)</sup></sup></sub>
- ✨: Phúc Gia Khang - Tích hợp hệ thống MISA AMIS vào phần mềm : hoàn thiện chức năng gửi chứng từ nhập kho.
- ☑: https://github.com/dhhiswork/To_lap_trinh/issues/12

![](https://i.imgur.com/0nB6Jr4.png)
![](https://i.imgur.com/Dl2wZf9.png)

## [v.3.24.1220.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412200-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412200-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412200-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412200-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412200-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412200-NasDHSolutions.json)</sup></sup></sub>
- ✨: Yêu cầu - Các module add mã tạm 96151 Phòng khám đa khoa Sài Gòn Y Đức ·
- ☑: https://github.com/dhhiswork/YeuCau/issues/60

## [v.3.24.1219.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412190-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412190-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412190-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412190-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412190-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412190-NasDHSolutions.json)</sup></sup></sub>
- ✨: Phúc Gia Khang - Hoàn thiện tính năng gửi chứng từ nhập kho qua MISA AMIS
- ☑: https://github.com/dhhiswork/To_lap_trinh/issues/12

![](https://i.imgur.com/Q8zW3jw.png)
![](https://i.imgur.com/Kt4tErD.png)

## [v.3.24.1218.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412180-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412180-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412180-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412180-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412180-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412180-NasDHSolutions.json)</sup></sup></sub>
- ✨: Tính năng hợp đồng riêng Phúc Gia Khang - gửi chứng từ nhập kho đồng bộ qua MISA AMIS
- ☑: https://github.com/dhhiswork/To_lap_trinh/issues/12

![](https://i.imgur.com/Filnp4Q.png)

## [v.3.24.1215.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412150-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412150-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412150-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412150-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412150-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412150-NasDHSolutions.json)</sup></sup></sub>

- ✨: Tách mẫu tự thiết kế phiếu lĩnh thuốc `Nghiện` và mẫu phiếu lĩnh thuốc `Hướng thần/Tiền chất` đối với tham số `bcnghienht = 2`. Bổ sung para `tieude` và `tieudephu` cho mỗi phiếu.
![image](https://github.com/user-attachments/assets/b517164a-bf8c-48b1-ade7-ef6e91ed7a1b)
![image](https://github.com/user-attachments/assets/b26fffa2-e0a0-4fda-9556-821b51a20397)
![image](https://github.com/user-attachments/assets/13b7687b-10b5-4feb-b188-a5ee3408a635)
- ☑: https://github.com/dhhiswork/YeuCau/issues/46

## [v.3.24.1214.0]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412140-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412140-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412140-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412140-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412140-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32412140-NasDHSolutions.json)</sup></sup></sub>

- ✨: Chức năng `[Cập nhật phiếu Chưa lĩnh - Chưa trả]`: Xử lý nghiệp vụ đối với các loại xuất toa người bệnh (loaixn=xbb) có sử dụng tạm xuất (tamxuat). Những hàng hóa có thay đổi khi xử lý, sẽ cập nhật giá trị `current.tkdatatemp.da_can_kho = 1`.
- ☑: https://github.com/dhhiswork/Loi/issues/73

## [v.3.24.1130.2]() <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32411302-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32411302-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32411302-NasDHSolutions.json)</sup></sup></sub> <sub><sup><sup>[⬇️OneDrive](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32411302-OneDrive.json) [⬇️GoogleStorage](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32411302-GoogleStorage.json) [⬇️NasDHSolutions](https://code-dh-hospital.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32411302-NasDHSolutions.json)</sup></sup></sub>
- 🐛: Lỗi - Theo dõi dữ liệu tủ trực ![](https://i.imgur.com/YCRL8N4.png) ![](https://i.imgur.com/HHOeWf5.png)
- ☑: https://github.com/dhhiswork/Loi/issues/62

## [v.3.24.1130.1]()
- 🐛: Lỗi - Theo dõi dữ liệu tủ trực ![](https://i.imgur.com/YCRL8N4.png) ![](https://i.imgur.com/HHOeWf5.png)
- ☑: https://github.com/dhhiswork/Loi/issues/62

## [v.3.24.1130.0]()
- 🐛: Lỗi - Theo dõi dữ liệu tủ trực ![](https://i.imgur.com/YCRL8N4.png) ![](https://i.imgur.com/HHOeWf5.png)
- ☑: https://github.com/dhhiswork/Loi/issues/62

## [v.3.24.1112.1]() <sub><sup><sup>[⬇️OneDrive](https://tolaptrinh.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32411121-OneDrive.json) [⬇️GoogleStorage](https://tolaptrinh.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32411121-GoogleStorage.json) [⬇️NasDHSolutions](https://tolaptrinh.github.io/directTo/?&redirect_url=https%3A%2F%2Fo-dh-007-default-rtdb.asia-southeast1.firebasedatabase.app%2FdirectTo%2FHospitalMedicineexe%2F32411121-NasDHSolutions.json)</sup></sup></sub>

- 🐛: Sửa lỗi chưa ghi nhận trạng thái da_can_kho đối với toa tạm kho tủ trực khi thực hiện [Cập nhật xuất] tủ trực.
- ☑: https://github.com/dh-hos/To_Lap_Trinh/issues/662

## [v.3.24.1112.0]()

- 🐛: Sửa lỗi chưa ghi nhận trạng thái da_can_kho đối với toa tạm kho tủ trực khi thực hiện [Cập nhật xuất] tủ trực.
- ☑: https://github.com/dh-hos/To_Lap_Trinh/issues/662

## [v.3.24.1013.0]()

- ✨: Thực hiện - Xử lý nghiệp các loại xuất dựa vào trạng thái cân kho đối với các loại xuất: Xuất khoa phòng, Xuất khác.
- ☑: https://github.com/dh-hos/To_Lap_Trinh/issues/670

## [v.3.24.1006.0]()

- ✨: 💼 Medcine, SecondStore Thực hiện - Lưu trạng thái đã cân kho vào bảng tạm.
- ☑: https://github.com/dh-hos/To_Lap_Trinh/issues/667

## [v.3.24.0929.1]()
- ✨: Form `[Xuất khác]`: Lưu/Hiển thị/In cột `[Thành tiền]` theo `[Giá VAT]` hoặc `[Giá xuất]` phụ thuộc vào tham số `[xuatkhac.thanhtien]`.
- ☑: https://github.com/dh-hos/To_Lap_Trinh/issues/653

## [v.3.24.0929.0]()

- ✨: Form `[Xuất khác]`: Lưu/Hiển thị/In cột `[Thành tiền]` theo `[Giá VAT]` hoặc `[Giá xuất]` phụ thuộc vào tham số `[xuatkhac.thanhtien]`.
- ☑: https://github.com/dh-hos/To_Lap_Trinh/issues/653

## [v.3.24.0928.0]()

- ✨: Bổ sung chức năng in hàng vượt định mức theo mẫu tự thiết kế. Riêng PK Hồng Đức có thể sử dụng mẫu này để khỏi phải tự thiết kế lại mẫu từ đầu: [XRptBCTDinhMucTonKho_HongDuc.zip](https://github.com/user-attachments/files/17173782/XRptBCTDinhMucTonKho_HongDuc.zip)
- ☑: https://github.com/dh-hos/To_Lap_Trinh/issues/651

## [v.3.24.0921.0]()
- 🐛: **💼**: **_Lỗi - Bảng kê xuất tổng hợp hiển thị sai đơn giá xuất_**
- 🐛: ***Chức năng trả nhà cung cấp***: lấy giavat làm Đơn giá khi in ![](https://i.imgur.com/NJl17HI.png) ![](https://i.imgur.com/vAlmoVX.png)
- 🐛: ***Chức năng tổng hợp xuất, lấy giavat làm Đơn giá đối với loại xuất trả nhà cung cấp***: ![](https://i.imgur.com/oZ67LCp.png) 
- ☑: https://github.com/dh-hos/dhg.hospitalmedicine/issues/50

## [v.3.24.0625.0]()
- ✨: Yêu cầu - Medicine bổ sung trường thông tin thầu
- ![](https://i.imgur.com/PfmVmQe.png)
- ☑: https://github.com/dh-hos/To_Lap_Trinh/issues/415

## [v.3.24.0618.0]()
- 🐛: Hiệu chỉnh báo cáo sử dụng thuốc, không thống kê phần xuất từ kho lẻ xuống tủ trực vào cột xuất khác.
- ☑: https://github.com/dh-hos/dhg.hospitalmedicine/issues/48

## [v.3.24.0603.1]()
- ✨: Cập nhật Msi trên Telegram

## [v.3.24.0603.0]()
- ✨: Bổ sung nhập liệu ma_cskcb_thuoc
- ![](https://i.imgur.com/Xk4ImFE.png)
- ☑: https://github.com/dh-hos/To_Trien_Khai/issues/57
- ☑: https://github.com/dh-hos/To_Ho_Tro/issues/20