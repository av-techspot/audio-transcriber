# Audio Transcriber

Простой и быстрый транскрибатор аудио в текст с таймкодами на Python. Экспорт только в DOCX формат.

## Возможности

- 🎵 Поддержка популярных аудио форматов (MP3, WAV, M4A, FLAC и др.)
- ⏱️ Таймкоды для каждого сегмента речи
- 📄 Экспорт в DOCX с форматированием
- 🚀 Быстрая работа с моделями Whisper разных размеров
- 💻 Работает на Windows, Linux, macOS

## Установка

### 1. Клонирование репозитория
```bash
git clone https://github.com/yourusername/audio-transcriber.git
cd audio-transcriber
```

### 2. Установка Python зависимостей
```bash
pip install -r requirements.txt
```

### 3. Установка PyTorch (Windows)
```bash
# CPU версия
pip install torch --index-url https://download.pytorch.org/whl/cpu

# CUDA версия (если есть NVIDIA GPU)
pip install torch --index-url https://download.pytorch.org/whl/cu121
```

### 4. Установка FFmpeg

**Windows:**
```bash
# Через Chocolatey
choco install ffmpeg

# Или скачать вручную с https://ffmpeg.org/download.html
# и добавить в PATH
```

**Linux:**
```bash
sudo apt update
sudo apt install ffmpeg
```

**macOS:**
```bash
brew install ffmpeg
```

## Использование

### Базовое использование
```bash
python transcribe.py audio.mp3
```
Создаст файл `audio.docx` с транскрипцией.

### Указание выходного файла
```bash
python transcribe.py input.wav output.docx
```

### Выбор модели Whisper
```bash
python transcribe.py audio.mp3 --model base
```
Доступные модели: `tiny`, `base`, `small`, `medium`, `large`

### Использование локальных моделей
```bash
# Скачайте модель вручную и укажите папку
python transcribe.py audio.mp3 --models-dir "C:\whisper-models"
```

### Указание пути к FFmpeg (если не в PATH)
```bash
python transcribe.py audio.mp3 --ffmpeg "C:\ffmpeg\bin\ffmpeg.exe"
```

### Все параметры
```bash
python transcribe.py audio.mp3 output.docx --model small --models-dir "C:\models" --ffmpeg "C:\ffmpeg\bin\ffmpeg.exe"
```

## Формат вывода

DOCX файл содержит:
- Заголовок с именем аудио файла
- Параграфы с таймкодами в формате `[HH:MM:SS - HH:MM:SS] текст`

Пример:
```
[00:00:00 - 00:00:03] Привет, это тестовая запись.
[00:00:03 - 00:00:07] Whisper отлично работает с русским языком.
```

## Требования

- Python 3.8+
- FFmpeg
- 4+ GB RAM (для модели small)
- 2+ GB свободного места (для моделей)

## Модели Whisper

| Модель  | Размер | Скорость | Качество | RAM |
|---------|--------|----------|----------|-----|
| tiny    | 39 MB  | Очень быстро | Низкое | 1 GB |
| base    | 74 MB  | Быстро | Хорошее | 1 GB |
| small   | 244 MB | Средне | Хорошее | 2 GB |
| medium  | 769 MB | Медленно | Отличное | 5 GB |
| large   | 1550 MB| Очень медленно | Лучшее | 10 GB |

## Устранение неполадок

### Ошибка "FFmpeg не найден"
```bash
# Проверьте установку
ffmpeg -version

# Если не работает, используйте полный путь
python transcribe.py audio.mp3 --ffmpeg "C:\ffmpeg\bin\ffmpeg.exe"
```

### Ошибка SSL при загрузке модели
```bash
# Скачайте модель вручную и укажите папку
mkdir whisper-models
# Скачайте small.pt в папку whisper-models
python transcribe.py audio.mp3 --models-dir "whisper-models"
```

### Ошибка "No module named 'numpy'"
```bash
pip install numpy tqdm
```

### Медленная работа
- Используйте модель `base` или `tiny`
- Убедитесь, что установлена CUDA версия PyTorch для GPU

## Примеры

### Транскрипция подкаста
```bash
python transcribe.py podcast.mp3 --model medium
```

### Быстрая транскрипция
```bash
python transcribe.py meeting.wav --model tiny
```

### Пакетная обработка (PowerShell)
```powershell
Get-ChildItem *.mp3 | ForEach-Object { python transcribe.py $_.Name }
```

## Лицензия

MIT License - см. файл [LICENSE](LICENSE)

## Вклад в проект

1. Fork репозитория
2. Создайте ветку для новой функции
3. Внесите изменения
4. Создайте Pull Request

## Поддержка

Если возникли проблемы:
1. Проверьте раздел "Устранение неполадок"
2. Создайте Issue с описанием проблемы
3. Приложите вывод команды с ошибкой
