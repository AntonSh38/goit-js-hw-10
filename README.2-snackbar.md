📖 Частина 1: Підготовка інструментів javascriptimport iziToast from 'izitoast';
import 'izitoast/dist/css/iziToast.min.css'; 🎒 Що відбувається: Ми "запрошуємо
гостей на вечірку"

Перший рядок: запрошуємо бібліотеку iziToast (вона вміє показувати красиві
повідомлення) Другий рядок: запрошуємо її "одяг" (стилі), щоб повідомлення були
гарними

Частина 2: Знаходимо форму javascriptconst formEl =
document.querySelector('.form'); 🔍 Що відбувається: Ми шукаємо форму на
сторінці

document - це вся HTML сторінка querySelector('.form') - знайди елемент з класом
"form" formEl - зберігаємо знайдену форму в змінну (як у коробку)

Частина 3: Ставимо "слухача" javascriptformEl.addEventListener('submit',
onFormSubmit); 👂 Що відбувається: Ставимо "охоронця" біля форми

addEventListener - це як поставити охоронця 'submit' - охоронець чекає, коли
натиснуть кнопку submit onFormSubmit - коли це станеться, викликай цю функцію

Частина 4: Головна функція (коли натиснули кнопку) javascriptfunction
onFormSubmit(event) { 🎬 Початок дії: Ця функція запускається, коли користувач
натискає кнопку javascriptevent.preventDefault(); 🛑 Зупиняємо: Кажемо браузеру
"Стоп! Не роби те, що робиш зазвичай з формою!"

Зазвичай форма перезавантажує сторінку, але нам цього не треба

Частина 5: Збираємо дані з форми javascriptconst delayInput =
document.querySelector('input[name="delay"]'); const delayValue =
delayInput.value; 📝 Читаємо затримку:

Рядок 1: знаходимо поле, де користувач ввів кількість мілісекунд Рядок 2:
дістаємо те, що він написав (це буде текст, наприклад "2000")

javascriptconst selectedRadio =
document.querySelector('input[name="state"]:checked'); const stateValue =
selectedRadio.value; 🔘 Читаємо вибір:

Рядок 1: знаходимо, яку радіокнопку вибрав користувач (:checked означає
"вибрану") Рядок 2: дістаємо значення ("fulfilled" або "rejected")

javascriptconst delay = Number(delayValue); 🔢 Перетворюємо в число:

delayValue був текстом "2000" Number() перетворює його в справжнє число 2000

Частина 6: Створюємо проміс (обіцянку) javascriptconst promise = new
Promise((resolve, reject) => { 🤝 Даємо обіцянку: "Я обіцяю, що через якийсь час
щось зроблю!"

resolve - функція для виконання обіцянки reject - функція для відмови від
обіцянки

javascriptsetTimeout(() => { ⏰ Ставимо таймер: "Зачекай стільки мілісекунд,
скільки сказав користувач" javascriptif (stateValue === 'fulfilled') {
resolve(delay); } else { reject(delay); } 🤔 Приймаємо рішення:

Якщо користувач вибрав "fulfilled" → виконуємо обіцянку (resolve) Якщо вибрав
"rejected" → відмовляємося від обіцянки (reject) В обох випадках передаємо
кількість мілісекунд

javascript}, delay); ⏱️ Закриваємо таймер: Вся ця перевірка відбудеться через
delay мілісекунд

Частина 7: Обробляємо результат обіцянки javascriptpromise.then(delay => { ✅
Якщо обіцянка виконалася: Цей код спрацює, якщо викликався resolve()
javascriptiziToast.success({ title: 'Ok', message:
`✅ Fulfilled promise in ${delay}ms`, }); 🎉 Показуємо зелене повідомлення:
"Ура! Обіцянка виконана!" javascript.catch(delay => { ❌ Якщо обіцянка не
виконалася: Цей код спрацює, якщо викликався reject() javascriptiziToast.error({
title: 'Error', message: `❌ Rejected promise in ${delay}ms`, }); 🔴 Показуємо
червоне повідомлення: "Ой! Обіцянка не виконана!"

Як це працює разом:

👆 Користувач вводить "3000" і вибирає "Fulfilled" ⏰ Запускається таймер на 3
секунди 🤝 Проміс чекає... ✅ Через 3 секунди проміс виконується 🎉 З'являється
зелене повідомлення "Fulfilled promise in 3000ms"
