# Fetch API

>Fetch API предоставляет интерфейс для получения ресурсов (файлов и любых други данных, например, по сети). Это покажется знакомым любому, кто использовал XMLHttpRequest, но новое API является более мощным и гибким набором функций.

- developer.mozilla.org

#### slide 01

#### XMLHttpRequest
```javascript
function request(type, url, opts, callback) {
  var xhr = new XMLHttpRequest();
  var fd;

  if (typeof opts === 'function') {
    callback = opts;
    opts = null;
  }

  xhr.open(type, url);

  if (type === 'POST' && opts) {
    fd = new FormData();

    for (var key in opts) {
      fd.append(key, JSON.stringify(opts[key]));
    }
  }

  xhr.onload = function () {
    callback(JSON.parse(xhr.response));
  };

  xhr.send(opts ? fd : null);
}
```

#### $.ajax
```javascript
$.ajax({
        type: 'POST',
        url: 'url',
        dataType: 'json',
        cache: false,
        data: data,
        success: function(data) {
          callback({
            data: data,
            cb: callback()
            ...
               ...
                  ...
                     callback()
            });
        }
      });
```

#### $.ajax +
```javascript
function request(urls, callback, type, extra) {
    var obj_;
    var type_ = type; // String
    var params_ = extra; // {}

    obj_ = obj_ || {};
    type_ = type_ || 'GET';

    obj_ = {
        url: urls,
        type: type_,
        success: function(data) {
          if (callback) callback(data.result);
        }
    };

    if (params_) obj_.data = params_;

    $.ajax(obj_);
};
```
