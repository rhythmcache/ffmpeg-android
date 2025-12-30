# Build Changelog

**Commit:** ee2eb6ced80f6799f348f56803e939b0f1e0f3b8
**Author:** Zhao Zhili <zhilizhao@tencent.com>
**Date:** Mon Dec 29 07:25:49 2025 +0000

fftools/ffmpeg_filter: fix access private API of libavcodec

Firstly, mathops.h is a private header of libavcodec and should not be used
in fftools. It may reference libavcodec internal symbols, causing link
error with dynamic library, e.g.,

fftools/ffmpeg_filter.c:2687: undefined reference to `ff_rv_zbb_supported'

Secondly, mid_pred operates on int types, while current use case is
int64_t.
