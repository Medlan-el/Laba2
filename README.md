# Создание инструмента для распознавания речи в различных диалектах: адаптация моделей распознавания на разные языковые варианты

Whisper:
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1SjEl51PWQvQU-Iz-D-QtKw02ODncgLtV#scrollTo=czBHXELISwwU)

Google:
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/177Cq-ZhcfhVX9Ba6T6sy3L9TfVJReSr3#scrollTo=d5f80175)

## Установка

Запустите скрипт:

```sh
pip install jupyter
pip install nbconvert
```

```sh
jupyter nbconvert --to notebook --execute
file_name.ipynb
```

## Алгоритм работы

В качестве примера я привела два алгоритма, реализующие обработку голоса и распознавание речи. Первые алгоритм основан на модели от [OpenAI](https://github.com/openai/whisper). Второй алгоритм осуществляется через модель от [Google](https://cloud.google.com/speech-to-text/docs/speech-to-text-supported-languages).

Оба алгоритма работают по одинаковому процессу. В качестве входных данных мы загружаем видео из youtube и меняем его формат `.wav`. Для преобразования видео мы используем библиотеку yt-dlp.

Далее полученная аудиодорожка обрабатывается и на выходе мы получаем текст разбитый на сегменты (таймкоды). Пример выходных [данных](./output/output.csv). 

![](https://raw.githubusercontent.com/openai/whisper/main/approach.png)

**Замечание:**  Вторая модель требует предварительной обработки входных данных, такой как разделение аудиодорожки на сегменты, токенизация и обработка языка. Модель от OpenAI предоставляет все необходимые инструменты "из коробки".

Подробные инструции к моделям можно узнать по ссылка ниже

- [Whisper](https://github.com/openai/whisper)
- [Google speach to text](https://cloud.google.com/speech-to-text/docs/speech-to-text-supported-languages)

Оба варианта не требуют платных подписок или api.

## Использование

Вы можете заменить `url` youtube видео на свой:

```python
extract_audio(filename="test_audio", file_ext="mp3", url="url_here")
```

**Замечание:** Чем длиннее видеоролик, тем более эффективно модели воспринимают его основную суть, что влечет за собой повышение качества обработки. Однако, из-за необходимости сегментации аудиодорожки второй моделью, вызванной ограничениями Google, рекомендуется избегать видеороликов длиннее 5 минут.
