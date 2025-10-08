# Используем базовый образ Python 3.12
FROM python:3.12

# Устанавливаем системные зависимости и setuptools для замены distutils
RUN apt-get update && apt-get install -y python3-venv python3-pip build-essential \
    && pip install setuptools==70.0.0 \
    && rm -rf /var/lib/apt/lists/*

# Создаём рабочую директорию
WORKDIR /app

RUN pip install gunicorn==23.0.0

# Копируем файл зависимостей
COPY requirements.txt .

# Обновляем pip и устанавливаем зависимости проекта
RUN pip install --upgrade pip && pip install -r requirements.txt --no-cache-dir

# Копируем весь проект в контейнер
COPY . .

# Запускаем сервер Django
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "backend.wsgi"]
