* ***html(canvas)转图片(base64)、PDF***

  * ***HTML转canvas:*** [ html2canvas.js ](https://html2canvas.hertzen.com/)

  * ***canvas转base64:***

    ```javascript
    var imgData = canvas.toDataURL("image/jpeg");
    ```

  * **canvas转PDF:**  [ jspdf.js ](https://parall.ax/products/jspdf)

    * https://www.cnblogs.com/wei-dong/p/8193554.html

* **页面滚动显示动画**

  * scrollreveal.js

    ```javascript
            window.sr = ScrollReveal({
                distance: '80px',
                duration: 1000,
                delay: 200,
                scale: 1,
                easing: 'ease'
            });
            sr.reveal('.animation');
            sr.reveal('.animation-delay', {
                delay: 400
            });
            sr.reveal('.activ-rule li', 200);
    ```
