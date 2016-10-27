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

#### Fetch API
##### Type GET
```javascript
  fetch('/rests/admin/news/tag/list/')
      .then(function(response) {
        // typeof response === 'object'
        return response;
      }).then(function(body) {
        console.log('\nbody', body);
      }).catch(function(err) {
        console.log('\nparsing failed', err);
      });
```

##### Type POST
```javascript
  fetch(url, {
      method: 'post',
      body: JSON.stringify(fields),
      credentials: 'include', // important
      // headers: {
      //  'Accept': 'application/json',
      //  'Content-Type': 'application/json'
      // },
    }).then(function(response) {
      return response.json();
    }).then(function(data) {
      console.log('result ->', data.result);
    }).catch(function(err) {
      console.log('err ->', err);
    });
```

#### polyfill
https://github.com/github/fetch

bower
>$ bower install fetch
>$ bower install es6-promise

npm
>$ npm install whatwg-fetch --save