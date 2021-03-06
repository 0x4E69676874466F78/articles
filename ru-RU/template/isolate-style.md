# Изоляция стилей

Изоляция стилей решает проблему конфликта имен CSS-классов путем добавления к этим именам префиксов, которые обычно генерируются случайным образом. Это позволяет использовать одинаковые имена классов в разметке разных компонентов, гарантируя отсутствие конфликтов в рамках всего приложения. Более подробно об изоляции стилей в докладе [Жизнь в изоляции](http://www.slideshare.net/basisjs/ss-48417378/).

Способы изоляции:

- [&lt;b:isolate/&gt;](#bisolate) – изоляция всей разметки и стилей шаблона
- [&lt;b:style ns/&gt;](#bstyle-ns) – изоляция конкретного файла стилей
- [&lt;b:include isolate/&gt;](#binclude-isolate) – изоляция включаемого фрагмента разметки и его стилей

## &lt;b:isolate/&gt;

Изоляция всей разметки и стилей шаблона. Применяется к финальной разметке шаблона, то есть после обработки всех включений и подключения всех стилей. Не наследуется, то есть действует только для самого шаблона.

Например, в результате обработки шаблона:

```html
<b:isolate/>
<b:style>
  .some-class {
    color: red;
  }
</b:style>

<div class="some-class">Компонент</div>
```

Разметка примет вид:

```css
.i1__some-class {
  color: red;
}
```

```html
<div class="i1__some-class">Компонент</div>
```

Подробнее в описании [&lt;b:isolate&gt;](b-isolate.md)

## &lt;b:style ns/&gt;

Изоляция подключаемого файла стилей. В этом случае обращение к именам классов файла осуществляется с указанием заданного пространства имен.

```html
<b:style ns="foo"/>

<div class="example foo:example"/>
```

Подробнее в описании [&lt;b:style&gt;](b-style.md#Изоляция-стилей)

## &lt;b:include isolate/&gt;

Если требуется изолировать включаемый фрагмент (шаблон), то используется атрибут `isolate`. При этом изоляция применяется только к разметке и стилям включаемого фрагмента.

```html
<b:style>
  .foo {
    color: red;
  }
</b:style>

<div class="foo">
  <b:include src="./foo.tmpl" isolate/>
</div>
```

`foo.tmpl`:

```html
<b:style>
  .foo {
    color: green;
  }
</b:style>

<div class="foo"/>
```

Результат:

```html
<b:style>
  .foo {
    color: red;
  }
  .xh7jokjfx7jo2ccq__foo {
    color: green;
  }
</b:style>

<div class="foo">
  <div class="xh7jokjfx7jo2ccq__foo"/>
</div>
```

Подробнее в описании [&lt;b:include&gt;](b-include.md#Изоляция-стилей)
