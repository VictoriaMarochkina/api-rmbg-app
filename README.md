## API для удаления фона с изображений (BRIA RMBG-1.4 + FastAPI)

REST API-сервис на FastAPI для удаления фона с изображений с помощью модели  
[BRIA RMBG-1.4](https://huggingface.co/briaai/RMBG-1.4) из библиотеки Transformers.

В сервисе реализованы два эндпоинта:

- `POST /remove-background` — возвращает изображение **без фона** (PNG)
    Тело запроса: multipart/form-data с полем file — изображение (jpg, jpeg, png, webp)
Ответ: image/png — изображение без фона (PNG), отдаётся как файл result.png.

Пример (`curl`):

```bash
  curl -X POST "http://localhost:8000/remove-background" \
  -H "accept: image/png" \
  -H "Content-Type: multipart/form-data" \
  -F "file=@/полный/путь/к/photo.jpg" \
  --output result.png
```
- `POST /get-mask` — возвращает **маску сегментации** (PNG) Тело запроса: multipart/form-data с полем file — изображение (jpg, jpeg, png, webp) Ответ: image/png — маска сегментации (PNG), отдаётся как файл mask.png.

Пример (`curl`):

```bash
  curl -X POST "http://localhost:8000/get-mask" \
  -H "accept: image/png" \
  -H "Content-Type: multipart/form-data" \
  -F "file=@/полный/путь/к/photo.jpg" \
  --output mask.png
```

Изображения передаются как файлы (`multipart/form-data`) через `UploadFile`.


