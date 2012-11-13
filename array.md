[content]: https://github.com/1184893257/simplelinux/blob/master/README.md#content

[��Ŀ¼][content]

<a name="top"></a>

<h1 align="center">�����ָ��
</h1>

����ָ���������ʲô����

����C����array.c����

	#include <stdio.h>
	
	int main()
	{
		int date[3] = {2012,11,11};
		
		int *p = date;
		
		int a = date[1];
		int b = p[1];
		
		printf("a:%d b:%d\n", a, b);
		printf("date:%p\np   :%p\n", date, p);
		return 0;
	}

`����`��༰ע�ͣ�

<table>
<tr><td>
<pre><code>    .file	"array.c"
	.section	.rodata
.LC0:
	.string	"a:%d b:%d\n"
.LC1:
	.string	"date:%p\np   :%p\n"
	.text
.globl main
	.type	main, @function
main:
	pushl	%ebp			#-ָ֡���л�
	movl	%esp, %ebp		#/
	andl	$-16, %esp		#-ջ���뵽16�ֽ�
	subl	$48, %esp		#-���ؾֲ������ռ�
	movl	$2012, 24(%esp)	#\
	movl	$11, 28(%esp)	#-date�����ʼ��
	movl	$11, 32(%esp)	#/
	leal	24(%esp), %eax	#\
	movl	%eax, 44(%esp)	#-��ʼ��ָ��p
	movl	28(%esp), %eax	#\
	movl	%eax, 40(%esp)	#-��ʼ��a
	movl	44(%esp), %eax	#\
	addl	$4, %eax		#-\
	movl	(%eax), %eax	#-��ʼ��b
	movl	%eax, 36(%esp)	#/
</code></pre></td>
<td valign="bottom"><img src="http://fmn.rrfmn.com/fmn059/20121113/1850/original_fmSH_48030000e812125c.jpg" /></td>
</tr>

<tr><td>
<pre><code>    movl    $.LC0, %eax
	movl	36(%esp), %edx
	movl	%edx, 8(%esp)
	movl	40(%esp), %edx
	movl	%edx, 4(%esp)
	movl	%eax, (%esp)
	call	printf		#��һ�ε��� printf ����
</code></pre></td>
<td valign="bottom"><img src="http://fmn.rrimg.com/fmn062/20121113/1850/original_6dpg_28e80000e7fc1191.jpg" /></td>
</tr>

<tr><td>
<pre><code>    movl    $.LC1, %eax
	movl	44(%esp), %edx
	movl	%edx, 8(%esp)
	leal	24(%esp), %edx
	movl	%edx, 4(%esp)
	movl	%eax, (%esp)
	call	printf		#�ڶ��ε��� printf ����
</code></pre></td>
<td valign="bottom"><img src="http://fmn.rrimg.com/fmn056/20121113/1850/original_ECol_44540000c23f1190.jpg" /></td>
</tr>

<tr><td colspan="2">
<pre><code>    movl    $0, %eax    #return 0
	leave
	ret
	.size	main, .-main
	.ident	"GCC: (GNU) 4.5.1 20100924 (Red Hat 4.5.1-4)"
	.section	.note.GNU-stack,"",@progbits
</code></pre></td>
</tr>
</table>

������Ҷ� lea ָ����ܱȽ�İ�������� mov ָ�����
���� lea ָ��ݵ����ڴ�ĵ�ַ���� mov ָ��ݵĵ���
�ڴ��ֵ�����磺

	leal 24(%esp), %eax		# �� 24+esp �Ľ���� eax
	movl 24(%esp), %eax		# �� 2012 �� eax

## �ܽ�

�������ȣ����ǿ��� main Ҳ��һ���������������Ļ�����
��<em>��������</em>�з������� Double ������һ���Ľṹ��

������Σ�ָ�����д洢�ռ�ģ�32λ����4���ֽڵĴ�С����
���д洢����һ���ڴ��ַ��������ֻ�������е�Ԫ���д洢�ռ䣬
�� C �����о����õ����������������������׵�ַ��ʹ�ã�
����˵��û�д洢�ռ�ġ����轫��������ֵ��һ��ָ�룬
�������Ĵ�����ʽ�ǣ�

* �����ȫ�����飬������ mov ָ���е�һ����������������
* ����Ǿֲ����飬������ lea ָ������ esp �� ebp + 
��������Ľ��

`����`<b>����������׵�ַ��һ������ָ��Ĳ�������
���ھֲ������ռ��У�Ҳ����ȫ�ֱ����ռ��У�
���Ǳ��̻��ڴ�����</b>��

����printf �����ĵ��ø���ĺ���һ�����ȴ�������
Ȼ�� call printf����ӡָ�붼����ʹ�� %p ��ʽ��������
��������н�����£�

	[lqy@localhost temp]$ gcc -o array array.c
	[lqy@localhost temp]$ ./array
	a:11 b:11
	date:0xbf9c3b68
	p   :0xbf9c3b68
	[lqy@localhost temp]$ 

`����`date �� p ��ֵ���� date ������׵�ַ��

[��Ŀ¼][content]
