# Тестовый вариант использования шаблонизатора ECT.js

В файл **ect.js** сразу добавлен CoffeeScript.

Сайт шаблонизатора - [ectjs.com](http://ectjs.com/)

## Пример использования

### HTML

```html
<div class="wrap">
  <!-- Конейнер для вывода -->
  <div class="js-product row"></div>
</div>

<!-- шаблон -->
<script type="text/template" hidden id="product-preview">

  <% for product in @products : %>
  
  <div class="grid-4">

    <div class="product-preview padded">

      <div class="product-img">
        <img src="<%= product.img %>">
      </div>

      <div class="product-title padded-vertical">
        <%= product.title %>
      </div>

      <div class="product-price row padded-vertical">
        <div class="product-sale grid-6">
          <%= product.price %>
        </div>
        <div class="product-old grid-6">
          <%= product.oldprice %>
        </div>
      </div>
      
      <!-- Eсли заполнен артикул -->
      <% if product.sku.length > 0: %>
      <div class="product-sku">
        Артикул: <%= product.sku %>
      </div>
      <% end %>

      <div class="product-button padded-vertical">
        <!-- Если нет в наличии отключаем кнопку -->
        <% if product.available : %>
        <button class="product-buy">
          Купить
        </button>
        <% else : %>
        <button class="product-buy product-not_available" disabled="disabled">
          Нет в наличии
        </button>
        <% end %>
      </div>

    </div>

  </div>
  
  <% end %>
  
</script>
```

### Js

```js
$(function(){
  //renderer - объект ECT
  //renderer содержит root в котором хранятся id и html шаблонов
  //В нашем случае один шаблон <script type="text/template" hidden id="product-preview">
  var renderer = ECT({ 
    root: {
      preview: $('#product-preview').html()
    }
  });

  //JSON с данными
  $data = {
    products: [
    {
      title: "Товар 1",
      img: "https://placeholdit.imgix.net/~text?txtsize=33&txt=product&w=240&h=240",
      price: "2000 руб",
      oldprice: "25000 руб",
      available: true,
      sku: "123456"
    },
    {
      title: "Товар 2",
      img: "https://placeholdit.imgix.net/~text?txtsize=33&txt=product&w=240&h=240",
      price: "1000 руб",
      oldprice: "30000 руб",
      available: false,
      sku: ""
    },
    {
      title: "Товар 3",
      img: "https://placeholdit.imgix.net/~text?txtsize=33&txt=product&w=240&h=240",
      price: "1500 руб",
      oldprice: "",
      available: true,
      sku: "456789"
    },
    {
      title: "Товар 4",
      img: "https://placeholdit.imgix.net/~text?txtsize=33&txt=product&w=240&h=240",
      price: "2500 руб",
      oldprice: "2000 руб",
      available: true,
      sku: ""
    },
    {
      title: "Товар 5",
      img: "https://placeholdit.imgix.net/~text?txtsize=33&txt=product&w=240&h=240",
      price: "1357 руб",
      oldprice: "6000 руб",
      available: true,
      sku: "456137"
    },
    {
      title: "Товар 6",
      img: "https://placeholdit.imgix.net/~text?txtsize=33&txt=product&w=240&h=240",
      price: "1556 руб",
      oldprice: "3500 руб",
      available: false,
      sku: "124578"
    }
    ]
  };

  //Рендер шаблона в контейнер
  //Берем ранее созданный объект ECT и вызываем в нём метод рендер в который передаём id шаблона и наш JSON с данными
  $('.js-product').html(renderer.render( 'preview', $data ))
});
```

### Результат

```html
<div class="js-product row">
    <div class="grid-4">
        <div class="product-preview padded">
            <div class="product-img">
                <img src="https://placeholdit.imgix.net/~text?txtsize=33&amp;txt=product&amp;w=240&amp;h=240">
            </div>
            <div class="product-title padded-vertical">
                Товар 1
            </div>
            <div class="product-price row padded-vertical">
                <div class="product-sale grid-6">
                    2000 руб</div>
                <div class="product-old grid-6">
                    25000 руб</div>
            </div>
            <!-- Eсли заполнен артикул -->
            <div class="product-sku">
                Артикул: 123456</div>
            <div class="product-button padded-vertical">
                <!-- Если нет в наличии отключаем кнопку -->
                <button class="product-buy">
                    Купить
                </button>
            </div>
        </div>
    </div>
    ...
</div>
```

