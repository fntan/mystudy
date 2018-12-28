```javascript
window.ajax = async function (params, callback) {
    let url = params.url;
    let method = params.method;
    let data = params.data;
    let body = new FormData();
    for (let key in data) {
        if (data.hasOwnProperty(key)) {
            body.append(key, data[key]);
        }
    }
    let xhr = new XMLHttpRequest();
    xhr.timeout = 3000;
    xhr.open(method, url, true);
    xhr.addEventListener("readystatechange", evt => {
        if (xhr.readyState === 4) {
            if (xhr.status === 200) {
                callback(xhr.response);
            } else {
                throw xhr.statusText;
            }
        }
    });
    xhr.send(body);
};
```

