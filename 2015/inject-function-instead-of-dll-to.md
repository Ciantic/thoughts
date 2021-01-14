---
title: 'Inject a function (instead of DLL) to target process in Windows'
date: 2015-11-12T01:27:00.002-08:00
oldUrl: "http://ciantic.blogspot.com/2015/11/inject-function-instead-of-dll-to.html"
---

When I was doing my [Disable Flashing Taskbar Buttons patch to explorer.exe](./in-memory-patching-explorerexe-to.md) first I did it by injecting AutoHotkey.dll inside explorer.exe and patched it this way.  
  
Since the only thing I needed was a call `GetWindowLongPtrW` to get the task switcher memory location, I started to look a better way.  
  
Turns out it's quiet simple.  
  
`CreateRemoteThread` is the function (usually?) used to inject a DLL by making target process to run LoadLibrary, but instead you can of course use it to run arbitrary assembly since it takes address.  
  
Only trick is to turn your function (in my case call to `GetWindowLongPtrW`) to function call that takes single argument.  
  
I made a little C program for this:  
  
```C
struct MyParams {
 HWND hWnd;
 int nIndex;
 LONG_PTR res;
};

void __stdcall myInjectFunction(LPVOID params) {
 MyParams *myParams = (MyParams*) params;
 myParams->res = GetWindowLongPtrW(myParams->hWnd, myParams->nIndex);
}

int main()
{
 MyParams myParams;
 myParams.hWnd = (HWND) 0x123456;
 myParams.nIndex = 0xFF;
 myInjectFunction(&myParams);
    return 0;
}
```

myInjectFunction is the function to be injected, above code must be compiled by disabling inlining. If you run it through disassembler e.g. "dumpbin /disasm /all yourprogram.exe" you should get something like:

```
40 53              push   rbx
48 83 EC 20        sub    rsp,20h
8B 51 08           mov    edx,dword ptr [rcx+8]
48 8B D9           mov    rbx,rcx
48 8B 09           mov    rcx,qword ptr [rcx]
FF 15 6B 10 00 00  call   qword ptr [__imp_GetWindowLongPtrW]
48 89 43 10        mov    qword ptr [rbx+10h],rax
48 83 C4 20        add    rsp,20h
5B                 pop    rbx
C3                 ret
CC               
```

Above is assembly 101 function body, with some ptr trickery. This assembly contains a one flaw though, for to be uses as is, even though GetWindowLongPtrW is in known memory location (user32 and kernel32 has de-facto memory locations) it's not in right form to be used.

The call to GetWindowLongPtrW must be in longer form:

```
40 53              push   rbx
48 83 EC 20        sub    rsp,20h
8B 51 08           mov    edx,dword ptr [rcx+8]
48 8B D9           mov    rbx,rcx
48 8B 09           mov    rcx,qword ptr [rcx]
48 B8 XX XX XX XX XX XX XX XX movabs rax, GetWindowLongPtrW
FF D0              call   rax
48 89 43 10        mov    qword ptr [rbx+10h],rax
48 83 C4 20        add    rsp,20h
5B                 pop    rbx
C3                 ret
CC            
```

You can try out changing the assembly runtime with x64dbg until it works.  

In this demonstration I won't fill the 8 byte (XX) address because you have to determine it runtime by calling `GetProcAddress` and then transforming it to reversed hexadecimal form.

After this one simply writes the bytes using `WriteProcessMemory` and calls `CreateRemoteThread` with newly created memory address and it just works just like the C equivalent did.

Now my script was dependency free, pure AHK script.