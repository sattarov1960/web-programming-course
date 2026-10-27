# L3. Короткая справка

[Задание](../README.md) · [Гайд](GUIDE.md) · [Справка](CHEATSHEET.md) · [Интерактив](interactive.html) · [Слайды](slides-standalone/slides.html)

## Контролируемое поле

```tsx
const [value, setValue] = useState("");

<input
  value={value}
  onChange={(event) => setValue(event.target.value)}
/>
```

Для radio используются `checked` и `onChange`:

```tsx
<input
  type="radio"
  checked={selectedId === optionId}
  onChange={() => setSelectedId(optionId)}
/>
```

Для textarea — `value` и `onChange` с текстом события:

```tsx
<textarea
  value={text}
  onChange={(event) => setText(event.target.value)}
/>
```

## Неизменяемые обновления

```ts
const nextObject = { ...object, value: nextValue };
const nextItems = items.map((item) =>
  item.id === targetId ? { ...item, value: nextValue } : item,
);
const withoutItem = items.filter((item) => item.id !== targetId);
```

Не изменяйте массив или объект состояния через `push` и присваивание. В A3 ответ связывается с `Task.id`, а точное представление коллекции и операция обновления остаются частью самостоятельной реализации.

## Производные значения

```ts
const isFilledText = (value: string) => value.trim().length > 0;
const progress = `${answeredCount} из ${taskCount}`;
```

Прогресс и список пропущенных заданий вычисляйте из исходных данных. Не поддерживайте отдельный счётчик, который может разойтись с ответами.

## Срок жизни состояния

Состояние поля переживает повторный render его владельца, но заканчивается при размонтировании владельца. Данные, которые нужны полю, навигации и обзору, должны иметь общего владельца с подходящим сроком жизни.

## Контроль перед сдачей

- radio и textarea получают значение из состояния React;
- ответ соответствует `Task.id`, а не позиции задания;
- переходы не стирают ответы;
- прогресс и пропуски пересчитываются из исходных данных;
- отмена предупреждения не закрывает попытку и не очищает ответы;
- `submitted` блокирует редактирование до явного старта новой попытки;
- нет API, `fetch`, серверной оценки, `localStorage` и `sessionStorage`.
