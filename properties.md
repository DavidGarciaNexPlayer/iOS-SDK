
# Properties

There are a wide array of properties that can be adjusted to control the behavior of various aspects of the player, from buffer time (how many seconds of streaming content are buffered before playback begins) to the behavior of the player under various error conditions (whether or not to allow audio-only playback if an unsupported video codec is detected, for example).

Properties can be set and retrieved through:

- setProperty:toValue: (NXPlayer)
- getProperty:value: (NXPlayer)
- getProperty: (NXPlayer)

Properties are identified with an integer identifier from the NXProperty enumeration.

The value of each property is an unsigned integer. For some properties, it may be necessary to cast this to a different type. See the individual property documentation for details. If no type is specified, it is safe to treat the property as an unsigned integer.

> **Note** Members of the enumeration that have not been documented, as well as values that have not yet been used are subject to change in future versions. Do not access or change undocumented properties, or your code may behave unpredictably and may break in future versions.


## enum NXProperty

Property identifiers.
These identify properties that can be set and retrieved with:

- setProperty:toValue: (NXPlayer)
- getProperty:value: (NXPlayer)
- getProperty: (NXPlayer)

### NXPropertyInitialBufferingDuration 

Number of milliseconds of media to buffer initially before beginning streaming playback (HLS, RTSP, etc.). This is the initial amount of audio and video that NexPlayer buffers when it begins playback. If further buffering is required later in the playback process, the value of the property **NXPropertyReBufferingDuration** will be used instead.

If this is set to zero, NexPlayer will automatically select the recommended buffering time based on the content type (longer for HLS, shorter for other streaming types).

-  Type: unsigned int 
-  Default: 0 (automatic) 
-  Units: msec

### NXPropertyReBufferingDuration 

Number of milliseconds of media to buffer if additional buffering is required during streaming playback (HLS, RTSP, etc.). This is the amount of audio and video that NexPlayer buffers when the buffer becomes empty during playback (requiring additional buffering). For the initial buffering, the value of the property NXPropertyInitialBufferingDuration is used instead. If this is set to zero, NexPlayer will automatically select the recommended buffering time based on the content type (longer for HLS, shorter for other streaming types).
 
 - Type: unsigned int 
 - Default: 0 (automatic) 
 - Units: msec


### NXPropertyTimestampDifferenceVDispWait

The number of milliseconds (as a negative number) that video is allowed to run ahead of audio before the player waits for audio to catch up. For example, -20 means that if the current video time is more than 20msec ahead of the audio time, the current video frame will not be displayed until the audio catches up to the same time stamp. This is used to adjust video and audio synchronization.

- Type: int(should be negative) 
- Default: -20 (20msec) 
- Units: msec

### NXPropertyTimestampDifferenceVDispSkip

 The number of milliseconds that video is allowed to run behind audio before the system begins skipping frames to maintain synchronization. For example, 200 means that if the current video time is more than 200msec behind the audio time, the current video frame will be skipped. This is used to adjust video and audio synchronization.

 - Type: unsigned int 
 - Units: msec 
 - Default: 200 (0.2 sec)

### NXPropertyPrefetchBufferSize 

The size of the prefetch buffer to prepare for playback. If the buffer status satisfies either limit set by MAX_BUFFER_RATE or MAX_BUFFER_DURATION, the filling of the prefetch buffer will be stopped even though there may be spare space still available in the prefetch buffer.

If this value is set to 20MB, 1/4 (5MB) is allocated to the past (content already played) and 3/4(15MB) is allocated to the future (content yet to be played).
 
- Type: unsigned int 
- Units: bytes 
- Default: 50x1024x1024 (50MB)

> **Warning** Setting too large of a value here may lead to a large consumption of data packets under 3G or LTE network conditions.

 ### NXPropertyDataInactivityTimeout 
 
 Amount of time to wait for a server response before generating an error event. If there is no response from the server for longer than the amount of time specified here, an error event will be generated and playback will stop.

 Set this to zero to disable timeout (NexPlayer will wait indefinitely for a response).

- Type: unsigned int
- Default: 60,000 (60 seconds) 
- Units: msec

### NXPropertySocketConnectionTimeout

Amount of time to wait before timing out when establishing a connection to the server. If the connection to the server (the socket connection) cannot be established within the specified time, an error event will be generated and playback will not start.

Set this to zero to disable timeout (NexPlayer will wait indefinitely for a connection).

- Type: unsigned int 
- Default: 0 (infinite) 
- Units: msec (0 for infinite)

### NXPropertyRTPPortMin 

The minimum port number to be used when receiving RTP data. This sets the minimum possible port number to be used for the RTP port that is created when performing RTSP streaming over UDP.

- Default: 12000

### NXPropertyRTPPortMax

The maximum port number to be used when receiving RTP data. The maximum possible port number to be used for the RTP port that is created when performing RTSP streaming over UDP.

- Default: 30000

### NXPropertyNotOpenPlayAudio 

Prevents the audio track from playing back when set to TRUE (1).

- Type: boolean 
- Default: 0

### NXPropertyNotOpenPlayVideo

Prevents the video track from playing back when set to TRUE (1).

- Type: boolean 
- Default: 0

### NXPropertyNotOpenPlayText 

Prevents the text (subtitle) track from playing back when set to TRUE (1).

- Type: boolean 
- Default: 0

### NXPropertyProxyAdress

Sets the proxy address. :{String} 

- Default: null
 
### NXPropertyProxyPort

Sets the proxy port number. 

- Type: integer 
- Default: 0

### NXPropertyLogLevel 

Sets the log level. 
 
 Values:
 
 - NXPropertyLogLevel_Debug
 - NXPropertyLogLevel_RTP
 - NXPropertyLogLevel_RTCP
 - NXPropertyLogLevel_Frame
 
### NXPropertyAVInitOption 

Controls when video initialization happens. This can be any of the following values:
 
 - **NXPropertyAVInitOption_Partial (0x00000000)** If there is an audio track, wait for audio initialization to complete before initializing video.

 - **NXPropertyAVInitOption_All (0x00000001)** Begin video initialization as soon as there is any video data, without any relation to the audio track status.
 
- Default: NXPropertyAVInitOption_All

### NXPropertyPlayableForNotSupportAudioCodec

If set to 1, allows media playback even if the audio codec is not supported. The default behavior (if this is 0) is to return an error or generate an error event if the audio codec is not supported.

- Type: unsigned int 
- Default: 0

### NXPropertyPlayableForNotSupportVideoCodec

If set to 1, allows media playback even if the video codec is not supported. The default behavior (if this is 0) is to return an error or generate an error event if the audio codec is not supported.

- Type: unsigned int
- Default: 0

### NXPropertyUseEyePleaser

If more than this number of frames are skipped during rendering, the remaining frames up to the next keyframe are forcibly discarded and playback resumes from the next keyframe.

- Type: unsigned int 
- Default: 0xFFFFFFFF

### NXPropertyApplsLiveViewOption 

Live playback option. 

 - Type: unsigned int 
 - Default: NXPropertyHLSLiveViewRecent
 - Values:
 
  - **NXPropertyHLSLiveViewRecent (0x00000000)** Start playback from the most recently received me-
dia segment (.ts) files of the HLS live playlist. (The player will begin playback at a media segment
that was loaded four(4) segments earlier than the latest media segment file loaded.) For example,
if 5.ts is the latest media segment (.ts) file loaded in a sequence of five media segments, playback
will begin at the beginning of the second media segment, four segments (2.ts, 3.ts, 4.ts, and 5.ts)
preceding the latest media segment file loaded.
 
  - **NXPropertyHLSLiveViewRecentByTargetDuration (0x00000001)** Start playback from the most re-
cently received media segement (.ts) files, based on the value set for the EXT-X-TARGETDURATION
tag in the HLS live playlist. (The player will begin playback at the media segment that is immediately precedes the media segment that isthree times (x3) the target durationbefore the latest media segment file loaded.) As a concrete example, if the target duration is set to 12 seconds and the total duration of currently loaded media segments is 48 seconds, playback will begin at the media file that immediately precedes the media segment with the timestamp at 12 (48-36) seconds. If this example HLS playlist includes media segment files 1.ts (duration of 10 seconds), 2.ts (9 sec), 3.ts (11 sec), 4.ts (10 sec), and 5.ts (8 sec), then playback will begin at the first media segment, 1.ts, because it immediate precedes the 2.ts segment (where the timestamp at 12 seconds occurs).

  - **NXPropertyHLSLiveViewFirst (0x00000002)** Unconditionally start HLS playback from the first entry in the HLS playlist.

  - **NXPropertyLiveViewLowLatency (0x00000003)** Playback begins as close to the live edge as pos-
sible. The first file to load is the last segment in the playlist. (Do not use this option for normal
playback.)
 

### NXPropertyUserAgentString 

RTSP/HTTP User Agent value. 

-  Type: String

### NXPropertyFirstDisplayVideoFrame

Controls what is displayed while the player is waiting for audio data. If this is set to zero, the player will not display the first video frame until the audio is ready to play. Whatever was previously displayed will continue to be visible (typically a black frame) while it is waiting for audio data.

If this is set to 1, and video data becomes available prior to audio data, the first video frame will be displayed as a still image until audio data is available. 

Once audio has started, the behavior for both settings is the same; this only affects what is displayed while the player is waiting for audio data.

Under old versions of the SDK (prior to the addition of this property), the default behavior was as though this property were set to zero.

 - Type: boolean 
 - Default: 1
 - Values:
  - 0: Show nothing.
  - 1: Show first video frame.

NXPropertySourceOpenTimeOut 

Sets the amount of time to wait for an open request to complete.

This is used when NexPlayer tries to open new media. If there is no response from the server for longer
than the amount of time specified here, the open request will be stopped and `nexPlayer:completedAsyncCmdOpenWithResult:playbackType:` will be called with the result, namely the error code, NXErrorMediaOpenTimeout.

- Type: unsigned integer
- Unit: msec (1/1000 sec)
- Default: 300000 (300 seconds)

### NXPropertySocketOperationTimeout

The maximum waiting time till an HTTP request/response message
arrives to NexPlayer. If the reply does not arrive within this time after HTTP request message is sent to the streaming server, it will be regarded as an error.

- Type: unsigned int 
- Default: 30,000 (30 seconds
- Units: msec (0 for infinite)

### NXPropertyLowLatencyBufferOption 

Set a low latency buffer option. 

 - Type: unsigned int
 - Default: NXPropertyLowLaytencyBufferOptionNone
 - Values:

  - **NXPropertyLowLaytencyBufferOptionNone (0x00000000)** The latency value is set by INITIAL_B-
    UFFERING_DURATION and RE_BUFFERING_DURATION of NexProperty. It should set the reliable
    value depending on the bitrate of content and network environment.
  - **NXPropertyLowLaytencyBufferOptionAutoBuffer (0x00000001)** The latency value is calculated
    by the player at runtime. During playback, the latency may increase or decrease because it may
    change depending on the network environment.
  - **NXPropertyLowLaytencyBufferOptionConstBuffer (0x00000002)** The latency value is calculated
    by the player at the beginning of playback and maintains the value unchanged during playback.
    The latency increases more than when using Auto Buffer Mode, but the rebuffering will be reduced
    and try to maintain constant latency after rebuffering.
    

### NXPropertySeekRangeFromRAPoint 

Sets the range where NexPlayer will seek to a Random Access
point rather than the exact target position provided in the seekToAdjustedTime API.

> **Warning** This property is only valid when the second parameter, exact, in the seekToAdjustedTime API is true.

Setting this value is a kind of option for the seekToAdjustedTime API and can be used to minimize the time required to seek in content by taking advantage of Random Access points in the content. A Random Access point is a specific position that the parser is allowed to seek to directly.

This value sets the range where NexPlayer will seek from a Random Access point given by the parser to a target position that equalsmsec(milliseconds), the first parameter in the seek() API.
If the exact parameter, the second parameter in the seekToAdjustedTime API, istrueand the difference between a Random Access point and the target position is within this value, seekToAdjustedTime will find and seek to the exact target position. If the exact parameter is set to true and the difference between a Random Access point and the target position is beyond this range, seek will give up the accurate target point and will instead seek to and play from the Random Access point.

For example, if NexPlayer is seeking to 10000 ms exactly (exact = true) and there is a Random Access point at 7000 ms, if this property is set to less than 3000 ms, the player will ignore the exact target value and will instead play from 7000 ms. On the other hand, if this property is set to more than 3000 ms, then NexPlayer will seek exactly to 10000 ms and begin playback.

> **Warning** Please remember that in order to seek to a target position, audio or video frames have to be decoded. If too large of a value is set here, it may cause the seek process to consume an excessive amount of time especially in high resolution video content.

- Type: unsinged int 
- Units: msec (1/1000 sec) 
- Default: 10000 (10 seconds)

### NXPropertySetToSkipBFrame 

If set totrue, unconditionally skips all B-frames without decoding them.

- Type: boolean 
- Default: 0

**NXPropertyTooMuchLostFrameDuration** Maximum amount of silence to insert to make up for lost audio frames. Under normal operation, if audio frames are lost (if there is a time gap in received audio frames), silence will be inserted automatically to make up the gap.

However, if the number of audio frames lost represents a span of time larger than the value set for this property, it is assumed that there is a network problem or some other abnormal condition and silence is not inserted.

This prevents, for example, a corruption in the time stamp in an audio frame from causing the system
to insert an exceptionally long period of silence (which could possibly prevent further audio playback or cause other unusual behavior).

- Type: unsigned int 
- Units: msec (1/1000 sec) 
- Default: 20000 (20 seconds)

### NXPropertySupportLocal

If set to 1, enables local file playback support.

- Type: boolean
- Default: 1

### NXPropertySupportRTSP

If set to 1, enables RTSP streaming support.

- Type: boolean 
- Default: 0

> **Warning** This property is not supported in this API version.

### NXPropertySupportPD

If set to 1, enables progressive download support.

- Type: boolean
- Default: 1
 
### NXPropertySupportWMS 

If set to 1, enables Microsoft Windows Media Streaming support.

- Type: boolean
- Default: 0
 
### NXPropertySupportRDT 

If set to 1, enables Real Media Streaming support.

- Type: boolean
- Default: 0

### NXPropertySupportAppleHTTP

If set to 1, enables Apple HTTP Live Streaming (HLS) support.
 
- Type: boolean
- Default: 1
 
### NXPropertySupportABR 

If set to 1, enables HLS Adaptive Bit Rate (ABR) support.

- Type: boolean
- Default: 1

### NXPropertySupportDash 

If set to 1, enables DASH support.

- Type: boolean
- Default: 1
 
### NXPropertyMaxBW 

When streaming with multiple tracks, this sets the maximum allowable bandwidth. Any track over this bandwidth will not be selected for playback. Set to zero for no maximum.

- Type: unsigned int
- Units: bps (bits per second)
- Default: 0 (no maximum)
 
### NXPropertyH264Profile

Limits the H.264 profile that can be selected from an HLS playlist. Under normal operation, the track with the highest supported H.264 profile is selected from an HLS playlist. If this property is set, no track with a profile higher than this value will be selected. This should be set to zero for no limit.

- Type: unsigned integer
- Default: 0 (use any profile),

### NXPropertyIgnoreAudioLostFrame 

Suppresses automatic silence insertion for lost audio frames. During normal RTSP streaming operation, if an audio frame is lost (for example, due to a bad connection), the NexPlayer engine inserts a frame of silence into the audio stream to maintain synchronization. Enabling this setting suppresses that function. This may improve performance in some cases where the RTSP server doesn’t send an audio stream. This should be used with caution as it can cause the audio and video streams to lose synchronization.

- Default: 0 (disabled)
- Values:
 - 0: disabled
 - 1: enabled
 
### NXPropertyAlwaysBuffering 

Controls whether audio buffering is independent of the video state. In the case of an empty audio frame, if this property is enabled, buffering will always start regardless of the state of the video buffer.
 
- Default: 0 (disable)
- Values:
 - 0: disable
 - 1: enable

### NXPropertyIgnoreAVSync

Bypasses AV synchronization. When this property is enabled, AV synchronization is bypassed. As soon as data is received, it is immediately presented to the user.

> **Warning** This will almost certainly cause the audio and video to lose synchronization, and video playback speed will be unpredictable and vary depending on the speed of the connection and the speed by which the local system can decode frames. This may be useful for playing back a live video feed where frames are sent by the server at the correct intervals for playback.
 
- Default: 0 (disabled)
- Values:
 - 0: disabled
 - 1: enabled
  
### NXPropertySupportMSSmoothStreaming 

If set to 1, this enables MS Smooth Streaming support.

 - Type: boolean
 - Default: 1
 
### NXPropertyAVSyncOffset 

Adjusts A/V synchronization by ofsetting video relative to audio. Positive values cause the video to play faster than the audio, while negative values cause the audio to play faster than the video. Under normal operation, this can be set to zero, but in some cases where the synchronization is bad in the original content, this can be used to correct for the error.

While A/V synchronization is generally optimized internally by NexPlayer , there may occasionally be devices which need to be offset in order to improve overall A/V synchronization. For examples of how to set AV_SET_OFFSET based on the device in use, please see the Sample Application code as well as the introductory section A/V Synchronization section.

Appropriate values for any other problematic devices need to be determined experimentally by testing
manually.

- Type: integer
- Unit: msec (1/1000 sec)
- Range: -2000∼+2000
- Default: 0

### NXPropertyMaxWidth 

Limits the maximum width (in pixels) of the video tracks that can be selected during streaming play. This is used to prevent NexPlayer from attempting to play tracks that are encoded at too high a resolution for the device to handle effectively. NexPlayer will instead select a track with a lower resolution.

> **Note** On iOS ONLY, if this is zero (the default), NexPlayer will automatically set the value based on the device type and type of play (streaming or local). Note that when this is set to zero, getProperty: (NXPlayer) will also return zero. To get the actual value that is in effect during playback, call getEffectiveProperty: (NXPlayer) instead.

- Type: integer
- Units: pixels
- Default: NXPropertyMaxWidthMaxValue

### NXPropertyMaxHeight 

Limits the maximum height (in pixels) of the video tracks that can be selected during streaming play. This is used to prevent NexPlayer from attempting to play tracks that are encoded at too high a resolution for the device to handle effectively. NexPlayer will instead select a track with a lower resolution.

> **Note** On iOS ONLY , if this is zero (the default), NexPlayer will automatically set the value based on
the device type and type of play (streaming or local). Note that when this is set to zero, `getProperty: (NXPlayer)` will also return zero. To get the actual value that is in effect during playback, call `getEffectiveProperty: (NXPlayer)` instead.

- Type: integer
- Units: pixels
- Default: NXPropertyMaxHeightMaxValue

### NXPropertyPreferBandwidth 

Sets preferred bandwidth when switching tracks during streaming play. Under normal operation (when this property is zero), if the available network bandwidth drops below the minimum needed to play the current track without buffering, the player will immediately switch to a lower bandwidth track, if one is available, to minimize any time spent buffering.

If this property is set, the player will attempt to choose only tracks above the specified bandwidth, even if that causes some buffering. However, if the buffering becomes too severe or lasts for an extended time,
the player may eventually switch to a lower-bandwidth track anyway.
 
- Type: unsigned int
- Units: kbps (kilobits/sec)  
- Default: 0 (immediate switching)
- Values:
 - 0: No preferred bandwidth (immediate switching)
 - >0: Preferred bandwidth in kbps

See Also

 - NXPropertyPreferAV

### NXPropertyPreferAV 

Controls whether NexPlayer prefers tracks with both audio and video content. Under normal operation (when this property is set to 0), if the available network bandwidth drops below the minimum needed to play the current track without buffering, the player will immediately switch to a lower bandwidth track, if one is available, to minimize any time spent buffering.

If this property is set to 1, the player will attempt to choose only tracks that include both audio and video content, even if that causes some buffering. However, if the buffering becomes too severe or lasts for an extended time, the player may eventually switch to an audio-only track anyway.

- Type: unsigned int
- Default: 0 (immediate switching)
- Values:
 - 0: Normal behavior (immediate switching)
 - 1: Prefer tracks with both audio and video

 See Also
 - NXPropertyPreferBandwidth

### NXPropertyEnableTrackdown 

Allows NexPlayer to switch to a lower bandwidth track if the resolution or bitrate of the current track is too high for the device to play smoothly. Under normal operation, NexPlayer switches tracks based solely on current network conditions. When this property is enabled, NexPlayer will also switch to a lower bandwith track if too many frames are skipped during playback.

This is useful for content that is targeted for a variety of devices, some of which may not be powerful
enough to handle the higher quality streams.

The `NXPropertyTrackdownVideoRatio` property controls the threshold at which the track change will occur, if frames are being skipped.

Have to set it before start to play.
 
- Type: boolean
- Default: 0 
- Values:
 - 0: Normal behavior (switch based on network conditions only)
 - 1: Switch based on network conditions and device performance
 
### NXPropertyTrackdownVideoRatio 

Controls the ratio of skipped frames that will be tolerated before a track change is forced, if NXPropertyEnableTrackdown is enabled. The formula used to determined if a track switch is necessary is:

```
(^100) *(RenderedFrames / DecodedFrames) < TrackdownVideoRatio
```
 
In other words, if this property is set to 70, and NXPropertyEnableTrackdown is set to 1, NexPlayer will require that at least 70% of the decoded frames be displayed. If less than 70% can be displayed (greater than 30% skipped frames), then the next lower bandwidth track will be selected.

A performance-based track switch **permanently** limits the maximum bandwidth of tracks that are eligible for playback, until the content is closed. For this reason, setting this ratio higher than the default value of 70 is strongly discouraged. (This differs from the bandwidth-based algorithm, which continuously adapts to current network bandwidth).

- Type: integer
- Range: 0 to 100
- Default: 70, 

### NXPropertyHLSRunmode 

Controls the alogrithm used for bitrate switching when playing an HLS stream.

- Type: unsigned int
- Default: 0
- Values:
 - 0: Uses a more agressive algorithm: Up-switching happens sooner.
 - 1: Uses a more conservative algorithm: Up-switching happens only if a significant amount of extra bandwidth is available beyond that required to support the given bitrate. This is similar to the iPhone algorithm.

### NXPropertyHTTPCredentials 

Adds additional HTTP headers to use to supply credentials when a 401 response is received from the server. The string should be in the form of zero or more HTTP headers
(header name and value), and each header (including the last) should be terminated with a CRLF sequence, for example:
 
```id: test1\r\npw: 12345\r\n```


The particulars of the headers depend on the server and the authentication method being used.

- Type: String
 
### NXPropertyMinBufferRate 

The minumum ratio of prefetch buffer to resume filling buffer. If the ratio of filling buffer is less than this value, filling buffer will be resumed until buffer status meets the condition of `MAX_BUFFER_RATE` or `MAX_BUFFER_DURATION`. 
 
- Type: unsigned integer
- Unit: percent
- Default: 70 (70%)

### NXPropertyMaxBufferRate

The maximum ratio of prefetch buffer to pause filling buffer. If the ratio of filling buffer is more than this value, filling buffer will be paused until buffer status meets only the condition of `MIN_BUFFER_RATE`. 

- Type: unsigned integer
- Unit: percent
- Default: 90 (90%)

### NXPropertyMinBufferDuration 

The minumum duration of prefetch buffer to resume filling buffer. If the duration of filling buffer is less than this value, filling buffer will be resumed until buffer status meets the condition of `MAX_BUFFER_RATE` or `MAX_BUFFER_DURATION`. 

- Type: unsigned integer
- Unit: second
- Default: 30 (30s)

### NXPropertyMaxBufferDuration 

The minumum ratio of prefetch buffer to resume filling buffer. If filling buffer is less this value, filling buffer will be resumed until buffer status meets only the condition of `MIN_BUFFER_DURATION`. 
 
- Type: unsigned integer
- Unit: second
- Default: 60 (60s)

### NXPropertyUseSyncTask

Sets whether or not NexPlayer should use SyncTask feature. SyncTask may
improve decoding performance.

Note
> This property must be set before initializing NexPlayer or opening and playing content.

- Type: unsigned int
- Default: 0 
- Values :
 - 0: Do not use SyncTask.
 - 1: Use SyncTask.

### NXPropertySetCookie 

Controls whether the player honors cookies sent by the server.
 
- Type: unsigned int
- Default: 1
- Values:
 - 0: Ignore HTTP cookie headers sent by the server.
 - 1: Cookie headers received from a streaming server along with the initial manifest or playlist are included with further HTTP requests during the session.

### NXPropertySetLiveBackOff 

Sets the SmoothStreamingLiveBackOff property when playing Smooth
Streaming content. This property sets the duration of content (closest to live) that cannot yet be accessed or downloaded by the player. It is like setting how long to wait before asking for the latest fragment in a live presentation, and thus basically sets the played "live" point back from the actual live content available on the server.

The end-to-end latency of the player (what is being played "live" in the player compared to what is available live on the server) is at least the duration ofLiveBackOff added to the duration set for LivePlaybackOffset with NXPropertySetLiveBackOffset.

- Type: unsigned int
- Units:msec
- Default: 6000

### NXPropertySetLiveBackOffset 

Sets the Smooth Streaming LivePlaybackOffset property when playing Smooth Streaming content. This property sets the duration away from the live position to start playback when joining a live presentation when the LiveView option is set to "Recent", but excludes the `LiveBackOff` duration (set by NXPropertySetLiveBackOff).

As a result, live content will be played behind the actual live position by a duration determined by BOTH `LiveBackOff` and the value for `LivePlaybackOffset` set here.

Setting this property enables faster startup because it allows a buffer to be built up as fast as bandwidth will support (potentially faster than real time), which creates a buffer against network jitter. It does however also increase end-to-end latency, which means what is played "live" in the player is farther behind the actual live playing point of the content.

- Type: unsigned int 
- Units: msec
- Default: 7000

### NXPropertyStartWithAV 

Starts video together with or separately from audio. This property starts to play audio and video together when starting, if the video timestamp is slower than audio’s timestamp.

If it is 1, it forces the video and audio to start at the same time. If it is 0, it lets the video and audio to start separately.

- Type: boolean
- Default: 0 (video and audio will start separately, based on the timestamps)

### NXPropertyIgnoreAbnormalSegmentTimestamp 

Ignores abnormal segment timestamps. If it is 1 or enabled, NexPlayer will ignore abnormal segment timestamps. If it is 0 or disabled, NexPlayer will not ignore any abnormal segment timestamps.

 - Type: boolean
 
> **Warning** This property is not supported in this API version.
 
### NXPropertyEnableModifyHTTPRequest 

Allows the application to modify the content of an HTTP Request that NexPlayer is about to send to a remote HTTP server. When this property is set equal to 1 (enabled), NexPlayer invokes `nexPlayer:onModifyHttpRequest:` with the HTTP Request as an argument. The application can return the modified version of the HTTP Request that will actually be sent.

- Values:
 - 0 : Disabled. Don’t deliver any HTTP Request.
 - 1 : Enabled. Deliver HTTP Request to modify on the application side.

> **See Also** `NXPlayerDelegate.h::NXPlayerDelegate:nexPlayer:onModifyHTTPRequest:` for more information.

### NXPropertyOpenMediaFileFromSpecifiedTS 

Allows NexPlayer to begin downloading content media files from a specified time stamp in the content.

> **Warning** This property is currently only supported for VOD in HTTP Live Streaming (HLS).
 
NexPlayer allows users to start playback in the middle of a content file with the start api, but typically, before playback can begin, the player still opens content from the first media file available and then has to receive all of the media files between the first file and the point where the user would like to start playback.

When playback is to start in the middle of content, this property allows the player to skip receiving the unneeded earlier media files based on the time stamp value set by the application, and instead begin downloading media files from a position closer to the specified time stamp instead.

This property can thus reduce the time needed to open and start playing a media file in the middle of VOD content.

> **Note** This property must be set before NexPlayer.open is called.

- Type: unsigned integer
- Unit: msec (1/1000 s)
- Default: 0xFFFFFFFF

### NXPropertyRequestRadioMetadataMode 

Allows NexPlayer to add an explicit request for metadata in internet radio stream content.

> **Warning** This is currently only supported in SHOUTcast and IceCast HLS content.

If an explicit request for metadata is not made, a server may or may not send internet radio stream
metadata even if it exists.

Setting this property to 1 means an explicit request for internet radio stream metadata will be included with every content request sent to a server. If this property is set to 2, NexPlayer will only add an explicit request for metadata after initially receiving content and identifying it as a SHOUTcast or Icecast stream.

Values:

 - **0 : DEFAULT :** Default mode. Does not add an additional explicit request for internet radio stream metadata.
 - **1 : INSERT_HEADER :** Always inserts a header with a request for internet radio stream metadata
    (with every content request).
 - **2 : INSERT_HEADER_AFTER_TRIAL :** If NexPlayer determines content is a SHOUTcast or Ice-
    cast stream, a header with an explicit request for metadata will be added to subsequent server
    requests.
    
### NXPropertyMinBW 

When using HLS ABR, this is the minimum allowable bandwidth. Any track with a bandwidth smaller than this value will not be played back.

> **Note** To dynamically set a minimum bandwidth allowed while content is playing, please call the method `NexABRController::changeMinBandWidth()` instead. This property should be set to zero for no minimum.
 
- Type: unsigned integer
- Unit: bps (bits per second)
- Default: 0 (no minimum)

### NXPropertyEnableCEA708 

Enables rendering and display of CEA 708 closed captions in content when available. While CEA 608 closed captions are always enabled, it is necessary to set this property to 1 in order for NexPlayer to support CEA 708 closed captions.
 
In the case where content contains both CEA 608 and CEA 708 closed captions and this property enables

CEA 708 closed captions, the application will have to handle choosing which captions to render and
display to the user.

- Type: boolean
- Default: 0
- Values:
 - **0:** CEA 708 closed captions disabled.
 - **1:** CEA 708 closed captions enabled.

### NXPropertyEnableWebVTT 

Sets whether or not to display WebVTT text tracks automatically when they are included in content. In the case when both CEA 708 closed captions and WebVTT text tracks are included in content, this property can be used to set whether to display the WebVTT text tracks or the closed captions automatically.

By default, this property is set to 1 to enable WebVTT text tracks automatically if they exist in content (as was the behavior of NexPlayer previously). If for some reason it would be preferable that CEA 708 closed captions be displayed instead of the WebVTT text tracks, this property should be set to 0 with by with setProperty: 
 
```
mNexPlayer.setProperty(NexProperty.ENABLE_WEBVTT, 0);
```

This property should only be called once, immediately after calling `init` but before calling `open`.

- Type: boolean
- Default: 1 (WebVTT text tracks enabled)
- Values:
 - 0 : WebVTT text tracks ignored; CEA 708 closed captions enabled
 - 1 : WebVTT text tracks enabled; CEA 708 closed captions ignored

### NXPropertyPartialPrefetch 

Sets whether or not to begin playback after a part of the TS file is downloaded.

By default, this property is set to 0 to download the first TS file completely to play content.

- Type: boolean
- Default: 0, 
- Values:
 - 0 : Partial prefetch ignored; playback will begin after downloading the first TS file completely.
 - 1 : Partial prefetch enabled; playback will begin after a part of the TS file is downloaded.

### NXPropertyTimedID3MetaKey 

Allows custom ID3 tags added to timed metadata in content to be recognized and handled by NexPlayer. When customized ID3 tags with additional information have been added to the timed metadata in content, this property can be used to help NexPlayer recognize and pass those ID3 tags and the extra information they contain to an application.

This property must be setbeforeopenis called.

- Type: String
- Values: a list of the customized ID3 tag names separated by semicolons (;)
- Default: nothing

### NXPropertyEnableID3TTML 

Sets whether or not to display TTML text tracks in ID3 tag automatically when they are included in content. In the case when both CEA closed captions and TTML text tracks in ID3 tag are included in content, this property can be used to set whether to display the TTML text tracks in ID3 tag or the closed captions automatically.

By default, this property is set to 0 to disable TTML text tracks in ID3 tag automatically if they exist in content (as was the behavior of NexPlayer previously). If for some reason it would be preferable that

TTML captions in ID3 tag to be displayed instead of the CEA closed captions text tracks, this property should be set to 1 usingsetProperty:This property should only be called once, immediately after calling `init` but before calling `open`.

- Type: boolean
- Default: 0
- Values:
 - 0 : TTML text tracks in ID3 tag ignored; CEA closed captions enabled
 - 1 : TTML text tracks in ID3 tag enabled; CEA closed captions ignored
 
### NXPropertyPreferLanguage 

Sets the language of both audio and text played in multi-stream content. It can be used to set the preferred language of audio and text streams to be displayed in content, before NexPlayer begins playing content.

This property should be set by calling setProperty:toValue: (NXPlayer) after init and before open is
called, as demonstrated in the following sample code:

```
[nxPlayer setProperty:NXPropertyPreferLanguage toValue:"eng"];
```

 - Type: String
 - Default: null
 - Values: Accurate language labels as Strings. For example, "eng" for English.

> **Note** Accurate language labels (not the name of a text stream) should be used for the values of this property.

### NXPropertyPreferLanguageAudio 

Sets the language to use for audio in multi-stream content, before content is played. This property can be used to set the preferred language of audio streams to be used in content, before NexPlayer begins playing content.

This property should be set by callingsetProperty:after init and before open: (NXPlayer)
is called.

To set the preferred language for both audio and text streams to the same language, use the `NXPropertyPreferLanguage` instead.

 - Type: String
 - Default: null
 - Values: Accurate language labels as Strings. For example, "eng" for English.

> **Warning** To change any media streamwhilecontent is playing, the method `setVideoStream:audioStream:textStream:trackAttributes:` should be called instead.

> **Note** Accurate language labels (not the name of a text stream) should be used for the values of this property.


### NXPropertyPreferLanguageText 

Sets the language to use for text in multi-stream content, before content is played.

This property can be used to set the preferred language of text streams to be displayed in content,before NexPlayer begins playing content.
 
This property should be set by calling `setProperty:` after `init` and before `open`
is called.

 - Type: String
 - Default: null
 - Values: Accurate language labels asStrings. For example, "eng" for English.

> **Warning** To change any media streamwhilecontent is playing, the method `setVideoStream:audioStream:textStream:trackAttributes:` should be called instead. To set the preferred language for both audio and text streams to the same language, use the `NXPropertyPreferLanguage` instead.


> **Note** Accurate language labels (not the name of a text stream) should be used for the values of this property.

### NXPropertyWebVTTWaitOpen 

Avoids waiting for the first WebVTT segment to download when starting to play content. This property can be used when playing WebVTT content. By default, NexPlayer waits until the first WebVTT segment is downloaded before content begins to play so that no caption text will be missed.

However, if this property is disabled (set to 0), the player will start playing content as soon as possible (instead of waiting until the first WebVTT segment is fully downloaded). This may be preferred if content should start playing as quickly as possible (although initial WebVTT text may be missed).

This property should be called once, immediately after callinginitbut before callingopen.

- Type: boolean
- Default: 1
- Values:
 - **0:** Content starts playing before first WebVTT segment is downloaded.
 - **1:** Content starts playing after first WebVTT segment is downloaded.

### NXPropertyStartNearestBW 

Sets a target bandwidth (before playing HLS content) when selecting which track to play as playback starts. While NexPlayer automatically chooses an ideal track to play based on several factors including device capability and network conditions, there may be situations in which starting playback from a track with a bandwidth near a particular bandwidth is desired.

When this property is set, NexPlayer selects and starts playing the track in content that has the bandwidth closest to the set bandwidth value, initially ignoring other factors.

Note that as playback continues, the track played may change as NexPlayer judges all factors that
influence streaming playback and chooses the best option.

This property should be called after init but before calling open.

- Type: int
- Unit: bps (bits per second)
- Default: null
- Values: The target bandwidth value, in bits per second (bps). Note that if `NXPropertyStartNearestBW` is set to 0, NexPlayer will play normally, as if this property has not been set.

### NXPropertyAudioOnlyTrack 

Sets whether to enable or disable the Audio Only track in HLS content. This property should be called after init but before calling open.

- Type: int
- Default: 1
- Values:
 - **0:** Audio Only track disabled.
 - **1:** Audio Only track enabled.

### NXPropertyContinueDownloadAtPause 

Sets whether or not to continue downloading data in pause state when playing content. When this property is set, content data will continue to be downloaded even when NexPlayer is paused.

> This property should be called after init and before calling open.

- Type: NSUInteger
- Default: 0
- Values:
 - **0:** Stop downloading in pause state.
 - **1:** Continue downloading in pause state.

### NXPropertySegmentTSReliable 

Sets whether or not to trust a content segment’s timestamp when playback starts. 

> This property should be called after init but before calling open.

- Type: int
- Default: 1
- Values:
 - **0:** Adjust the timestamp during playback.
 - **1:** Trust the timestamp during playback.

### NXPropertySuggestedPresentationDelayTime 

For DASH, use suggestedPresentationDelay to synchronize end users. For HLS, use the #EXT-X-PROGRAM-DATE-TIME tag to sync end users. 

> This property should be called after init but before calling open.

- Type: unsigned integer
- Unit: msec (1/1000 sec)
- Default: 2000 (2 sec)


### NXPropertyEnableSpdSyncToGlobalTime 

Enables synchronization to UTC time(SPD).  

> This property should be called after init but before calling open.

- Type: int
- Default: 0
- Values:
 - **0:** SPD disabled.
 - **1:** SPD enabled.

### NXPropertySpdSyncDiffTime 

If the current playback is not more synchronized than this value, the player will speed up playback and make sync. 

> This property should be called after init but before calling open.

- Type: unsigned integer
- Unit: msec (1/1000 sec)
- Default: 300 (300 msec)

### NXPropertySpdTooMuchDiffTime 

If playback is out of sync than this value, the player will jump to synchronize the video rather than make it by speeding up.

> This property should be called after init but before calling open.

- Type: unsigned integer
- Unit: msec (1/1000 sec)
- Default: 5000 (5 seconds)

### NXPropertySetHWdecoderPixelFormat 

Sets iOS HW decoder pixel foramt of output property (kCVPixel-
BufferPixelFormatTypeKey). This property is to set a pixel format for decoded video format. Have to set it before start to play.

> **Warning** Don’t use general play if you use this property for general play. If you don’t use it properly, the video will not display normally.

- Type: int
- Default: 0 (kCVPixelFormatType_420YpCbCr8BiPlanarVideoRange)
- Values:
 - **0:** If you want to develop iOS application, you should use this. (kCVPixelFormatType_420YpCbCr8BiPlanarVideoRange)
 - **1:** If you want to develop Unity application, you should use this. kCVPixelFormatType_32BGRA

### NXPropertySetMaxCaptionLength 

Set it to extend max caption length.

> This property should be called after init but before calling open.

- Type: int
- Default: 8192

### NXPropertyRFCBufferCount

Controls the maximum number of pages the player can allocate for the remote file cache. The remote file cache stores data that has been read from disk or received over the network (this includes local, streaming, and progressive content). In general, this value should not be changed, as an incorrect setting can adversely affect performance, particularly when seeking. 

In order to play multiplexed content, at least one audio chunk and one video chunk must fit inside a single RFC buffer page. For certain formats (PIFF, for example) at very high bitrates, the chunks may be too big to fit in a single page, in which case the RFC buffer page size will need to be increased. 
If the system has limited memory resources, it may be necessary to decrease the buffer count when increasing the page size. 

Increasing the page size can increase seek times, especially for data received over the network (progressive download and streaming cases), so this value should not be changed unless there are issues playing specific content that cannot be solved in another way.

- Type: unsigned int 
- Units: number of buffers 
- Default: 20

### NXPropertyRFCBufferPageSize 

Controls the size of each page in the remote file cache. Use caution when adjusting this value. Improper settings may adversely affect performance, or may cause some content to fail to play.

See NXPropertyRFCBufferCount for a detailed description.

- Type: unsigned int
- Units: kilobytes
- Default: 512

### NXPropertyCEA608TextMode 

This property sets whether CEA 608 closed captions should be rendered in caption mode or text mode. 

- Type: boolean
- Default: 0
- Values:
 - **0:** Render CEA 608 closed captions in caption mode.
 - **1:** Render CEA 608 closed captions in text mode.

### Timed Metadata Keys

**Variables**

- static NSString ∗kNXTimedMetaKeySessionInfo = @"@"SessionInfo"

 ID3 tags which are stored in the NS Dictionary and can be retrieved using their c\ keys. This key gets the content session information if available.

- static NSString ∗kNXTimedMetaKeyTitle = @"@"Title"

 This key gets the content title if available.

- static NSString ∗kNXTimedMetaKeyArtist = @"@"Artist"

 This key gets the content artist, if available.

- static NSString ∗kNXTimedMetaKeyAlbum = @"@"Album"

 This key gets content album information, if available.

- static NSString ∗kNXTimedMetaKeyGenre = @"@"Genre"

 This key gets the content genre if available.

- static NSString ∗kNXTimedMetaKeyYear = @"@"Year"

 This key gets the year of content, if available.

- static NSString ∗kNXTimedMetaKeyLyrics = @"@"Lyrics"

 This key gets content lyrics, if available.

- static NSString ∗kNXTimedMetaKeyTrackNum = @"@"TrackNumber"

 This key gets the track number, if available.

- static NSString ∗kNXTimedMetaKeyImage = @"@"Picture"

 This key gets the image associated with the content, if available.

- static NSString ∗kNXTimedMetaKeyComment = @"@"Comment"

 This key gets a comment associated with the content, if available.

- static NSString ∗kNXTimedMetaKeyText = @"@"Text"

 This key gets text associated with the content, if available.

- static NSString ∗kNXTimedMetaKeyPrivateFrame = @"@"PrivateFrame"

 This key gets the data from extra tags in metadata if available.

- static NSString ∗kNXTimedMetaKeyExtraData = @"@"extraTagData"

 This key gets the data from extra tags in metadata if available.


### Types

### Classes 

- struct NexAudioPostProcessingParams
    
 The characteristics of audio samples to be provided by NexAudioPostProcessingAdapter to the audio post-processor, which implements the NexAudioPostProcessingAdapterDelegate protocol.

- struct NexVideoRawBits
 
 This data structure contains information of YUV420 planar video planes (three planes including Y, U and V), pixel resolution and line stride.

- struct NEXPLAYERRemoteFileIOInterface_
    
 A structure holding function pointers to all of the functions that comprise the Remote File I/O interface.

- struct NXCEA608CellInfo
 
 CEA-608 caption cell information.

- struct NXSARInfo
 
 SAR (Sample Aspect Ratio) of H.264 contents.

### Macros

\#define NXDuration_Unknown (0xFFFFFFFFU)

For live streams where duration of content cannot be determined, this type can be passed in place ofNXDuration.

### Typedefs

- typedef struct NexAudioPostProcessingParams NexAudioPostProcessingParams

 The characteristics of audio samples to be provided by NexAudioPostProcessingAdapter to the audio post-processor, which implements the NexAudioPostProcessingAdapterDelegate protocol.

- typedef void(∧UpdatedTextureBlock )(NexVideoTexture∗texture)
 
 This method is called when a new video texture is available to be rendered from the caller.

- typedef struct NexVideoRawBits NexVideoRawBits
 
 This data structure contains information of YUV420 planar video planes (three planes including Y, U and V), pixel resolution and line stride.

- typedef enum NXDRMDataType_ NXDRMDataType
 
 Type of data being passed for DRM descrambling.

- typedef void∗NEXFileHandle
 
 File handle used in Remote File I/O callbacks.

- typedef enum _NEXFileMode NEXFileMode
 
 File open mode.

- typedef enum _NEXFileSeekOrigin NEXFileSeekOrigin
 
 Origin for Remove File I/O callback seek operations.

- typedef struct NEXPLAYERRemoteFileIOInterface_ NEXPLAYERRemoteFileIOInterface
 
 A structure holding function pointers to all of the functions that comprise the Remote File I/O interface.

- typedef NSUInteger NXDuration
 
 Represents the duration of the content as a span of time in milliseconds.

- typedef void∗NXFileHandle

 Opaque file handle.

- typedef enum NXFileMode_ NXFileMode
 
 Mode for opening a file.

- typedef enum NXFileSeekOrigin_ NXFileSeekOrigin
 
 Origin when seeking within a file.

- typedef enum NXDRMType_ NXDRMType
 
 DRM types.

- typedef enum NXKeepAliveSendMode_ NXKeepAliveSendMode

 Keep alive send modes.

- typedef enum NXFileFormat_ NXFileFormat

 File formats.

- typedef enum NXRTSPOptions_ NXRTSPOptions
 
 RTSP options.

### Enumerations

### NXBufferInfoMediaType

This enumeration defines the possible stream type for NXBufferInfoMediaType.
 
```
enum NXBufferInfoMediaType { 
	NXBufferInfoMediaTypeVideo = 0x0, 
	NXBufferInfoMediaTypeAudio = 0x2,
	NXBufferInfoMediaTypeText = 0x3 
}
```


### NXBufferingState

This enumeration defines the possible buffering state for NXBufferingState.


```
enum NXBufferingState { 
	NXBufferingStatePaused** = 0x0, 
	NXBufferingStateResume** = 0x1 
}
```

### NXDeviceInfoConnectionType

NexPlayer connection types.

```
enum NXDeviceInfoConnectionType { 
	NXDeviceInfoConnectionTypeUnknown, 
	NXDeviceInfoConnectionTypeNone, 
	NXDeviceInfoConnectionTypeWWAN, 
	NXDeviceInfoConnectionTypeWiFi 
}
```

### NXDRMDataType_    

Type of data being passed for DRM descrambling.       

```
enum NXDRMDataType_ { 
	NXDRMDataTypeVideo = 0, 
	NXDRMDataTypeAudio = 1 
}
```
    
### NXError 

NexPlayer error codes.

```
enum NXError {
    NXErrorNone = 0x00000000, 
    NXErrorHasNoEffect, 
    NXErrorInvalidParameter, 
    NXErrorInvalidInfo,
    NXErrorInvalidState, 
    NXErrorMemoryOperation, 
    NXErrorFileOperation, 
    NXErrorFileInvalidSyntax,
    NXErrorNotSupportPVXFile
    NXErrorNotSupportAudioCodec, 
    NXErrorNotSupportVideoCodec,
    NXErrorNotSupportVideoResolution,
    NXErrorNotSupportMedia, 
    NXErrorInvalidCodec, 
    NXErrorCodec, 
    NXErrorPartialSuccess,
    NXErrorAlreadyCreateAsyncProc, 
    NXErrorInvalidAsyncCmd, 
    NXErrorAsyncOthercmdPrcessing, 
    NXErrorRTCPByeReceived,
    NXErrorUserTerminated, 
    NXErrorSystemFail, 
    NXErrorNoDataInBuffer, 
    NXErrorUnknown,
    NXErrorNotSupportToSeek, 
    NXErrorNotSupportAVCodec, 
    NXErrorMediaOpenTimeout = 0x00000023,
    NXErrorDataInactivityTimeout = 0x00000026,
    NXErrorNetworkProtocol = 0x00000029, 
    NXErrorMediaNotFound = 0x0000002A, 
    NXErrorDrmDecryptFailed = 0x00000022, 
    NXErrorDrmInitFailed = 0x0000002C,
    NXErrorNotSupportFeature = 0x00000FFF, 
    NXErrorProtocolInvalidURL = 0x00010001, 
    NXErrorProtocolInvalidResponse = 0x00010002, 
    NXErrorProtocolContentInfoParsingFail = 0x00010003,
    NXErrorProtocolNoProtocol = 0x00010004, 
    NXErrorProtocolNoMedia = 0x00010005, 
    NXErrorProtocolNetOpenFail = 0x00010006, 
    NXErrorProtocolNetConnectFail = 0x00010007,
    NXErrorProtocolNetBindFail = 0x00010008, 
    NXErrorProtocolNetDNSFail = 0x00010009, 
    NXErrorProtocolNetConnectionClosed = 0x0001000A, 
    NXErrorProtocolNetSendFail = 0x0001000B,
    NXErrorProtocolNetRecvFail = 0x0001000C, 
    NXErrorProtocolNetRequestTimeout = 0x0001000D, 
    NXErrorProtocolNotSupportAESEncryption = 0x0001000E, 
    NXErrorProtocolNetSSLCertFail = 0x0001000F,
    NXErrorProtocolDisabledMedia = 0x00010010, 
    NXErrorHTTPStatusCode = 0x00020000, 
    NXErrorInternalBase = 0x00030000, 
    NXErrorExternalBase = 0x00040000,
    NXErrorExternalDescrambleTimeout = 0x01000001, 
    NXErrorDownloaderInvalidParameter = 0x00050000,
    NXErrorDownloaderInvalidState, 
    NXErrorDownloaderMemoryOperation,
    NXErrorDownloaderFileOperation, 
    NXErrorDownloaderConnectionFail, 
    NXErrorDownloaderConnectionClosed, 
    NXErrorDownloaderPVXdownFail,
    NXErrorDownloaderPVXparsingFail, 
    NXErrorDownloaderNotMultiparts, 
    NXErrorDownloaderHTTPparsingFail, 
    NXErrorTimeshiftBase = 0x00060000,
    NXErrorTimeshiftWrite = 0x00060001, 
    NXErrorTimeshiftRead = 0x00060002, 
    NXErrorTimeshiftFindIframe = 0x00060003, 
    NXErrorDivXDRMBase = 0x00070000,
    NXErrorDivXDRMNotAuthorized, 
    NXErrorDivXDRMNotRegistered, 
    NXErrorDivXDRMRentalExpired,
    NXErrorDivXDRMGeneralError,
    NXErrorDivXDRMNeverRegistered, 
    NXErrorThumbnailBase = 0x00080000, 
    NXErrorThumbnailCreateFail, 
    NXErrorThumbnailProcessFail,
    NXErrorThumbnailDRMContents, 
    NXErrorRecordBase = 0x00090000, 
    NXErrorAddframeSizeFull, 
    NXErrorAddframeTimeFull,
    NXErrorAddframeMemFull, 
    NXErrorAddframeError, 
    NXErrorAPIBase = 0x00900000, 
    NXErrorAPICannotCreateDownloader,
    NXErrorAPIInvalidInfo, 
    NXErrorCommandResult, 
    NXErrorCreateRFC, 
    NXErrorRTSPCommandTimeout,
    NXErrorPauseSupervisionTimeout, 
    NXErrorNoValidFrameFound, 
    NXErrorOperationNotValidInCurrentState, 
    NXErrorDownloadFailure,
    NXErrorUnsupportedEncryption, 
    NXErrorNotSupportedContentInAirPlay, 
    NXErrorInvalidSDKBase =0x80000000, 
    NXErrorInvalidSDK = 0x8000000D,
    NXErrorNotActivatedAppID = 0x80000012, 
    NXErrorTimeLocked = 0x800000A0, 
    NXErrorInvalidLicense = 0x800000C0 
}

```

### NexHLSTSDescrambleResult

This enumeration defines the possible return values from a NXHLSTSDescrambler method.

```
enum NexHLSTSDescrambleResult { 
	NexHLSTSDescrambleResultSucceed = 0, 
	NexHLSTSDescrambleResultNeedMoreBuffer = 1, 
	NexHLSTSDescrambleResultError
}
```

### NXHttpStateInfoFileType

An enumeration of the possible types of files being handled by NexPlayer during playback.

```       
enum NXHttpStateInfoFileType{
	NXHttpStateInfoFileTypeUnknown = 0, 
	NXHttpStateInfoFileTypeMPD = 1, 
	NXHttpStateInfoFileTypeSegment = 2, 
	NXHttpStateInfoFileTypeInitialSegment = 3,
	NXHttpStateInfoFileTypeKey = 4, 
	NXHttpStateInfoFileTypeSegmentIndex = 5 
}
```      

### _NEXFileMode

File open mode.

```
enum _NEXFileMode { 
	NEX_FILE_READ = 1, 
	NEX_FILE_WRITE = 2, 
	NEX_FILE_READWRITE = 3, 
	NEX_FILE_CREATE = 4 
}
```

### _NEXFileSeekOrigin

Origin for Remove File I/O callback seek operations.

```
enum _NEXFileSeekOrigin { 
	NEX_SEEK_BEGIN = 0, 
	NEX_SEEK_CUR = 1, 
	NEX_SEEK_END = 2 
}
```
    
### NXOpenMode    

Open modes
    
```
enum NXOpenMode {
	NXOpenModeAuto = 0, 
	NXOpenModeLocal = 1, 
	NXOpenModeStreaming = 2, 
	NXOpenModeLocalBundle = 3,
    NXOpenModeLocalDocs = 4, 
    NXOpenModeStoreStream = 5 
}
```

### NXOnOffDefault 

```   
enum NXOnOffDefault { 
	NXDefault = 0, 
	NXOff = 1, 
	NXOn = 2 
}
```

### NXPlaybackType

Playback types.

```
enum NXPlaybackType { 
	NXPlaybackTypeLocal = 0, 
	NXPlaybackTypeStreaming = 1 
}
```

### NXTransportType

Transport layers (TCP and UDP) for RTP and RTCP packets.


```
enum NXTransportType { 
	NXTransportTypeTCP = 0, 
	NXTransportTypeUDP = 1 
}
```

### NXPlayerState

Possible states of the player (paused, stopped, etc.).


```
enum NXPlayerState {
    NXPlayerStateNone = 0, 
    NXPlayerStateClose = 1, 
    NXPlayerStateStop = 2, 
    NXPlayerStatePlay = 3,
    NXPlayerStatePause = 4 
}
```


### NXRTSPMethod

RTSP method identifiers.

```
enum NXRTSPMethod {
    NXRTSPMethodNone = 0x00000000, 
    NXRTSPMethodDescribe = 0x00000001, 
    NXRTSPMethodSetup = 0x00000002, 
    NXRTSPMethodPlay = 0x00000004,
    NXRTSPMethodPause = 0x00000008, 
    NXRTSPMethodTeardown = 0x00000010, 
    NXRTSPMethodOptions = 0x00000020, 
    NXRTSPMethodRedirect = 0x00000040,
    NXRTSPMethodSetParameter = 0x00000080, 
    NXRTSPMethodGetParameter = 0x00000100, 
    NXRTSPMethodAnnounce = 0x00000200, 
    NXRTSPMethodPlaylist = 0x00000400,
    NXRTSPMethodAll = 0x0000FFFF 
}
```


### NXCodecID

Codec type identifiers

```
enum NXCodecID {
	NXCodecID_UNKNOWN = 0x00000000, 
	NXCodecID_MPEG4V = 0x10020100, 
	NXCodecID_HEVC = 0x10010400, 
	NXCodecID_H264 = 0x10010300,
	NXCodecID_H263 = 0x10010200, 
	NXCodecID_WMV = 0x10060000, 
	NXCodecID_WMV1 = 0x10060100,
	NXCodecID_WMV2 = 0x10060200,
	NXCodecID_WMV3 = 0x10060300, 
	NXCodecID_DIVX = 0x10040000, 
	NXCodecID_WVC1 = 0x10060400,
	NXCodecID_AAC = 0x20020000,
	NXCodecID_AACPlus = 0x20020100, 
	NXCodecID_WMA = 0x20070000, 
	NXCodecID_WMA1 = 0x20070100, 
	NXCodecID_WMA2 = 0x20070200,
	NXCodecID_MP3 = 0x20010200, 
	NXCodecID_AC3 = 0x20030000, 
	NXCodecID_AC4 = 0x20030200, 
	NXCodecID_EAC3 = 0x20030100,
	NXCodecID_DTS = 0x20040000, 
	NXCodecID_EXTERNAL_SMI = 0x30030100, 
	NXCodecID_EXTERNAL-SRT = 0x30040100, 
	NXCodecID_3GPP_TIMEDTEXT = 0x30010100,
	NXCodecID_TEXT_WEBVTT = 0x300C0100, 
	NXCodecID_TEXT_CC_CEA = 0x300D0100, 
	NXCodecID_TEXT_TTML = 0x300B0100, 
	NXCodecID_VOB_SUB = 0x30060100,
	NXCodecID_MICRODVD_SUB = 0x30070100, 
	NXCodecID_DIVX_XSUB = 0x300E0000, 
	NXCodecID_DIVX_XSUBPLUS = 0x300E0100, 
	NXCodecID_AMR = 0x20180000 
}
```

### NXCEA608Color

CEA 608 Colors

```
enum NXCEA608Color {
    NXCEA608Color_White = 0, 
    NXCEA608Color_White_Semitrans = 1, 
    NXCEA608Color_Green = 2, 
    NXCEA608Color_Green_Semitrans = 3,
    NXCEA608Color_Blue = 4, 
    NXCEA608Color_Blue_Semitrans = 5, 
    NXCEA608Color_Cyan = 6, 
    NXCEA608Color_Cyan_Semitrans = 7,
    NXCEA608Color_Red = 8, 
    NXCEA608Color_Red_Semitrans = 9, 
    NXCEA608Color_Yellow = 10, 
    NXCEA608Color_Yellow_Semitrans = 11,
    NXCEA608Color_Magenta = 12, 
    NXCEA608Color_Magenta_Semitrans = 13, 
    NXCEA608Color_Black = 14,
    NXCEA608Color_Black_Semitrans = 15,
    NXCEA608Color_Transparent = 16, 
    NXCEA608Color_Default = 17, 
    NXCEA608Color_Last = NXCEA608Color_Default 
}
```

### NXCEA608Charset

CEA 608 Character Set IDs.

```
- enum NXCEA608Charset {
	NXCEA608Charset_Unicode = 0, 
	NXCEA608Charset_Private1 = 1, 
	NXCEA608Charset_Private2 = 2, 
	NXCEA608Charset_KSC_5601_1987 = 3,
	NXCEA608Charset_GB_2312_80 = 4 
}
```

### NXMediaType

Media types

```
enum NXMediaType {
	NXMediaTypeUnknown = 0, 
	NXMediaTypeAudio = 1, 
	NXMediaTypeVideo = 2, 
	NXMediaTypeText = 3,
	NXMediaTypeAV = 4 
}
```

### NXCEA608Channel

CEA 608 Channel IDs.

```
enum NXCEA608Channel {
	NXCEA608Channel_None = 0, 
	NXCEA608Channel_Ch1 = 1, 
	NXCEA608Channel_Ch2 = 2, 
	NXCEA608Channel_Ch3 = 3,
	NXCEA608Channel_Ch4 = 4 
}
```

### NXDebugMsgCat

Debugging Messages to include.

```
enum NXDebugMsgCat {
	NXDebugMsgCat_RTSP = 0x00, 
	NXDebugMsgCat_RTP_RECV = 0x01, 
	NXDebugMsgCat_RTP_RECV_END = 0x02, 
	NXDebugMsgCat_RTCP_RR_SEND = 0x03,
	NXDebugMsgCat_RTCP_BYE_RECV = 0x04, 
	NXDebugMsgCat_CONTENT_INFO = 0x05, 
	NXDebugMsgCat_HTTP_RESPONSE = 0x06, 
	NXDebugMsgCat_DOWNLOADED_BUFF = 0x07,
	NXDebugMsgCat_DECODING = 0x08, 
	NXDebugMsgCat_H264_SEI_PICTIMING = 0x09, 
	NXDebugMsgCatEYE_PLEASER_STATE = 0x10, 
	NXDebugMsgCat_HTTP_REQUEST = 0x11,
	NXDebugMsgCat_TIMESHIFT_BUFFERFULL = 0x12 
}
```

### NXFileMode_

Mode for opening a file.

```
enum NXFileMode_ { 
	NXFileModeRead = 1, 
	NXFileModeWrite = 2, 
	NXFileModeReadWrite = 3, 
	NXFileModeCreate = 4 
}
```

### NXFileSeekOrigin_

Origin when seeking within a file.

```
enum NXFileSeekOrigin_ { 
	NXFileSeekOriginBeginning = 0, 
	NXFileSeekOriginCurrent = 1, 
	NXFileSeekOriginEnd = 2 
}
```

### NXDRMType_

DRM types.

```
enum NXDRMType_ { 
	NXDRMTypePayload = 0x01, 
	NXDRMTypePacket = 0x10, 
	NXDRMTypeFrame = 0x20
}
```

### NXScale

Video image scaling modes.

```
enum NXScale {
    NXScale_None = 0, 
    NXScale_OriginalSize = 1, 
    NXScale_FitInView = 2, 
    NXScale_FillView = 3,
    NXScale_Stretch = 4 
}
```

### NXKeepAliveSendMode_

Keep alive send modes.

```
enum NXKeepAliveSendMode_ {
    NXKeepAliveSendMode_None = 0x00000000, 
    NXKeepAliveSendMode_PauseState = 0x00000001, 
    NXKeepAliveSendMode_PlayState = 0x00000002, 
    NXKeepAliveSendMode_PausePlayState = 0x00000003,
    NXKeepAliveSendMode_AllState = 0x000000FF 
}
```

### NXFileFormat_

File formats.

```
enum NXFileFormat_ {
	NXFileFormatMP4 = 0x00000001, 
	NXFileFormatAMRNB = 0x00000002, 
	NXFileFormatAMRWB = 0x00000004, 
	NXFileFormatADIFAAC = 0x00000008,
	NXFileFormatMP3 = 0x00000010, 
	NXFileFormatADTSAAC = 0x00000020, 
	NXFileFormatAVI = 0x00000040,
	NXFileFormatASF = 0x00000080,
	NXFileFormatRMFF = 0x00000100, 
	NXFileFormatMKV = 0x00000200, 
	NXFileFormatPDCF = 0x00000400,
	NXFileFormatOGM = 0x00000800,
	NXFileFormatOGG = 0x00001000, 
	NXFileFormatMPEG_PS = 0x00002000, 
	NXFileFormatMPEG_TS = 0x00004000, 
	NXFileFormatFLV = 0x00008000,
	NXFileFormatQCELP = 0x00010000, 
	NXFileFormatFLAC = 0x00020000, 
	NXFileFormatAPE = 0x00040000,
	NXFileFormatMOV = 0x00080000,
	NXFileFormatWAV = 0x00100000, 
	NXFileFormatNONE = 0x7FFFFFFF 
}
```

### NXRTSPOptions_

RTSP options

```
enum NXRTSPOptions_ {
	NXRTSPOptionsSendModeNone = 0x00000000, 
	NXRTSPOptionsDescribe = 0x00000001, 
	NXRTSPOptionsFirstSetup = 0x00000002, 
	NXRTSPOptionsEverySetup = 0x00000004,
	NXRTSPOptionsFirstPlay = 0x00000008, 
	NXRTSPOptionsEveryPlay = 0x00000010, 
	NXRTSPOptionsFirstPause = 0x00000020, 
	NXRTSPOptionsEveryPause = 0x00000040,
	NXRTSPExtraOptionsWaitResponse = 0x00010000, 
	NXRTSPExtraOptionsNoWaitResponse = 0x00020000
}
```

### NXRTSPOptions_

These are the available log levels for the `setLogLevel: (NXPlayer)`.

```      
- enum NXLogLevel {
    NXLogLevelError = -3, 
    NXLogLevelWarning = -2, 
    NXLogLevelDisabled = -1, 
    NXLogLevelInformation = 0,
    NXLogLevelDebug = 1, 
    NXLogLevelVerbose = 2, 
    NXLogLevelAboveVerbose = 3, 
    NXLogLevelExtraVerbose = 4 
}
```       

### NexAvailableBitrate

This enumeration defines the possible options for the `setVideoBitrates:len:withOption: (NXPlayer)`.

```
enum NexAvailableBitrate {
	NexAvailableBitrateNone = 0, 
	NexAvailableBitrateMatch = 1, 
	NexAvailableBitrateNearest = 2, 	
	NexAvailableBitrateHigh = 3,
	NexAvailableBitrateLow = 4, 
	NexAvailableBitrateInsideRange = 5 
}
```       

### NexInformativeEvent

This enumeration defines the possible events for `NXPlayer::didReceiveInformativeEvent:details:`.

```
enum NexInformativeEvent { 
	NexInformativeEventDownloadBegan = 0, 
	NexInformativeEventDownloadFinished = 1 
}
```

### NexBandwidthSegmentOption

This enumeration defines the possible options for the `NXPlayerABRController:: setTargetBandwidth:withSegmentOption:withTargetOption:`. One of the following NexBandwidthSegmentOption values, indicating how to handle the buffered content when the track switches:
       
```       
enum NexBandwidthSegmentOption { 
	NexBandwidthSegmentOptionDefault = 0, 
	NexBandwidthSegmentOptionQuickMix = 1, 
	NexBandwidthSegmentOptionLateMix = 2 
}
```       

### NexBandwidthTargetOption 
      
This enumeration defines the possible options for the `NXPlayerABRController:: setTargetBandwidth:withSegmentOption:withTargetOption:`. This can be a guide on how to use the target bandwidth value set. One of the following NexBandwidthTargetOptionoptions:       

```
enum NexBandwidthTargetOption { 
	NexBandwidthTargetOptionDefault = 0, 
	NexBandwidthTargetOptionBelow = 1, 
	NexBandwidthTargetOptionAbove = 2, 
	NexBandwidthTargetOptionMatch = 3 
}
```
       
### NexDynamicThumbnailOption 

This enumeration defines IDs for the possible options when handling Dynamic Thumbnail information in HLS & Smooth Streaming content. These are possible values for the uId parameter in `NxPlayer::setOptionDynamicThumbnailwithOption: andParam1: andParam2:`.


```
enum NexDynamicThumbnailOption { 
	NexDynamicThumbnailOptionNone = 0, 
	NexDynamicThumbnailOptionInterval = 1 
}
```

### enum NexDynamicThumbnailOption

Possible types of media which can be played by NexPlayer during playback. The primary use of NXHttpStateInfoMediaType is for representing a media type of NXHttpStateInfoFileTypeSegment.

```
enum NexDynamicThumbnailOption { 
	NexDynamicThumbnailOptionNone = 0, 
	NexDynamicThumbnail = 1 
}
```


### Typedef Documentation

### NexAudioPostProcessingParams 

The characteristics of audio samples to be provided by NexAudioPostProcessingAdapter to the audio postprocessor, which implements the NexAudioPostProcessingAdapterDelegate protocol.

```
typedef struct NexAudioPostProcessingParams NexAudioPostProcessingParams
```

### NEXFileHandle

File handle used in Remote File I/O callbacks.

This is the file handle used in calls to the various Remote File I/O callback functions. This value is returned by the file-open callback, and can be any value that the remote file callbacks can use to uniquely identify the open file instance.

```
typedef void∗ NEXFileHandle
```

### NEXFileMode

File open mode.

This is passed by NexPlayer in calls to the `NEXPLAYERRemoteFile_OpenFt` callback.

This is a bitfield, so the constants can be combined with the bitwise-or operator.

- NEX_FILE_WRITE | NEX_FILE_CREATE *Open file for writing; create if it doesn’t exist*
- NEX_FILE_READ | NEX_FILE_WRITE *Same as NEX\_FILE\_READWRITE*

```
typedef enum_NEXFileMode NEXFileMode
```

### NEXFileSeekOrigin

Origin for Remove File I/O callback seek operations.

```
typedef enum _NEXFileSeekOrigin NEXFileSeekOrigin
```

**See Also**

 - NEXPLAYERRemoteFile_SeekFt
 - NEXPLAYERRemoteFile_Seek64Ft


### NEXPLAYERRemoteFileIOInterface

A structure holding function pointers to all of the functions that comprise the Remote File I/O interface.

This structure provides replacements for the standard operating system file I/O functions. Basically, to play back local content that is not available via the standard operating system file APIs, all calls to open or read from the file are directed to the function pointers in this structure instead.

This structure is passed to the Remote File I/O Interface when registering the callbacks.

More information about each function pointer can be found in the documentation.

```
typedef struct NEXPLAYERRemoteFileIOInterface_ NEXPLAYERRemoteFileIOInterface
```

**See Also**

- NEXPLAYERRemoteFile_OpenFt
- NEXPLAYERRemoteFile_CloseFt
- NEXPLAYERRemoteFile_ReadFt
- NEXPLAYERRemoteFile_SeekFt
- NEXPLAYERRemoteFile_Seek64Ft
- NEXPLAYERRemoteFile_WriteFt
- NEXPLAYERRemoteFile_SizeFt

### NexVideoRawBits

This data structure contains information of YUV420 planar video planes (three planes including Y, U and V), pixel resolution and line stride.


```
typedef structNexVideoRawBits NexVideoRawBits
```

### NXDRMDataType

Type of data being passed for DRM descrambling.

The NXDRMDescrambler protocol handles both audio and video data; this enumeration is used to distinguish between the two when data is passed to the descrambling method.

```
typedef enum NXDRMDataType_ NXDRMDataType
```

**See Also**

-  NXDRMDescrambler for more details.


### NXDRMType

DRM types.

These are returned by DRM descramblers to indicate at what stage the descrambling takes place. Not all DRM descrambling protocols support all types; see the individual descrambler protocol documentation for details.

```
typedef enum NXDRMType_ NXDRMType
```

### NXFileFormat

File formats.

These are possible file format values that can be used forNXContentInfo::fileFormat.

```
typedef enum NXFileFormat_ NXFileFormat
```

### NXFileHandle

Opaque file handle.

This is an arbitrary value used to identify files in calls to NXRemoteFileIOInterfacemethods. The meaning of this is unique to a given implementation of NXRemoteFileIOInterface, and return values from different implementations should not be mixed.

```
typedef void ∗ NXFileHandle
```

**See Also**

- NXRemoteFileIOInterface for more details.

### NXFileMode

Mode for opening a file.

Identifies different methods for opening or creating a file. This is is passed to implementations of the NXRemoteFileIOInterfaceprotocol to indicate how a file should be opened.

```
typedef enum NXFileMode_ NXFileMode
```

**See Also**

- NXRemoteFileIOInterfacefor more details.

### NXFileSeekOrigin

Origin when seeking within a file.

Identifies different origins for seeking within a file. This is is passed to implementations of the NXRemoteFileIOInterfaceprotocol to indicate where to measure the seek offset from.

```
typedef enum NXFileSeekOrigin_ NXFileSeekOrigin
```

**See Also**

- NXRemoteFileIOInterfacefor more details.


### NXKeepAliveSendMode

Keep alive send modes.

These are possible values for the `property::NXPropertyKeepAliveSendMode`

See that property for details.

```
typedef enum NXKeepAliveSendMode_ NXKeepAliveSendMode**
```

### NXRTSPOptions

RTSP options.

These are possible values for the `::NXPropertyRTSPOptionsSendMode` property.

```
typedef enum NXRTSPOptions_ NXRTSPOptions
```

### UpdatedTextureBlock

This method is called when a new video texture is available to be rendered from the caller.

```
typedef void(∧UpdatedTextureBlock)(NexVideoTexture ∗texture)
```

Parameters

- texture: The new video texture available for rendering.


### Enumeration Type Documentation

### enum _NEXFileMode

File open mode. 

This is passed by NexPlayer in calls to the `NEXPLAYERRemoteFile_OpenFt` callback.

This is a bit field, so the constants can be combined with the bitwise-or operator.

```
// Open file for writing; create if it doesn’t exist
NEX_FILE_WRITE | NEX_FILE_CREATE 

// Same as NEX_FILE_READWRITE
NEX_FILE_READ | NEX_FILE_WRITE 
```

**Enumerator**

- `NEX_FILE_READ` Open for reading
- `NEX_FILE_WRITE` Open for writing
- `NEX_FILE_READWRITE` Open for reading and writing
- `NEX_FILE_CREATE` Create the file if it doesn’t exist

### enum _NEXFileSeekOrigin

Origin for Remove File I/O callback seek operations.

**See Also**

- NEXPLAYERRemoteFile_SeekFt
- NEXPLAYERRemoteFile_Seek64Ft
- NEX\_SEEK\_BEGIN Beginning of file
- NEX\_SEEK\_CUR Current position
- NEX\_SEEK\_END End of file

### enum NexAvailableBitrate

This enumeration defines the possible options for the setVideoBitrates:len:withOption: (NXPlayer).

**Enumerator**

- `NexAvailableBitrateNone` No restriction on subtracks other than the bitrates selected inbitrates.
- `NexAvailableBitrateMatch` Only use subtracks which have exact same bitrate as the selected bitrates passed inbitrates.
- `NexAvailableBitrateNearest` Only use subtracks which have the nearest bitrates to the target bitrates.
- `NexAvailableBitrateHigh` Only use subtracks which have bitrates equal to or higher than the target bitrate.
- `NexAvailableBitrateLow` Only use subtracks which have bitrates equal to or lower than the target bitrate.
- `NexAvailableBitrateInsideRange` Only use subtracks which have bitrates inside the range defined by the bitrates.

### enum NexBandwidthSegmentOption

This enumeration defines the possible options for the `NXPlayerABRController::setTargetBandwidth:withSegmentOption:withTargetOption:`. One of the following NexBandwidthSegmentOptionvalues, indicating how to handle the buffered content when the track switches:

**Enumerator**

- `NexBandwidthSegmentOptionDefault` Default. NexPlayer will decide between NexBandwidthSegmentOptionQuickMix (switching tracks quickly) and NexBandwidthSegmentOptionLateMix (playing buffered content and changing tracks more slowly).
- `NexBandwidthSegmentOptionQuickMix` NexPlayer will clear the buffer as much as possible and will start to download a new track so the user can switch faster.
- `NexBandwidthSegmentOptionLateMix` NexPlayer will preserve and play the content segments already
buffered, and will download a new track.

### enum NexBandwidthTargetOption

This enumeration defines the possible options for the NXPlayerABRController:: setTargetBandwidth:withSegmentOption:withTargetOption:. This can be a guide on how to use the target bandwidth value set. One of the following NexBandwidthTargetOptionoptions:

**Enumerator**

- `NexBandwidthTargetOptionDefault` Default target option (NexBandwidthTargetOptionBelow).
- `NexBandwidthTargetOptionBelow` Select a track with a bandwidth below the target bandwidth.
- `NexBandwidthTargetOptionAbove` Select a track with a bandwidth above the target bandwidth.
- `NexBandwidthTargetOptionMatch` Select the track that has a bandwidth that matches the set target. Otherwise send an error and no new target bandwidth will be selected.

### enum NexDynamicThumbnailOption

This enumeration defines IDs for the possible options when handling Dynamic Thumbnail information in HLS & Smooth Streaming content. These are possible values for theuIdparameter in `NxPlayer::setOptionDynamicThumbnailwithOption: andParam1: andParam2:`.

### enum NexHLSTSDescrambleResult

This enumeration defines the possible return values from a NXHLSTSDescrambler method.

### enum NexInformativeEvent

This enumeration defines the possible events for NXPlayer::didReceiveInformativeEvent:details:.

**Enumerator**

NexInformativeEventDownloadBegan Download of a URL began. Parameter keys in details: kNexInformativeEventURL.

NexInformativeEventDownloadFinished Download of a URL finished. Parameter keys in details: kNex-
InformativeEventURL, and kNexInformativeEventResult.

### enum NXBufferInfoMediaType

This enumeration defines the possible stream type forNXBufferInfoMediaType.

**Enumerator**

- `NXBufferInfoMediaTypeVideo` Video stream type.
- `NXBufferInfoMediaTypeAudio` Audio stream type.
- `NXBufferInfoMediaTypeText` Text stream type.

### enum NXBufferingState

This enumeration defines the possible buffering state for NXBufferingState.

### enum NXCEA608Channel

CEA 608 Channel IDs. These are possible values for `NXPlayer::selectedCEA608Channel`.

They set the channel from which CEA 608 closed captions will be received. While there are four channels to receive caption information from the NTSC line 21 fields, as channels 1 and 2 share field 1 and channels 3 and 4 share field 2, the most common channels used to receive captions are channels 1 and 3. These channels can represent the same information in different languages and are often intended to be selected by the user from the application.

**Enumerator**

- `NXCEA608Channel_None` No CEA 608 captions (disable)
- `NXCEA608Channel_Ch1` NTSC line 21 field 1 closed captions (first channel); CEA 608 Caption Channel 1.
- `NXCEA608Channel_Ch2` NTSC line 21 field 1 closed captions (second channel); CEA 608 Caption Channel 2.
- `NXCEA608Channel_Ch3` NTSC line 21 field 2 closed captions (first channel); CEA 608 Caption Channel 3.
- `NXCEA608Channel_Ch4` NTSC line 21 field 2 closed captions (second channel); CEA 608 Caption Channel 4.

### enum NXCEA608Charset

CEA 608 Character Set IDs. These are used to choose the character set to display CEA 608 closed caption information.

**Enumerator**

- `NXCEA608Charset_Unicode` Unicode character set.
- `NXCEA608Charset_Private1` For use with a private, non-standard character set. May be ignored.
- `NXCEA608Charset_Private2` For use with a private, non-standard character set. May be ignored.
- `NXCEA608Charset_KSC_5601_1987` Korean character set.
- `NXCEA608Charset_GB_2312_80` Chinese character set.

### enum NXCEA608Color

CEA 608 Colors. These are used to indicate the foreground and background colors associated with CEA 608 closed captions. Note that only the semi-transparent options will be used for background color of captions.

**Enumerator**

- `NXCEA608Color_White` white
- `NXCEA608Color_White_Semitrans` semi-transparent white
- `NXCEA608Color_Green` green
- `NXCEA608Color_Green_Semitrans` semi-transparent green
- `NXCEA608Color_Blue` blue
- `NXCEA608Color_Blue_Semitrans` semi-transparent blue
- `NXCEA608Color_Cyan` cyan
- `NXCEA608Color_Cyan_Semitrans` semi-transparent cyan
- `NXCEA608Color_Red` red
- `NXCEA608Color_Red_Semitrans` semi-transparent red
- `NXCEA608Color_Yellow` yellow
- `NXCEA608Color_Yellow_Semitrans` semi-transparent yellow
- `NXCEA608Color_Magenta` magenta
- `NXCEA608Color_Magenta_Semitrans` semi-transparent magenta
- `NXCEA608Color_Black` black
- `NXCEA608Color_Black_Semitrans` semi-transparent black
- `NXCEA608Color_Transparent` transparent (only used for background color)
- `NXCEA608Color_Default` This value is only used when overriding font attribute.
- `NXCEA608Color_Last` This value marks the maximum possible color value.

### enum NXCodecID

Codec type identifiers. These are used with NXContentInformation::audioCodec, NXContentInformation::videoCodecandNXContentInformation::captionType.

### enum NXDebugMsgCat

Debugging Messages to include. These are possible values fornexPlayer:debugMessage:category: (NXPlayerDelegate-p) and set the debugging messages to be provided.

**Enumerator**

- `NXDebugMsgCat_RTSP` Debugging information related to the RTSP connection status.
- `NXDebugMsgCat_RTP_RECV` Debugging information associated with the start of an RTP packet receipt.
- `NXDebugMsgCat_RTP_RECV_END` Debugging information associated with the end of an RTP packet receipt.
- `NXDebugMsgCat_RTCP_RR_SEND` Debugging information associated with the transmission of an RTCP RR (Receiver Report) packet.
- `NXDebugMsgCat_RTCP_BYE_RECV` This occurs when an RTCP BYE packet is received.
- `NXDebugMsgCat_CONTENT_INFO` General information about the content that is currently playing.
- `NXDebugMsgCat_HTTP_RESPONSE` Debugging information of HTTP Response.
- `NXDebugMsgCat_DOWNLOADED_BUFF` Debugging information of downloaded buffer.
- `NXDebugMsgCat_DECODING` Debugging information of decoding event.
- `NXDebugMsgCat_H264_SEI_PICTIMING` Debugging information for handling H.264 SEI picture timing information.
- `NXDebugMsgCat_EYE_PLEASER_STATE` Debugging information of Eye-Pleaser State.
- `NXDebugMsgCat_HTTP_REQUEST` Debugging information of HTTP request.
- `NXDebugMsgCat_TIMESHIFT_BUFFERFULL` Debugging information of full of buffer for TimeShift.

### enum NXDeviceInfoConnectionType

NexPlayer connection types.

**Enumerator**

- `NXDeviceInfoConnectionTypeUnknown` Unknown connection type.
- `NXDeviceInfoConnectionTypeNone` Not connected.
- `NXDeviceInfoConnectionTypeWWAN` Cellular connection.
- `NXDeviceInfoConnectionTypeWiFi` WiFi connection.

### enum NXDRMDataType_

Type of data being passed for DRM descrambling.
The NXDRMDescrambler protocol handles both audio and video data; this enumeration is used to distinguish between the two when data is passed to the descrambling method.

**See Also**

- NXDRMDescrambler for more details.

### enum NXDRMType_

DRM types. These are returned by DRM descramblers to indicate at what stage the descrambling takes place. Not all DRM descrambling protocols support all types; see the individual descrambler protocol documentation for details.

**Enumerator**

- `NXDRMTypePayload` Descrambling is done at the payload level.
- `NXDRMTypePacket` Descrambling is done at the packet level.
- `NXDRMTypeFrame` Descrambling is done individually for each frame.

### enum NXError

NexPlayer error codes. There are many error codes defined in this enum, but only the error codes documented here are used.

**Enumerator**

- `NXErrorNone` No error.
- `NXErrorHasNoEffect` Already in the requested state or non-valid command (Ex: seek for live-streaming).
- `NXErrorInvalidParameter` One or more of the parameters passed in is invalid.
- `NXErrorInvalidInfo` One or more of the information passed in is invalid.
- `NXErrorInvalidState` The command is not valid at the current state. (Ex. NexPlayerSWPPause function is called when the current state is NEXPLAYERSTATEPAUSE)
- `NXErrorMemoryOperation` The memory operation failed. (Ex. heap memory allocation)
- `NXErrorFileOperation` The file operation failed. (Ex. file seek, file open)
- `NXErrorNotSupportAudioCodec` The content included unregistered audio codec type.
- `NXErrorNotSupportVideoCodec` The content included unregistered video codec type.
- `NXErrorInvalidCodec` The content includes unknown audio or video codec type.
- `NXErrorCodec` An error occurred at audio or video decoding.
- `NXErrorAsyncOthercmdPrcessing` The command queue for processing invoked Async functions was full.
- `NXErrorRTCPByeReceived` An error occurred in receiving RTCP BYE message from streaming server.
- `NXErrorUserTerminated` Terminated by the user.
- `NXErrorDataInactivityTimeout` An unhandled nexPlayerDataInactivityTimeout: (NXPlayerDelegate-p)event occurred.
- `NXErrorNetworkProtocol` Network or protocol error.
- `NXErrorMediaNotFound` Media not found at the URL.
- `NXErrorDrmDecryptFailed` DRM decryption failure.
- `NXErrorDrmInitFailed` DRM init failure.
- `NXErrorRTSPCommandTimeout` An unhandled nexPlayerRTSPCommandTimeout: (NXPlayerDelegate-p) event occurred.
- `NXErrorPauseSupervisionTimeout` An unhandled nexPlayerPauseSupervisionTimeout: (NXPlayer-
Delegate-p) event occurred.

### enum NXFileFormat_

File formats. These are possible file format values that can be used forNXContentInfo::fileFormat.

**Enumerator**

- `NXFileFormatMP4` MP4.
- `NXFileFormatAMRNB` AMR-NB.
- `NXFileFormatAMRWB` AMR-WB.
- `NXFileFormatADIFAAC` ADIFAAC.
- `NXFileFormatMP3` MP3.
- `NXFileFormatADTSAAC` ADTSAAC.
- `NXFileFormatAVI` AVI.
- `NXFileFormatASF` ASF.
- `NXFileFormatRMFF` RMFF.
- `NXFileFormatMKV` MKV.
- `NXFileFormatPDCF` PDCF.
- `NXFileFormatOGM` OGM.
- `NXFileFormatOGG` OGG.
- `NXFileFormatMPEG_PS` MPEG-PS.
- `NXFileFormatMPEG_TS` MPEG-TS.
- `NXFileFormatFLV` FLV.
- `NXFileFormatQCELP` QCELP.
- `NXFileFormatFLAC` FLAC.
- `NXFileFormatAPE` APE.
- `NXFileFormatMOV` MOV.
- `NXFileFormatWAV` WAV.

### enum NXFileMode_

Mode for opening a file. Identifies different methods for opening or creating a file. This is is passed to implementations of the NXRemoteFileIOInterfaceprotocol to indicate how a file should be opened.

**See Also**

NXRemoteFileIOInterface for more details.

**Enumerator**

- `NXFileModeRead` Read
- `NXFileModeWrite` Write
- `NXFileModeReadWrite` Read and Write
- `NXFileModeCreate` Create

### enum NXFileSeekOrigin_

Origin when seeking within a file. Identifies different origins for seeking within a file. This is is passed to implementations of theNXRemoteFileIOInterfaceprotocol to indicate where to measure the seek offset from.

**See Also**

- NXRemoteFileIOInterfacefor more details.

**Enumerator**

- `NXFileSeekOriginBeginning` Beginning of file
- `NXFileSeekOriginCurrent` Current position
- `NXFileSeekOriginEnd` End of file

### enum NXKeepAliveSendMode_

Keep alive send modes. These are possible values for the  property::NXPropertyKeepAliveSendMode
See that property for details.


**Enumerator**

- `NXKeepAliveSendMode_None` None.
- `NXKeepAliveSendMode_PauseState` Pause only.
- `NXKeepAliveSendMode_PlayState` Play only.
- `NXKeepAliveSendMode_PausePlayState` Pause and play.
- `NXKeepAliveSendMode_AllState` All.

### enum NXLogLevel

These are the available log levels for the setLogLevel: (NXPlayer).
The higher the log level, the more logs will be enabled. The following are the log levels in ascending order :

1. NXLogLevelError (Lowest level)
2. NXLogLevelWarning
3. NXLogLevelInformation
4. NXLogLevelDebug
5. NXLogLevelVerbose
6. NXLogLevelAboveVerbose
7. NXLogLevelExtraVerbose (Highest level)

> **Note** NXLogLevelDisabled disables the log.

**Enumerator**

* `NXLogLevelError` Enables error level log only.
* `NXLogLevelWarning` Enables warning level log and below.
* `NXLogLevelDisabled` Log disabled.
* `NXLogLevelInformation` Enables information level log and below (default)
* `NXLogLevelDebug` Enables debug level log and below.
* `NXLogLevelVerbose` Enables verbose level log and below.
* `NXLogLevelAboveVerbose` Enables above verbose level log and below. This will have more logs than the verbose level.
* `NXLogLevelExtraVerbose` Enables extra verbose level log and below. This will have more logs than the above verbose level.

### enum NXMediaType

Media types. These are used with NXMediaStreamInfo::typeto indicate the type of the stream (audio or video) described by `NXMediaStreamInfo`.

**Enumerator**

* `NXMediaTypeUnknown` Unknown media type.
* `NXMediaTypeAudio` Audio only stream.
* `NXMediaTypeVideo` Video only stream.
* `NXMediaTypeText` Text stream.
* `NXMediaTypeAV` A/V stream.

### enum NXOnOffDefault

Deprecated This has been deprecated since version 5.16. Do not use.

### enum NXOpenMode

Open modes. These are possible argument values for mode parameter in open: (NXPlayer).

**Enumerator**

- `NXOpenModeAuto` Select streaming play for "http:", "https:", "rtsp:" and "mms:" addresses, local play for everything else.
- `NXOpenModeLocal` Plays a local file, given a local path or a URL starting with "file://".
- `NXOpenModeStreaming` Plays streaming video; if a path (not a URL) is given, it is assumed to be a path to an SDP file for an RTSP stream.
- `NXOpenModeLocalBundle` Plays a local file from the current application bundle (a relative path should be passed)
- `NXOpenModeLocalDocs` Plays a local file from the application documents area (the area where files are placed if added via iTunes)
- `NXOpenModeStoreStream` New source type value for storing HLS Stream.

### enum NXPlaybackType

Playback types.

**Enumerator**

- `NXPlaybackTypeLocal` Content is local (local path or "file://" URL)
- `NXPlaybackTypeStreaming` Content is streaming (including on-demand, progressive download or live)

### enum NXPlayerState

Possible states of the player (paused, stopped, etc.). The current player state is available through `NXPlayer::state`.

**Enumerator**

- `NXPlayerStateNone` No current valid state (for example API not initialized)
- `NXPlayerStateClose` Content is currently closed.
- `NXPlayerStateStop` Content is open and stopped.
- `NXPlayerStatePlay` Content is open and playing.
- `NXPlayerStatePause` Content is open and paused during playback.

### enum NXRTSPMethod

RTSP method identifiers. These are used withaddRTSPHeaderField:forMethods: (NXPlayer)

**Enumerator**

- `NXRTSPMethodNone` No RTSP method.
- `NXRTSPMethodDescribe` RTSP DESCRIBE method (request presentation description, generally SDP)
- `NXRTSPMethodSetup` RTSP SETUP method (specify ports, transport, etc.)
- `NXRTSPMethodPlay` RTSP PLAY method (request playback)
- `NXRTSPMethodPause` RTSP PAUSE method (pause playback)
- `NXRTSPMethodTeardown` RTSP TEARDOWN method (stop media streams and terminate session)
- `NXRTSPMethodOptions` RTSP OPTIONS.
- `NXRTSPMethodRedirect` RTSP REDIRECT.
- `NXRTSPMethodSetParameter` RTSP GET PARAMETER.
- `NXRTSPMethodGetParameter` RTSP SET PARAMETER.
- `NXRTSPMethodAnnounce` RTSP ANNOUNCE.
- `NXRTSPMethodPlaylist` RTSP PLAYLIST.
- `NXRTSPMethodAll` Indicates all current and future RTSP method types.

### enum NXRTSPOptions_

RTSP options. These are possible values for the::NXPropertyRTSPOptionsSendModeproperty.

**Enumerator**

* `NXRTSPOptionsSendModeNone` No send-mode options specified.
* `NXRTSPOptionsDescribe` Send RTSP OPTIONS before RTSP DESCRIBE.
* `NXRTSPOptionsFirstSetup` Send RTSP OPTIONS before the first RTSP SETUP Request.
* `NXRTSPOptionsEverySetup` Send RTSP OPTIONS before every RTSP SETUP Request.
* `NXRTSPOptionsFirstPlay` Send RTSP OPTIONS before the first RTSP PLAY Request.
* `NXRTSPOptionsEveryPlay` Send RTSP OPTIONS before every RTSP PLAY Request.
* `NXRTSPOptionsFirstPause` Send RTSP OPTIONS before the first RTSP PAUSE Request.
* `NXRTSPOptionsEveryPause` Send RTSP OPTIONS before every RTSP PAUSE Request.
* `NXRTSPExtraOptionsWaitResponse` Wait for extra OPTIONS response timeout.
* `NXRTSPExtraOptionsNoWaitResponse` Do not wait for extra OPTIONS response timeout.

### enum NXScale

Video image scaling modes. These are various possible automatic video scaling modes that can be set for NXPlayerView::autoScaling.

**Enumerator**

* `NXScale_None` No automatic scaling.
* `NXScale_OriginalSize` Original video size.
* `NXScale_FitInView` Fit video to container (as large as possible without cropping; maintain aspect ratio)
* `NXScale_FillView` NexPlayer will fill the parent container (crop and maintain aspect ratio)
* `NXScale_Stretch` Stretch to container dimensions (does not maintain aspect ratio)

### enum NXTransportType

Transport layers (TCP and UDP) for RTP and RTCP packets.

**Enumerator**

- `NXTransportTypeTCP` RTP/RTCP over TCP.
- `NXTransportTypeUDP` RTP/RTCP over UDP.

### Function Documentation

#### typedef NS_OPTIONS ( NSUInteger, NXHttpStateInfoMediaType )

Possible types of media which can be played by NexPlayer during playback. The primary use of `NXHttpStateInfoMediaType` is for representing a media type of `NXHttpStateInfoFileTypeSegment`.

**See Also**

- NXHttpStateInfoDownStart for more details.
