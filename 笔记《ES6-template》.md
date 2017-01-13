```js
function compile(template){
  var templateSettings = {
    evaluate: /##([\s\S]+?)##/g,
    interpolate: /\{\{(.+?)\}\}/g,
    escape: /\{\{\{\{-([\s\S]+?)\}\}\}\}/g
  };
  /**
  var interpolate = /<%=(.+?)%>/g;
  var evaluate = /<%([\s\S]+?)%>/g;
  */

  template = template
    .replace(templateSettings.interpolate, '`); \n  echo( $1 ); \n  echo(`')
    .replace(templateSettings.evaluate, '`); \n $1 \n  echo(`');

  template = 'echo(`' + template + '`);';

  var script =
  `(function parse(data){
    var output = "";

    function echo(html){
      output += html;
    }

    ${ template }

    return output;
  })`;

  return script;
}
```
调用
```js
var parse = eval(compile(template));
div.innerHTML = parse({ supplies: [ "broom", "mop", "cleaner" ] });
```
