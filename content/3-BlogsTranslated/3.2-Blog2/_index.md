---
title: "Blog 2"
date: ""
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---




# Non-disruptive streaming with Olyzon and AWS Elemental MediaTailor preconditioned ads

**Author:** Thomas Buatois — June 24, 2025  
**Categories:** AWS Elemental MediaTailor, AWS Marketplace, Industries, Media & Entertainment, Media Services, Monetization, Partner solutions  
*Permalink | Share*

Streaming video providers face the ongoing challenge of maximizing ad revenue while maintaining viewer engagement. The challenge lies in delivering seamless advertisements (ads) that integrate into content without causing buffering, quality degradation, or playback interruptions that drive viewers away.

AWS Partner – Olyzon has developed an innovative solution using preconditioned ads from AWS Elemental MediaTailor to achieve this balance.

---

## Introducing preconditioned ads for enhanced ad insertion

MediaTailor supports preconditioned ads, a feature that enables custom control over the ad transcoding process.
This feature, also known as bring-your-own-ads through VAST responses, allows ad decision servers (ADS) to include HLS and DASH manifest URLs for multi-bitrate ad streams that have been pre-transcoded directly in the VAST XML creative file attribute.

MediaTailor can now stitch these pre-transcoded ad creatives into the manifest without further transcoding.
Previously, MediaTailor could only dynamically transcode ads to match the content stream at the time of insertion, causing potential delays in the ad delivery process.

---

## How preconditioned ads transform the workflow

In the traditional ad insertion workflow, MediaTailor must dynamically transcode ads to match the content stream, store them, and then stitch them into the live stream.
This process introduces delays because MediaTailor must wait to receive ads from the ADS's VAST responses before starting transcoding and stitching.

Preconditioned ads help reduce the time required to insert ads into content by eliminating the transcoding step.
These ads must be prepared to match the content stream and already transcoded before use with MediaTailor.
The ADS VAST response must include direct links to the pre-transcoded HLS and DASH manifests.
MediaTailor only needs to register the ad and stitch it into the content stream, reducing the time between receiving the VAST response and completing ad insertion.

---

## VAST response requirements for preconditioned ads

Unlike typical VAST responses, where MediaTailor receives single creatives and transcodes them into multiple bitrates itself, the ADS must provide correctly formatted VAST responses with pre-transcoded assets.

**VAST Example:**
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