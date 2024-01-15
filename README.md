# hover-slider
js
***
```
let hover = document.querySelectorAll('[data-hover-img]');
hover.forEach((el) => {
    el.addEventListener('mouseenter', (e) => {
        e.preventDefault();
        el.classList.add('active');
        let img = el.getAttribute('data-hover-img');
        let bg = el.parentElement.querySelector(".bg");
        bg.style.backgroundImage = "url("+img+")";
    });
    el.addEventListener('mouseleave', (e) => {
        el.classList.remove('active');
    });
    // Свайп влево вправо для мобилк
    
    let startX = 0;
    let endX = 0;
    
    el.addEventListener('touchstart', (e) => {
        startX = e.touches[0].clientX;
    });
    
    el.addEventListener('touchmove', (e) => {
        endX = e.touches[0].clientX;
    });
    
    el.addEventListener('touchend', () => {
        const diff = startX - endX;
        let items = el.parentElement;
        let bg = items.querySelector(".bg");
        if (Math.abs(diff) > 50) { 
            if (diff > 0) {
            // свайп влево, переключить на следующее изображение
                if(items.querySelector('.active')){
                    let item = items.querySelector('.active').nextElementSibling;
                    let img = item.getAttribute('data-hover-img');
                    if(img){
                        item.previousElementSibling.classList.remove('active');
                        item.classList.add('active');
                        bg.style.backgroundImage = "url("+img+")";
                    }
                } else {
                    let item = items.firstElementChild.nextElementSibling;
                    let img = item.getAttribute('data-hover-img'); 
                    item.classList.add('active');
                    bg.style.backgroundImage = "url("+img+")";
                }
            } else {
            // свайп вправо, переключить на предыдущее изображение
                if(items.querySelector('.active')){
                    let item = items.querySelector('.active').previousElementSibling;
                    let img = item.getAttribute('data-hover-img');
                    if(img){
                        item.nextElementSibling.classList.remove('active');
                        item.classList.add('active');
                        bg.style.backgroundImage = "url("+img+")";
                    }
                } else {
                    items.firstElementChild.classList.add('active');
                }
            }
        }
    });
});
```
html\php 
***
```
<div class="b-catalog-table__slider-wrapper">
    <ul class="b-catalog-table__slider">
        <?if ($item['MORE_PHOTO_COUNT'] > 1){?>
            <?foreach($item['MORE_PHOTO'] as $img){?>
            <li class="b-catalog-table__slider--slide" data-hover-img="<?=$img['SRC']?>"><span></span></li>
            <?}?>
        <?}?>
        <li class="img-empty"></li>
        <li class="b-catalog-table__slider--bg bg" style="display: list-item; background-image: url(<?=$img_bg?>);"></li>
        <li class="b-catalog-table__slider--mark"></li>
    </ul>
</div>
```
