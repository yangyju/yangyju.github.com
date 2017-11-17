---
layout: post
title: "getsockname()"
---
[getsockname in msdn](https://msdn.microsoft.com/en-us/library/windows/desktop/ms738543(v=vs.85).aspx)

Syntax:
```cpp
//cpp
int getsockname(
  _In_    SOCKET          s,
  _Out_   struct sockaddr *name,
  _Inout_ int             *namelen
);
```
```cpp
//cpp
//getsockname( m_server,  ( struct sockaddr* )&sockaddr_name,  &namelen);

//getpeername( m_server,  ( struct sockaddr* )&sockaddr_name,  &namelen);  

getsockname(client_user,  ( struct sockaddr* )&sockaddr_name,  &namelen);   

getpeername( client_user,  ( struct sockaddr* )&sockaddr_name,  &namelen);
```
