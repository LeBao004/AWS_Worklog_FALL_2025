---
title: "Blog 2"
date: ""
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---



# Phát trực tuyến không gián đoạn với quảng cáo được điều chỉnh trước của Olyzon và AWS Elemental MediaTailor

**Tác giả:** Thomas Buatois — ngày 24 tháng 6 năm 2025  
**Chuyên mục:** AWS Elemental MediaTailor, AWS Marketplace, Industries, Media & Entertainment, Media Services, Monetization, Partner solutions  
*Permalink | Share*

Các nhà cung cấp dịch vụ video streaming đang đối mặt với thách thức liên tục trong việc tối đa hóa doanh thu quảng cáo đồng thời duy trì mức độ tương tác của người xem. Thách thức nằm ở việc phân phối quảng cáo (ads) mượt mà, có thể tích hợp vào nội dung mà không gây trễ đệm (buffering), giảm chất lượng, hay ngắt quãng phát lại khiến người xem rời bỏ.

Đối tác AWS – Olyzon đã phát triển một giải pháp sáng tạo sử dụng preconditioned ads của AWS Elemental MediaTailor để đạt được sự cân bằng này.

---

## Giới thiệu preconditioned ads cho việc chèn quảng cáo nâng cao

MediaTailor hỗ trợ preconditioned ads, một tính năng cho phép kiểm soát tùy chỉnh quá trình ad transcoding.
Tính năng này, còn được gọi là bring-your-own-ads thông qua VAST responses, cho phép ad decision servers (ADS) bao gồm HLS và DASH manifest URLs cho các multi-bitrate ad streams đã được pre-transcoded trực tiếp trong thuộc tính VAST XML creative file.

Giờ đây, MediaTailor có thể stitch (nối) các pre-transcoded ad creatives này vào manifest mà không cần transcoding thêm.
Trước đây, MediaTailor chỉ có thể dynamically transcode ads để khớp với content stream tại thời điểm chèn, gây ra độ trễ tiềm ẩn trong quá trình phân phối quảng cáo.

---

## Cách preconditioned ads thay đổi quy trình làm việc

Trong quy trình ad insertion truyền thống, MediaTailor phải dynamically transcode quảng cáo để khớp với content stream, lưu trữ chúng, và sau đó stitch vào live stream.
Quá trình này gây ra độ trễ vì MediaTailor phải chờ nhận quảng cáo từ VAST responses của ADS trước khi bắt đầu transcoding và stitching.

Preconditioned ads giúp giảm thời gian cần thiết để chèn quảng cáo vào nội dung bằng cách loại bỏ bước transcoding.
Các quảng cáo này phải được chuẩn bị sẵn để khớp với content stream và đã được transcoded trước khi sử dụng với MediaTailor.
ADS VAST response phải bao gồm liên kết trực tiếp đến các manifest HLS và DASH đã pre-transcoded.
MediaTailor chỉ cần đăng ký quảng cáo và stitch nó vào content stream, giúp giảm thời gian giữa việc nhận VAST response và hoàn tất ad insertion.

---

## Yêu cầu VAST response cho preconditioned ads

Khác với VAST responses thông thường, trong đó MediaTailor nhận single creatives và tự transcode thành nhiều bitrate, ADS phải cung cấp VAST responses được định dạng đúng với pre-transcoded assets.

**Ví dụ VAST:**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<VAST xmlns:xsi="[http://www.w3.org/2001/XMLSchema-instance](http://www.w3.org/2001/XMLSchema-instance)" version="3.0">
    <Ad id="ad1">
        <InLine>
            <AdSystem>ExampleAdSystem</AdSystem>
            <AdTitle>ad1</AdTitle>
            <Impression><![CDATA[[https://example-impression.amazonaws.com](https://example-impression.amazonaws.com)]]></Impression>
            <AdServingId>de8e0d33-9c72-4d77-bb3a-f7e566ffc605</AdServingId>
            <Creatives>
                <Creative id="creativeId1" sequence="1">
                    <Linear skipoffset="00:00:05">
                        <Duration>00:00:30</Duration>
                        <MediaFiles>
                            <MediaFile delivery="progressive" width="1280" height="720" type="video/mp4" bitrate="533" scalable="true" maintainAspectRatio="true"><![CDATA[[https://example-ad-origin.amazonaws.com/ad1/ad1.mp4](https://example-ad-origin.amazonaws.com/ad1/ad1.mp4)]]></MediaFile>
                            <MediaFile delivery="streaming" width="1280" height="720" type="application/dash+xml" bitrate="533" scalable="true" maintainAspectRatio="true"><![CDATA[[https://example-ad-origin.amazonaws.com/ad1/index.mpd](https://example-ad-origin.amazonaws.com/ad1/index.mpd)]]></MediaFile>
                            <MediaFile delivery="streaming" width="640" height="360" type="application/x-mpegURL" bitrate="262" scalable="true" maintainAspectRatio="true"><![CDATA[[https://example-ad-origin.amazonaws.com/ad1/index_low.m3u8](https://example-ad-origin.amazonaws.com/ad1/index_low.m3u8)]]></MediaFile>
                            <MediaFile delivery="streaming" width="2560" height="1440" type="application/x-mpegURL" bitrate="1066" scalable="true" maintainAspectRatio="true"><![CDATA[[https://example-ad-origin.amazonaws.com/ad1/index_high.m3u8](https://example-ad-origin.amazonaws.com/ad1/index_high.m3u8)]]></MediaFile>
                        </MediaFiles>
                    </Linear>
                </Creative>
            </Creatives>
        </InLine>
    </Ad>
</VAST>