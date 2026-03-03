Базовые классы
.material-input — основной контейнер
.material-input .label — плавающая метка
.material-helper — вспомогательный текст

Варианты полей
.material-input.filled — заполненное поле
.material-input.outlined — контурное поле

Структура HTML
<div class="material-input filled" id="any-id">
    <span class="label">текст метки</span>
    <input type="text" id="input-id">
</div>
<div class="material-helper">подсказка</div>

<div class="material-input outlined" id="any-id">
    <span class="label">текст метки</span>
    <input type="text" id="input-id">
</div>
<div class="material-helper">подсказка</div>

Состояния (добавляются автоматически)
.focused — поле в фокусе
.has-value — поле содержит текст
.disabled — отключенное поле (добавляется вручную)

Автоматическая инициализация
При загрузке страницы скрипт сам находит все .material-input
и добавляет обработчики для классов .focused / .has-value

Ручная инициализация
initMaterialInput('id_контейнера') — для отдельного поля

Кастомизация через CSS-переменные
можно переопределять стили через обычный CSS:
.material-input.filled {
    background: ваш цвет;
}
.material-input.filled::after {
    background: цвет бордера;
}
.material-input.filled.focused::after {
    background: цвет фокуса;
}
.material-input.outlined::before {
    border-color: цвет контура;
    border-width: толщина;
}
.material-input.outlined.focused::before {
    border-color: цвет фокуса;
}
.material-input .label {
    color: цвет метки;
}

Внутренние псевдоэлементы
.filled::after — нижняя граница (плавная смена цвета и высоты)
.outlined::before — рамка (плавная смена цвета)

JavaScript API
window.initMaterialInput(id) — принудительная инициализация
                                (если поле добавили динамически)

Совместимость
работает со всеми браузерами где есть css transition
и ES6 (можно транспилировать если надо совсем старье)

Размеры по умолчанию
высота: 56px
отступы: padding: 18px 12px 0
радиус filled: 4px 4px 0 0
радиус outlined: 4px
толщина бордера в фокусе: 2px

Цвета по умолчанию
фон filled: #e9e6ed
бордер filled: #7e7a86
фокус filled: #6750a4
метка: #5e5a66
бордер outlined: #7e7a86
фокус outlined: #6750a4

Пример динамического создания
let div = document.createElement('div');
div.className = 'material-input filled';
div.innerHTML = '<span class="label">новая метка</span><input type="text">';
document.body.appendChild(div);
initMaterialInput(div.id); // если задали id
// или скрипт сам подхватит если добавить до DOMContentLoaded
// либо можно вызвать для всех новых полей вручную

Особенности outlined
рамка сделана через ::before чтобы не двигать контент
при фокусе меняется только цвет, толщина не меняется
(толщина всегда 2px в фокусе, задается через border-width)

Особенности filled
нижняя граница сделана через ::after чтобы не двигать
соседние элементы при утолщении с 1px до 2px
фон меняется плавно, цвет границы тоже
