# L2. Короткая справка

[Задание](../README.md) · [Гайд](GUIDE.md) · [Интерактив](interactive.html) · [Слайды](slides-standalone/slides.html)

Кодовый пример использует книги. A2 показывает задания одного учебного модуля из A1.

## Зачем и термины

- компонент — функция JSX;
- props — вход компонента;
- тип props — контракт входных значений, который проверяет TypeScript;
- state — изменяемые данные, запускающие новый рендер;
- `key` — идентификатор для сопоставления элементов списка React;
- Vite — dev-сервер и сборщик;
- mount — подключение React к DOM-элементу.

## Подключение к существующему проекту

Не запускайте генератор поверх `trainer/`: продолжайте проект L1.

```sh
npm install react@19.3.0 react-dom@19.3.0 --save-exact
npm install vite@6.4.3 @vitejs/plugin-react@4.3.4 @types/react@19.3.0 @types/react-dom@19.3.0 --save-dev --save-exact
npm pkg set "scripts.dev=vite" "scripts.build=tsc --noEmit && vite build" "scripts.preview=vite preview"
```

Команды одинаковы в Linux и Windows PowerShell. Конфиги `tsconfig`, `vite.config.ts`, `index.html` и mount-фрагмент находятся в [гайде](GUIDE.md).

Для работы с исходниками запустите `npm run dev`. Для проверки готового результата выполните `npm run check`, `npm run build`, затем `npm run preview`: последний режим показывает файлы из `dist/`, а `dev` — текущие исходники.

До L6 `npm test` не обязателен: Vitest и RTL подключаются позже.

## Props и список книг

```tsx
type BookRowProps = {
  isbn: string;
  title: string;
  onChoose: (isbn: string) => void;
};

function BookRow({ isbn, title, onChoose }: BookRowProps) {
  return <button onClick={() => onChoose(isbn)}>{title}</button>;
}

{books.map((book) => (
  <BookRow key={book.isbn} isbn={book.isbn} title={book.title} onChoose={onChoose} />
))}
```

Используйте id сущности в `key`, не индекс. `key` не является выбранным id или обычным prop строки. Дочерний компонент сообщает о выборе callback-ом.

## Формы данных

Проверяйте различающее поле union до чтения специальных полей. Бумажная книга имеет `pages`, аудиокнига — `duration`; аналогичная граница нужна между двумя формами задания A1. Необязательное `code` показывайте как текст только при его наличии.

## State

Храните только идентификатор выбранной сущности. На каждом рендере предусмотрите состояние «ничего не выбрано» и не дублируйте весь объект в state. A2 не включает каталог нескольких модулей, ввод ответов, HTTP, генерацию варианта и сохранение. Каталог возможен как дополнительная задача после основной логики курса.
