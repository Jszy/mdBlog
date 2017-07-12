第二版compile.js
```js
function compile(template) {
        var templateSettings = {
            evaluate: /##([\s\S]+?)##/g,
            interpolate: /\{\{(.+?)\}\}/g,
            escape: /\{\{\{\{-([\s\S]+?)\}\}\}\}/g
        };
        template = template
            .replace(templateSettings.escape, '`); \n  echo( escape($1) ); \n  echo(`')
            .replace(templateSettings.interpolate, '`); \n  echo( $1 ); \n  echo(`')
            .replace(templateSettings.evaluate, '`); \n $1 \n  echo(`');
        template = 'echo(`' + template + '`);';
        var script =
            `obj || (obj = {});
                var __p = "",
                    __j = Array.prototype.join;
                var htmlEscapes = {
                  '&': '&amp;',
                  '<': '&lt;',
                  '>': '&gt;',
                  '"': '&quot;',
                  "'": '&#39;'
                };
                var reUnescapedHtml = RegExp('[' + __keys(htmlEscapes).join('') + ']', 'g');
                function escape(string) {
                  return string == null ? '' : String(string).replace(reUnescapedHtml, escapeHtmlChar);
                }
                function __keys(object) {
                  object || (object = {});
                  var result = [];
                  for(var key in object){
                    result.push(key);
                  }
                  return result;
                }
                function escapeHtmlChar(match) {
                  return htmlEscapes[match];
                }
                function echo(html){
                  __p += __j.call( arguments,'');
                }
                with(obj){
                  ${ template }
                }
                return __p;
            `;
        return Function('obj',script);
    }
```
```js
function compile(template) {
        var templateSettings = {
            evaluate: /##([\s\S]+?)##/g,
            interpolate: /\{\{(.+?)\}\}/g,
            escape: /\{\{\{\{-([\s\S]+?)\}\}\}\}/g
        };
        template = template
        	.replace(templateSettings.escape, '`); \n  echo( escape($1) ); \n  echo(`')
            .replace(templateSettings.interpolate, '`); \n  echo( $1 ); \n  echo(`')
            .replace(templateSettings.evaluate, '`); \n $1 \n  echo(`');
        template = 'echo(`' + template + '`);';
        var script =
            `(function (obj){
			    obj || (obj = {});
			    var __p = "",
			        __j = Array.prototype.join;
			    var htmlEscapes = {
			      '&': '&amp;',
			      '<': '&lt;',
			      '>': '&gt;',
			      '"': '&quot;',
			      "'": '&#39;'
			    };
			    var reUnescapedHtml = RegExp('[' + __keys(htmlEscapes).join('') + ']', 'g');
			    function escape(string) {
			      return string == null ? '' : String(string).replace(reUnescapedHtml, escapeHtmlChar);
			    }
			    function __keys(object) {
			      object || (object = {});
			      var result = [];
				  for(var key in object){
					result.push(key);
				  }
			      return result;
			    }
			    function escapeHtmlChar(match) {
			      return htmlEscapes[match];
			    }
			    function echo(html){
			      __p += __j.call( arguments,'');
			    }
			    with(obj){
			      ${ template }
			    }
			    return __p;
			})`;
        return eval(script);
    }
```
调用方式
```js
let template = `
  ##for(var i=0;i<list.length;i++){##
  <span>{{list[i].name}}</span>  
  ##}##
`;
var templateFn = compile( template );
$('body').append( templateFn({
  list: [{name: 'jack'}, {name: 'tom'}, {name: '<script>alert(0)<\/script>'}]
}) )
```
