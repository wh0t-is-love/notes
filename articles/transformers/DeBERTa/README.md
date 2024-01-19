# DeBERTa

Ссылка на [статью](https://arxiv.org/pdf/2006.03654.pdf)

Статья на [habr](https://habr.com/ru/companies/lanit/articles/749946/)

[Пример](https://habr.com/ru/amp/publications/725960/) использования

DeBERTa (Decoding-enhanced BERT with disentangled attention) – дословно BERT улучшенного декодирования с рассеянным вниманием. Это основанная на RoBERTa архитектура, в которой авторы дополнительно применили механизм кодирования слова двумя векторами (кодирующими его содержание и положение в тексте) и заменили выходной softmax-слоя усовершенствованным декодером. Вот пример успешного применения этой архитектуры.

_Цитата из статьи_

```
Unlike BERT where each word in the input layer is represented using a vector which is the sum of its word (content) embedding and position embedding, each word in DeBERTa is represented using two vectors that encode its content and position, respectively, and the attention weights among words are computed using disentangled matrices based on their contents and relative positions, respectively. This is motivated by the observation that the attention weight of a word pair depends on not only their contents but their relative positions. For example, the dependency between the words “deep” and “learning” is much stronger when they occur next to each other than when they occur in different sentences.

В отличие от BERT, где каждое слово во входном слое представлено с использованием вектора, который является суммой вложения его слова (содержимого) и вложения позиции, каждое слово в DeBERTa представлено с использованием двух векторов, которые кодируют его содержимое и позицию соответственно, а весовые коэффициенты внимания между словами вычисляются с использованием распутанных матриц, основанных на их содержимое и взаимное расположение соответственно. Это мотивировано наблюдением, что привлекательность пары слов зависит не только от их содержания, но и от их взаимного расположения. Например, зависимость между словами “глубокий” и “обучение” гораздо сильнее, когда они встречаются рядом друг с другом, чем когда они встречаются в разных предложениях.
```

И еще одна:

```
Like BERT, DeBERTa is pre-trained using masked language modeling (MLM). MLM is a fill-in-the-blank task, where a model is taught to use the words surrounding a mask token to predict what the masked word should be. DeBERTa uses the content and position information of the context words for MLM. The disentangled attention mechanism already considers the contents and relative positions of the context words, but not the absolute positions of these words, which in many cases are crucial for the prediction. Consider the sentence “a new store opened beside the new mall” with the italicized words “store” and “mall” masked for prediction. Although the local contexts of the two words are similar, they play different syntactic roles in the sentence. (Here, the subject of the sentence is “store” not “mall,” for example.) These syntactical nuances depend, to a large degree, upon the words’ absolute positions in the sentence, and so it is important to account for a word’s absolute position in the language modeling process. DeBERTa incorporates absolute word position embeddings right before the softmax layer where the model decodes the masked words based on the aggregated contextual embeddings of word contents and positions.

Как и Берт, Деберта предварительно обучена с использованием masked language modeling (MLM). MLM - это задача "заполнить пробел", в которой модель учат использовать слова, окружающие маркер маски, чтобы предсказать, каким должно быть замаскированное слово. ДеБЕРТа использует информацию о содержании и позиционировании контекстных слов для MLM. Механизм рассеянного внимания уже учитывает содержание и относительное положение слов контекста, но не абсолютное положение этих слов, которые во многих случаях имеют решающее значение для прогнозирования. Рассмотрим предложение “новый магазин открылся рядом с новым торговым центром” с выделенными курсивом словами “магазин” и “торговый центр”, замаскированными для предсказания. Хотя локальные контексты этих двух слов схожи, они играют разные синтаксические роли в предложении. (Здесь подлежащим предложения является, например, “магазин”, а не “торговый центр”.) Эти синтаксические нюансы в значительной степени зависят от абсолютного положения слов в предложении, и поэтому важно учитывать абсолютное положение слова в процессе языкового моделирования. DeBERTa включает в себя встраивание абсолютных позиций слов непосредственно перед слоем softmax, где модель декодирует замаскированные слова на основе агрегированных контекстных встраиваний содержимого слов и позиций.
```

