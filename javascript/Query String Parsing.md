##1.    URL encoding

ΪʲôҪ����URL encoding��������Ϊ����Щ�ַ��ǲ��ܳ�ΪURLһ���ֵģ��ٸ����ӣ�����ո�������⣬��Щ�����⺬��ı����ַ�������#����ΪHTMLê�㣬���ڶ�λ��HTML�ĵ���ĳ��λ���ϣ�=������URL�����ڷָ�URL������key��value��

URL encoding�������¹���

-    ��ĸ��A�CZ �Լ� a�Cz�������֣�0-9���Լ�'.'��'-'��'~'��'_'��Щ�ַ������б���
-    �ո��Ҫ�����+����"%20"
-    �����������ַ���Ҫ�������%HH������ʽ��[ʮ������](http://en.wikipedia.org/wiki/Hexadecimal)��ʾ���κη�ASCII�ַ���Ӧ��ҪȡUTF-8��ʮ�����ƣ��������������룩����%HH��ʾ��

>NOTE:  ������ϸ��Ϣ�����Բο���ƪWIKI����[Query String](http://en.wikipedia.org/wiki/Query_string)�����ڿո���Լ������ı����ַ�������ȥ���ı�׼�ĵ�[RFC 1738](http://tools.ietf.org/html/rfc1738)��

##2.    Javascript Encode/Decode Functions

Javascript�����˼��Ա���ͽ���ĺ��������ֻ��`escape`��`unescape`��һ�Է�������������Է����Ѿ����Ƽ�ʹ���ˣ��µı�׼�ƶ��������µı���ͽ��뺯����`encodeURI` �� `decodeURI` �Լ� `encodeURIComponent` �� `decodeURIComponent`��

��ʵ�������õı�����뺯��������URL query string�ı���ͽ���ȴ����ʮ����ȷ�ġ�

����                         | ���             | ˵��               |
----------------------------|-----------------|--------------------|
"A + B"                     | "A+%2B+B"       | ����ֵ              |
escape("A + B")             | "A%20+%20B"     | ����               |    
encodeURI("A + B")          | "A%20+%20B"     | ����               |
encodeURIComponent("A + B") | "A%20%2B%20B"   | ���Խ��ܣ������е���� |

����                           | ���           | ˵��               |
------------------------------|---------------|--------------------|
"A+%2B+B"                     | "A + B"       | ����ֵ              |
unescape("A+%2B+B")           | "A+++B"       | ����               |    
decodeURI("A+%2B+B")          | "A+%2B+B"     | ����               |
decodeURIComponent("A+%2B+B") | "A+++B"       | ����               |


>NOTE:SEE ALSO:[Javascript Madness: Query String Parsing](http://unixpapa.com/js/querystring.html)