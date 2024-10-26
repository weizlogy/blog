---
layout: post
title:  "Windows XP上でIcmp6SendEcho2()呼び出し時、異常終了しないために"
date:   2012-03-10 14:48:00.001 09:00
categories: system-dev
---

Windows APIのIcmp6SendEcho2()をWindows XPで呼び出すときは以下の点に注意が必要です。

[Syntax from msdn.](http://msdn.microsoft.com/en-us/library/windows/desktop/aa366041(v=vs.85).aspx)

```C++
DWORD Icmp6SendEcho2(
  __in      HANDLE IcmpHandle,
  __in_opt  HANDLE Event,
  __in_opt  PIO_APC_ROUTINE ApcRoutine,
  __in_opt  PVOID ApcContext,
  __in      struct sockaddr_in6 *SourceAddress,
  __in      struct sockaddr_in6 *DestinationAddress,
  __in      LPVOID RequestData,
  __in      WORD RequestSize,
  __in_opt  PIP_OPTION_INFORMATION RequestOptions,
  __out     LPVOID ReplyBuffer,
  __in      DWORD ReplySize,
  __in      DWORD Timeout
);
```

- 第9引数 PIP_OPTION_INFORMATION は必須です。Vista 以降のOSで動かす場合は任意です。（NULLでもよい）
- 第10引数 ReplyBuffer は80byte以上の領域がないとWin32エラーコード122（システム コールに渡されるデータ領域が小さすぎます）が発生します。

IcmpSendEcho()とは設定値が微妙に異なりますね。
