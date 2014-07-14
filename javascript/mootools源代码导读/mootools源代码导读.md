##1.    mootoolsģ��

###1.1.    ģ��ṹ

```
/Source
    |--Browser
        |--Browser.js
    |--Class
        |--Class.js
        |--Class.Extras.js
    |--Core
        |--Core.js
    |--Element
        |--Element.js
        |--Element.Style.js
        |--Element.Dimensions.js
        |--Element.Event.js
        |--Element.Delegation.js
    |--Fx
        |--Fx.js
        |--Fx.CSS.js
        |--Fx.Morph.js
        |--Fx.Transitions.js
        |--Fx.Tween.js
    |--Request
        |--Request.js
        |--Request.HTML.js
        |--Request.JSON.js
    |--Slick
        |--Slick.Finder.js
        |--Slick.Parser.js
    |--Types
        |--Array.js
        |--DOMEvent.js
        |--Function.js
        |--Number.js
        |--Object.js
        |--String.js
    |--Utilities
        |--Cookie.js
        |--DOMReady.js
        |--JSON.js
```

###1.2.    ģ�鹦��

-    Core��    `MooTools`�����һЩͨ�õĺ��������������ģ���ڣ����ԭ����Javascript���󣬱���Function����һЩ��չ�����õ�һЩ��չ��ܶ���ķ������磺`overloadSetter`��`overloadGetter`��`implement`��`extend`�ȶ��������ģ���ﶨ��ġ�
-    Types��    ��չJavascriptԭ������Function Array String Event Number��
-    Browser��    �����UA��̽�Լ�����ϵͳƽ̨���
-    Class��    ������Class���캯����ʵ����Javascript������ϵͳ����`MooTools` ��ܵĻ�����
-    Slick��    CSSѡ�������档
-    Element��    ��չԭ����DOM���ࣺElement�����������µ�api��
-    Fx��    Javascript animation��ʵ�֡�
-    Request��    AJAXʵ�֡�
-    Utilities��    ʵ��һЩͨ�õĹ����࣬����Cookie���ṩ��cookie��д���ܡ�

##2.    mootools����

`MooTools`ѡ��ʹ��`grunt`��Ϊ��Ŀ�������ߣ������е�`grunt`���þ�������`Tests\gruntfile-options.js`��

Javascriptģ��֮���Ȼ���������Ĺ�ϵ��mootoolsͨ��ʹ����`YAML`��ʽ�İ������ļ����㶨������⣬���ǿ����ڸ�Ŀ¼�µ�`package.yml`������Щ������ϵ��

```javascript
sources:
  - "Source/Core/Core.js"
  - "Source/Types/Array.js"
  - "Source/Types/String.js"
  - "Source/Types/Number.js"
  - "Source/Types/Function.js"
  - "Source/Types/Object.js"
  - "Source/Types/DOMEvent.js"
  - "Source/Browser/Browser.js"
  - "Source/Class/Class.js"
  - "Source/Class/Class.Extras.js"
  - "Source/Slick/Slick.Parser.js"
  - "Source/Slick/Slick.Finder.js"
  - "Source/Element/Element.js"
  - "Source/Element/Element.Style.js"
  - "Source/Element/Element.Event.js"
  - "Source/Element/Element.Delegation.js"
  - "Source/Element/Element.Dimensions.js"
  - "Source/Fx/Fx.js"
  - "Source/Fx/Fx.CSS.js"
  - "Source/Fx/Fx.Tween.js"
  - "Source/Fx/Fx.Morph.js"
  - "Source/Fx/Fx.Transitions.js"
  - "Source/Request/Request.js"
  - "Source/Request/Request.HTML.js"
  - "Source/Request/Request.JSON.js"
  - "Source/Utilities/Cookie.js"
  - "Source/Utilities/JSON.js"
  - "Source/Utilities/DOMReady.js"
```

Ĭ������£�`grunt`�������е�JavascriptԴ���룬�������е�Ԫ���ԣ������ֻ��Ҫ�����ѹ��Javascript����ô����Ҫ��`Gruntfile.js`���Զ�������

![grunt default](./grunt_default.png)