[content]: https://github.com/1184893257/simplelinux/blob/master/README.md#content

[��Ŀ¼][content]

<a name="top"></a>

<h1 align="center">�ṹ��
</h1>

�����ṹ���� C ������Ҫ���Զ������ͷ�����
��ƪ������ʶһ�½ṹ�塣

## һ���ṹ�����̬

����CԴ����struct.c����

	#include <stdio.h>
	
	typedef struct{
		unsigned short int a;
		unsigned short int b;
	}Data;
	
	int main()
	{
		Data c, d;
		
		c.a = 1;
		c.b = 2;
		d = c;
		
		printf("d.a:%d\nd.b:%d\n", d.a, d.b);
		return 0;
	}

`����`��ֵ���ַ����

		movw	$1, 28(%esp)	# c.a = 1
		movw	$2, 30(%esp)	# c.b = 2
		movl	28(%esp), %eax	#
		movl	%eax, 24(%esp)	# d = c

`����`���Կ�����

* c.a ���� 28(%esp) ֮���2���ֽ�
* c.b ���� 30(%esp) ֮���2���ֽ�
* c �� 28(%esp) ֮���4���ֽ�
* d �� 24(%esp) ֮���4���ֽ�

`����`���ò���̾���֣��ṹ�����֡���Ԫ�����֣���һ�α������ˣ�
��Ԫ����������������ڽṹ���ƫ�ơ�

## �����ṹ��ĸ���

������һ��ʱ����ʦǧ������������<b>���鲻�ܸ��ƣ�</b>��
���ǵ�����������������������к��������ˣ�block.c����

	#include <stdio.h>
	
	typedef struct{
		char data[1000];
	}Block;
	
	Block a={{'a','b','c',}};
	
	int main()
	{
		Block b;

		b=a;
		
		puts(b.data);
		return 0;
	}

`����`Block a={{'a','b','c',}} �Ƕ� a �Ĳ��ֳ�ʼ����
'c' �����Զ��� 0��д�� Block a={{"abc"}} Ҳһ����
C ���ԶԳ�ʼ�����Ǻܿ��ݵġ�

����������������Ȼ�����ı��롢�����ˣ��⾿�������������죿
������ಿ�֣�

	leal	24(%esp), %edx
	movl	$a, %ebx
	movl	$250, %eax
	movl	%edx, %edi	# edi = &b
	movl	%ebx, %esi	# esi = &a
	movl	%eax, %ecx	# ecx = 250
	rep movsl

`����`���Ƿ��ֳ���ȷʵͨ�� 250 �� movsl ������һ��"����"��
��ԭ���ǣ��ṹ���ǿ��Ը��Ƶģ�
�ṹ���ֿ��԰����������͵���Ԫ�أ�����Ҳ�У�
����"����"Ҳ�������ˡ�

������Ϊʲô���������Ͳ��ܸ����أ�
���ǿ�������ȥ���⣺<b>һ�������ܱ����Ƶı�Ҫ������
����֪�����Ĵ�С</b>���ṹ����Ϊ�Զ������ͣ�
�ڱ����ʱ���������Ȼ�洢��������Ԫ�����͡������������Ϣ��
�ṹ��Ĵ�СҲ��֪���ˣ�������һ��ֻ�ں��������ͺ�
��ʼ��ַ��Ԫ�ظ������Ǳ����ӵģ����磺
void func(char s[]) �ɽ����κγ��ȵ��ַ���������������
����Ԫ�ظ���Ҳû�б����������һ���ִ����ڴ棬
��������ĸ����ǲ���ʵ�ֵġ�

## С��

����������ṹ����һ��ʵ�ڵ�Ķ��廰���Ǿ��ǣ�
<b>�и�ʽ���ֽ�����</b>�����˽ṹ��� C ���Ե�
�������;ͷḻ���ˣ�����ͬʱҲҪע�⣺

1. ���� 4 �ֽڵĽṹ�岻�������������������˷�ʱ�䡢�ռ䣩��
����ָ����á�
2. ���� 4 �ֽڵĽṹ�岻��������ֵ����
����˵һ�㷵��ֵ���� eax ���棬
��ô���� 4 �ֽڵ�ʱ����ô���أ��Լ�ȥ̽���ɣ�����

[��Ŀ¼][content]