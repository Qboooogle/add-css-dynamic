# add-css-dynamic
通过js动态改变css属性
>*
 >* 动态添加 CSS 样式
 >* @param selector {string} 选择器
 >* @param rules    {string} CSS样式规则
 >* @param index    {number} 插入规则的位置, 靠后的规则会覆盖靠前的
 >*
 
<pre>
var addCssRule = function() {
	// 创建一个 style， 返回其 stylesheet 对象
	// 注意：IE6/7/8中使用 style.stylesheet，其它浏览器 style.sheet
	function createStyleSheet() {
		var head = document.head || document.getElementsByTagName('head')[0];
		var style = document.createElement('style');
		style.type = 'text/css';
		head.appendChild(style);
		console.dir(style)
		return style.sheet ||style.styleSheet;
	}
	// 创建 stylesheet 对象
	var sheet = createStyleSheet();
	// 返回接口函数
	return function(selector, rules, index) {
		index = index || 0;
	    if (sheet.insertRule) {
	        sheet.insertRule(selector + "{" + rules + "}", index);
	    } else if (sheet.addRule) {
	        sheet.addRule(selector, rules, index);
	    }
	}
}();
addCssRule('p', 'color:red;border:3px solid gray;');
addCssRule('#mydiv', 'color:yellow;border:7px solid gray;');
</pre>
