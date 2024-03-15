+++
title = "Overview"
insert_anchor_links = "right"
weight = 100
+++


# [Forge (Stable Diffusion WebUI Forge)](https://github.com/lllyasviel/stable-diffusion-webui-forge)

Форк [A1111](https://github.com/AUTOMATIC1111/stable-diffusion-webui) от создателя ControlNet

Имеет ряд оптимизаций которые реально ускоряют генерацию и потребление памяти, меньше шансов получить OOM.

Плюс интегрирован ряд полезных расширений:

* Stable Video Diffusion (SVD) - генерация видео по изображению img2vid
* HyperTile - новый метод апскейла. Идея в том чтобы оптимизировать скорость апскейла и не свалиться в ООМ. \
    Все тесты проводились на RTX 3060 6Gb, вкладке img2img.  \
    Вывод - ускоряет только SD. SDXL и так быстро работает.

    * SD (Steps: 20, Sampler: DPM++ SDE Karras, CFG scale: 7, HyperTile_tile_size: 512)
        * 512 -> 1024: 21 -> 15.8 (x1.3)
        * 512 -> 2048: 3:21 -> 1:37 (x2)
    * SDXL (Steps: 20, Sampler: DPM++ SDE Karras, CFG scale: 7, HyperTile_tile_size: 1024)
        * 512 -> 1024: 13.2 -> 13.8 (x0.95)
        * 512 -> 2048: 1:24 -> 1:24 (x1)
        * 1024 -> 2048: 1:29 -> 1:23 (x1.07)
        * 1024 -> 4096: - OOM
    * SDXL Lighting (Steps: 8, Sampler: Euler A SGMUniform, CFG scale: 2)
        * 1024 -> 2048 44.2 -> 44.8 (x0.98)
        * 1024 -> 4096 - OOM
  
* KohyaHRFix - метод фикса нестандартных разрешений которые не совпадают с разрешением модели. Помогает избавиться от многоголовых и многоножек
* MultiDiffusion integrated - вариант апскейла/генерации нестандартных размеров. Отлично сочетается с Region Prompt
    * https://www.youtube.com/watch?v=qde9f_U6agU
    * https://multidiffusion.github.io/
    * https://civitai.com/models/34726?modelVersionId=54518
* LatentModifier - применяет к скрытым объектам различные фильтры и эффекты, например резкость.
* SelfAttentionGuidance - Улучшение качества выборки моделей диффузии
    * https://github.com/KU-CVLAB/Self-Attention-Guidance
* FreeU - метод, который существенно улучшает качество выборки диффузионной модели без каких-либо затрат: без обучения, без введения дополнительных параметров, без увеличения памяти или времени выборки.
    * https://stable-diffusion-art.com/freeu/
    * https://github.com/ChenyangSi/FreeU
  
* StyleAlign - выравнивает стили изображения по первому изображению из батча. Только для SDXL
    * https://style-aligned-gen.github.io/

* Zero123 (Z123) - превращает изображение в 3д объект.
* [DynamicThresholding (CFG-Fix)](https://github.com/mcmonkeyprojects/sd-dynamic-thresholding) - позволяет использовать более высокие масштабы CFG без проблем с цветом.


Полезные ссылки:
* https://youtu.be/toYRIs69iFc