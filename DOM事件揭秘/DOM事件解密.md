1���¼��� ҳ���н����¼���˳��
a)ð��
b)����
2�����/ɾ���¼��������
a)HTML�¼��������
<input type="button" value="��ť" onclick="showMessage()">
i.ȱ�㣺html��js���
b)DOM0���¼���������Ȼ�ȡԪ�أ������¼���Ԫ�����Ե���ʽ���ֲ���ֵ��һ��������
		var btn=document.getElementById("btn");
		btn.onclick=function(){}
//btn.onclick=null;
i.�ŵ㣺������� ��һ��Ԫ����Ӷ���¼��������
ii.��ֵΪnull��Ϊ����¼��������
c)DOM2���¼�������� addEventListener removeEventListener
		btn.addEventListener('click',handler,false);
btn.removeEventListener('click',handler,false);
i.������false��ð�ݽ׶Σ�true�ǲ���׶Ρ�
ii.�ŵ㣺��һ��Ԫ����Ӷ���¼��������
iii.ע�⣺ͨ��addEventListener��ӵ��¼�ֻ����removeEventListenerɾ����
d)IE�¼�������� 
btn.attachEvent("onclick",handler);
		btn.detachEvent("onclick",handler);
3���¼����� event
a)DOM���¼�����
i.type �¼�����
ii.target �¼�Ŀ��
iii.stopPropagation()���� ��ֹ�¼�ð��
iv.preventDefault()���� ��ֹĬ����Ϊ
b)IE���¼�����
i.type
ii.srcElement
iii.cancelBubble����
iv.returnValue����
4������������������DOM2-->IE-->DOM0��
a)ע�⣺
i.element['on'+type]=handler;
ii.�����жϵ�ʱ��д�����Ե���ʽ��
iii.IE8����window.event
var eventUtil = {
	addHandler: function(element, type, handler) {
		if (element.addEventListener) {
			element.addEventListener(type, handler, false);
		} else if (element.attachEvent) {
			element.attachEvent('on' + type, handler);
		} else {
			element['on' + type] = handler;
		}
	},
	removeHandler: function(element, type, handler) {
		if (element.removeEventListener) {
			element.removeEventListener(type, handler, false);
		} else if (element.detachEvent) {
			element.detachEvent('on' + type, handler);
		} else {
			element['on' + type] = null;
		}
	},
	getEvent: function(event) {
		return event ? event : window.event;
	},
	getType: function(event) {
		return event.type;
	},
	getElement: function(event) {
		return event.target || event.srcElement;
	},
	preventDefault: function(event) {
		if (event.preventDefault) {
			event.preventDefault();
		} else {
			event.returnValue = false;
		}
	},
	stopPropagation: function(event) {
		if (event.stopPropagation) {
			event.stopPropagation();
		} else {
			event.cancelBubble = true;
		}
	}
}
5���¼�����
a)QQ�����קЧ��&�齱ϵͳ

1����һ��Ԫ����Ӷ���¼�������򣬸�������Ĵ���˳��
2��֧��IE�¼����������������IE��OPERA?
3����ϰ���js���������
4���¼��ڲ����б��п���д��event��