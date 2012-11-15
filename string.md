[content]: https://github.com/1184893257/simplelinux/blob/master/README.md#content

[��Ŀ¼][content]

<a name="top"></a>

<h1 align="center">�ַ���
</h1>

������һƪ�����ַ������ַ���������ʹ�ã�
������������Ҳ���٣�

## һ���ַ����Ĵ洢λ��

����CԴ����string1.c����

	#include <stdio.h>
	
	int main()
	{
		puts("Hello, World!");
		return 0;
	}

`����`����ֱ�ӿ���ִ���ļ��ķ��������

	[lqy@localhost temp]$ gcc -o string1 string1.c
	[lqy@localhost temp]$ ./string1 
	Hello, World!
	[lqy@localhost temp]$ objdump -s -d string1 > string1.txt
	[lqy@localhost temp]$ 

`����`string1.txt �еĲ����������£�

<pre><code>Contents of section .rodata:
 8048488 03000000 01000200 00000000 48656c6c  ............Hell
 8048498 6f2c2057 6f726c64 2100               o, World!.      

...

080483b4 &lt;main>:
 80483b4:	55                   	push   %ebp
 80483b5:	89 e5                	mov    %esp,%ebp
 80483b7:	83 e4 f0             	and    $0xfffffff0,%esp
 80483ba:	83 ec 10             	sub    $0x10,%esp<b>
 80483bd:	c7 04 24 94 84 04 08 	movl   $0x8048494,(%esp)
 80483c4:	e8 27 ff ff ff       	call   80482f0 &lt;puts@plt></b>
 80483c9:	b8 00 00 00 00       	mov    $0x0,%eax
 80483ce:	c9                   	leave  
 80483cf:	c3                   	ret    
</code></pre>

�����ɼ� 0x8048494 Ӧ���� "Hello, World!" �ĵ�ַ��
Ȼ������ .rodata ���� 0x8048488 + 12 �����ô洢��
 "Hello, World!" �ĸ����ַ���
<a target="_blank" href="http://www.asciitable.com/">ASCII��</a>��
'H' �� <a target="_blank" href="http://www.asciitable.com/">ASCII��</a>�� 0x48��
����̾�� '!' �� <a target="_blank" href="http://www.asciitable.com/">ASCII��</a> ���� 0x21��
�����������Զ���Ϊ�������˸��ַ��������� 0x00��
<b>ֻҪ��˫�������������ַ����������������Զ���Ϊ���Ǽӽ�������</b>

�����ɴ����Ƿ��֣�
<b>�ַ�����ȫ�ֱ���һ����Ϊ��̬���ݴ洢�ڿ�ִ���ļ��У�
��ʹ�õ�ʱ���ó�����ַ�����ʡ�</b>

���������ַ����������� .rodata ���У�
������е������� .text �Σ�����Σ��е�����һ��
�ڿ�ִ���ļ��������ڴ�����ʱ
����ֻ���ģ������ֻ����ͨ����ҳ����ʵ�ֵģ�
��ҳ���������һ��λ������Ϊ 1 ��ʾ��ҳ��д��
����Ϊ 0 ��ʾ��ҳֻ���������ͼ��ֻ����ҳ��д�����ݣ�
CPU �ͻᴥ��ҳ�����쳣����
<b>����Դ�ַ����е��κ��ַ��������ڳ�������ʱ����</b>��

## �����ַ���ָ�� �� �ַ�����

����CԴ����string2.c����

	#include <stdio.h>
	
	int main()
	{
		char *s1 = "1234567";
		char s2[]= "1234567";
		
		puts(s1);
		puts(s2);
		return 0;
	}

`����`��ִ���ļ��ķ�������ĸ�ֵ�������£�

	 80483bd:	c7 44 24 1c c4 84 04 	movl   $0x80484c4,0x1c(%esp)
	 80483c4:	08 
	 80483c5:	a1 c4 84 04 08       	mov    0x80484c4,%eax
	 80483ca:	8b 15 c8 84 04 08    	mov    0x80484c8,%edx
	 80483d0:	89 44 24 14          	mov    %eax,0x14(%esp)
	 80483d4:	89 54 24 18          	mov    %edx,0x18(%esp)

`����`0x80484c4 ���ַ���"1234567"�ĵ�ַ��
���ԣ�<b>�����ַ�����ֵ��ָ��ʱ���ݵ���Դ�ַ����ĵ�ַ��
����ֵ���ֲ��ַ�����ʱ��Ҫ��������һ�����������ֲ������ռ�</b>��
��˵�2�ַ�ʽ���˷ѿռ䣨4�ֽ� vs 8�ֽڣ�
���˷�ʱ�䣨1��mov vs 4��mov�������ǵ�2�ַ�ʽҲ����
һ���Ǵ���<b>��1�ַ�ʽ���ݵ���Դ�ַ����ĵ�ַ��
��Դ�ַ�����ֻ��ҳ�У��޷��޸ģ������ַ�����ȴ�����޸�</b>��

�������飺��������б�����û��Ķ����ַ�����
�Ǿ���ָ��ɣ������� �ַ����� �� ��̬����Ŀռ� ���档

## ������ʽ������ �� ת���

����������֣������������ַ����и�ʽ��������ת���������ȥ����
CԴ����string3.c����

	#include <stdio.h>
		
	int main()
	{
		printf("--------\n%d\n", 123);
		return 0;
	}

### ���Դ�ļ���

	gcc -S string3.c

`����`������£�

	.LC0:
		.string	"--------\n%d\n"

### Ŀ���ļ���

	gcc -c string3.c
	objdump -s -d string3.o > string3.txt

`����`-c Ĭ������� string3.o �ļ��У�
string3.txt �е��ַ�����

	Contents of section .rodata:
	 0000 2d2d2d2d 2d2d2d2d 0a25640a 00        --------.%d..   

`����`����'\n'���滻���� 0x0a��%d û��

### ��ִ���ļ���

	gcc -o string3 string3.c
	objdump -s -d string3 > string3.txt

`����`��ִ���ļ���Ŀ���ļ�һ����

	Contents of section .rodata:
	 80484a8 03000000 01000200 00000000 2d2d2d2d  ............----
	 80484b8 2d2d2d2d 0a25640a 00                 ----.%d..       

`����`��������֪���ˣ�<b>ת����ڱ�ɶ������ļ���
�ͱ�ת��Ϊ����������Ǹ��ַ���</b>��
����ʽ��������Ȼ��Ҫ���� printf ����ʱ�õġ�
֪�������ʲô�ã������������� printf ������
��ôת���ַ����ǾͲ��ò����ˣ�
�������������ת���ȥ�ġ�

����������뿴�� printf ��ŵ�ʵ�֣�
linux 0.01 �� kernel/vsprintf.c ����һ���򻯵�
��û��ʵ�ָ������Ĵ���ʵ�֣�����ת���ַ��ǲ����ĵġ�

linux ���汾�ں�Դ���룺<a target="_blank" href="http://www.kernel.org/pub/linux/kernel/">http://www.kernel.org/pub/linux/kernel/</a>  
linux 0.01��<a target="_blank" href="http://www.kernel.org/pub/linux/kernel/Historic/">http://www.kernel.org/pub/linux/kernel/Historic/</a>

[��Ŀ¼][content]
