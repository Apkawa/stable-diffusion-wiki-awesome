+++
title = "Loved models"
insert_anchor_links = "right"
weight = 200
+++

Мой список самых любимых моделей. 
Модели, которыми почти не пользуюсь и ничего про них сказать не могу, в список не попадали.

И еще, каждая модель имеет свои особенности которые надо учитывать и приспосабливаться. 

Модели, которые не попали в мой список, не обязательно плохие, просто я не научился их готовить под свои нужды. 
Пробуйте сами.

# Stable Diffusion 3

Ждем, трясемся

* https://stability.ai/news/stable-diffusion-3
* https://stability.ai/news/stable-diffusion-3-research-paper

# SDXL Lighting

Ключевая особенность - это быстрая генерация, модели нужно только 4-7 шага для получения достойных результатов

* CFG Scale: 2
* Sampling steps: 7
* Sampling method: 
  * LCM
  * Euler A SGMUniform
  * DPM++ 2M SDE SGMUniform
  * DPM++ 2S a Karras

В итоге работает быстрее, 15 секунд на генерацию против 50 для SDXL. А качество весьма пристойное, в отличие от `SDXL Turbo`

UPD: А в Forge еще быстрее получается, 5 секунд.

Ссылки: 

* https://medium.com/@emabyte/sdxl-lightning-speed-and-quality-combined-in-just-2-steps-a8ed0c491510
* https://huggingface.co/ByteDance/SDXL-Lightning
* https://arxiv.org/abs/2402.13929
* [CivitAI SDXL lighting models](https://civitai.com/search/models?baseModel=SDXL%20Lightning&sortBy=models_v5)


* Real
  * [RealVisXL V4.0](https://civitai.com/models/139562/realvisxl-v40) \
    Очень реалистичная модель
  * [Juggernaut XL V9+](https://civitai.com/models/133005/juggernaut-xl) 
  * [Lightning Fusion - SDXL Lightning v1.2](https://civitai.com/models/317816?modelVersionId=372560) \
    Более анимешная модель, но все таки причисляю к реалистичной   
* Anime 
  * [blue_pencil-XL Lightning](https://civitai.com/models/202108/bluepencil-xl-lcm-lightning?modelVersionId=369896)


# SDXL

## Real

* [Aetherverse XL](https://civitai.com/models/308337/aetherverse-xl) - мультиконцептуальная модель, с уклоном в реализм но может и в 2.5D и аниме

## Anime

### Pony Diffusion XL

Довольно интересная универсальная модель которая отлично понимает промпт и анатомию тела. 
Фактически выполняет почти любую идею без лор. 
Лоры нужны только для общей стилисgтики, детализации и конкретных персонажей.

Основные моменты
* Всегда начинать с тегов `score_9, score_8_up, score_7_up` и тд.
* Не использовать TI инверсии, они довольно сильно ломают картину

* Для определенного стиля нужны включать определенные теги. Можно экспериментировать с определенными комбинациями
    * anime `source_anime, Japanese cartoon`, neg: `source_cartoon, source_pony`
    * furry `source_furry`
    * western `source_cartoon` - в западном стиле, стиль комиксов и мультиков.
    * `source_pony` - ну вы поняли, это my little pony
    * `realistic, 3d` - в негативе если нужен рисованый стиль, или в позитиве если нужен реализм
      * Для пущего реализма стоит еще добавить всякие лоры вроде https://civitai.com/models/331812?modelVersionId=373148
* Так же есть специальные теги для sfw и nsfw
  * `rating_safe` - все делает приличным, даже если всякую пошлятину написать в промпте
  * `rating_questionable` - Softcore erotica. Simple nudity or near-nudity, but no explicit sex or exposed genitals.
  * `rating_explicit` - Blatantly sexual content. Explicit sex acts, exposed genitals, and sexual fluids.

**Ссылки:**

* [CivitAI: Pony Diffusion V6 XL](https://civitai.com/models/257749/pony-diffusion-v6-xl) - Базовая модель
* [CivitAI: AutismMix SDXL](https://civitai.com/models/288584/autismmix-sdxl) 
* [What is score_9 and how to use it in Pony Diffusion](https://civitai.com/articles/4248)
* [CivitAI: Список LORA и моделей для PonyXL](https://civitai.com/search/models?baseModel=Pony&sortBy=models_v5)
* https://rentry.org/ponyxl_loras_n_stuff


# SD1.5

Обычные модели основанные на SD1.5

С появлением SDXL и особенно SDXL Lighting подобные модели уже не особо актуальны, 
но все же нужны для использования старых лор и обучения своих лор используя видеокарты 6-8Гб видеопамяти.

## Real

* [epiCPhotoGasm](https://civitai.com/models/132632) - лучшая модель для фотореализма
* [ChilloutMix](https://civitai.com/models/6424/chilloutmix)
* модели [XpucT](https://www.youtube.com/@XpucT)\
  Он ушел с civitai, там не ищите.
  
  * [Deliberate](https://huggingface.co/XpucT/Deliberate/tree/main)
    * Обзор Deliberate https://www.youtube.com/watch?v=y-VIvC-kkkg
  * [Reliberate](https://huggingface.co/XpucT/Reliberate/tree/main) 
  


## 2.5D

* [ReV Animated](https://civitai.com/models/7371/rev-animated) \
  Хорошая модель для изображений в стиле псевдореализма

## Anime

* [Counterfeit](https://civitai.com/models/4468/counterfeit-v30) - Просто дженерик аниме
* [MeinaMix](https://civitai.com/models/7240/meinamix) 
* [Cetus-Mix](https://civitai.com/models/6755/cetus-mix)
* [zMix](https://civitai.com/models/45066?modelVersionId=49680) \
  Имеет интересную рисовку, особенно v1.0, новые версии имеют более обычную рисовку.

<!--
### NSFW 

* [Coconut furry mix 2](https://civitai.com/models/150116/coconut-furry-mix-2)
* [Pineapple anime mix](https://civitai.com/models/190067/pineapple-anime-mix)

-->

# Другие списки

* Создатель ControlNet и его [любимые модели на huggingface](https://huggingface.co/lllyasviel/fav_models/tree/main/fav)