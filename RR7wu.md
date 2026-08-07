# Write up: [RE]RR7's secret key
difficulity: 1.0
Quality: 4.0
## The Title
<img width="1315" height="594" alt="image" src="https://github.com/user-attachments/assets/76ffb82c-ef9e-4208-8207-5fe605d27f71" />

[you can find  the challenge in here](https://crackmes.one/crackme/6a46f20c8a86e4c2c5525631)

## Information Gathering

I drop the file in the ghidra, open code browser
find the main function in the symbol tree <img width="1068" height="437" alt="image" src="https://github.com/user-attachments/assets/4910a132-8800-4347-804f-f3a9509469ff" />
Decompile the main function into C pseudocode.

```C
int __cdecl main(int _Argc,char **_Argv,char **_Env)

{
  int iStack_10;
  int iStack_c;
  
  __main();
  printf("Enter Your Number : ");
  scanf("%i",&iStack_c);
  if (iStack_c == 0x21) {
    printf("Enter The Secret Key : ");
    scanf("%i",&iStack_10);
    if (iStack_10 == 0x66) {
      printf("Congratulations, you have completed the challenge!");
    }
  }
  return 0;
}
```

In the decompiled code, we can see that to bypass the challenge, we need to satisfy two 'if' conditions

```C
if (iStack_c == 0x21) {
    printf("Enter The Secret Key : ");
    scanf("%i",&iStack_10);
    if (iStack_10 == 0x66) {
      printf("Congratulations, you have completed the challenge!");
    }
}
```
the true number is 0x21(hex) and the secret key is 0x66
now, changing the hex to dec, the true number is 33 and the secret number is 102

<img width="623" height="70" alt="image" src="https://github.com/user-attachments/assets/c663b720-d42b-49a1-9c78-d07a1957e3e7" />
