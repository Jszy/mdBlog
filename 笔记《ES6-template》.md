function compile(template){
  var templateSettings = {
    evaluate: /##([\s\S]+?)##/g,
    interpolate: /\{\{(.+?)\}\}/g,
    escape: /\{\{\{\{-([\s\S]+?)\}\}\}\}/g
  };
  template = template
    .replace(templateSettings.interpolate, '`); \n  echo( $1 ); \n  echo(`')
    .replace(templateSettings.evaluate, '`); \n $1 \n  echo(`');
  template = 'echo(`' + template + '`);';
  var script =
  `(function (obj){
    obj || (obj = {});
    var __p = "",
        __j = Array.prototype.join;
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
