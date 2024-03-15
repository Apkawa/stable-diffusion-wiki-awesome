+++
title = "Overview"
insert_anchor_links = "right"
weight = 100
+++
[sd-webui-controlnet](https://github.com/Mikubill/sd-webui-controlnet)


## IP-Adapter
Перенос стиля с изображения 

* https://habr.com/ru/articles/771500/

## Canny

После загрузки изображения-референса нейросеть рисует тонкой линией ее набросок. Так она довольно четко выделяет очертания объекта, сохраняя многие мелкие элементы.

## HED, Holistically-Nested Edge Detection.

Нейросеть при загрузке картинки размыто и неаккуратно очерчивает объекты на ней так, как это сделал бы человек.

## Depth

При загрузке создает набросок картинки с картой глубины — показывает, какие объекты располагаются ближе, а какие дальше.

Модель удобна для случаев, когда нужно заимствовать с изображения композиционную глубину.

## Normal Map
Карта нормалей определяет положение объекта в трехмерном пространстве.

Подходит для генерации 3D-персонажей или реалистичных картинок.

## MLSD, Mobile Line Segment Detection

Детектор прямых линий.

Полезен для генерации картинок на основе изображений с прямыми линиями: дизайна интерьеров, зданий, уличных сцен.

## Scribble

Генерирует картинку по скетчу. Достаточно сделать или загрузить рисунок, причем не нужно обладать талантом художника — хватит и примитивного наброска. А с помощью текста можно уже указать, во что превратить скетч.

## Recolor 

Раскраска ЧБ изображения или перекраска цветного 

## [OpenPose](./openpose.md)

Отлично работает с людьми на изображениях. При загрузке картинки определяет положение головы, плеч, рук, ног, а потом создает «скелет» — довольно точную схему позы. Если добавить текстовое описание, к примеру, поменять сыщика с референса на спасателя, то нейросеть изменит облик, но сохранит выбранную позу.


## QRCode-monster

Делаем скрытые но рабочие QR коды. И не только коды.

* https://huggingface.co/monster-labs/control_v1p_sd15_qrcode_monster
* https://civitai.com/models/111006/qr-code-monster
* https://learn.thinkdiffusion.com/hidden-faces-and-text-with-control-net-qr-code-monster/


## Instant ID

InstantID, который позволяет создавать изображения с использованием какого то лица. Именно что переносит ключевые особенности лица

* https://github.com/Mikubill/sd-webui-controlnet/discussions/2589

Скачайте модели в `{A1111_root}/models/ControlNet`
```
wget -O ip-adapter_instant_id_sdxl.bin https://huggingface.co/InstantX/InstantID/resolve/main/ip-adapter.bin 
wget -O control_instant_id_sdxl.safetensors https://huggingface.co/InstantX/InstantID/resolve/main/ControlNetModel/diffusion_pytorch_model.safetensors
```

## [TTPLanet_SDXL_Controlnet_Tile_Realistic_V1](https://civitai.com/models/330313/tplanetsdxlcontrolnettilerealisticv1?modelVersionId=370104)

Тайлинговая модель для контролнета, обучена на реалистичных данных.

Может менять цвет одежды и фон, с добавлением деталей уже сложнее. 
так же используется для апскейла, особенно для шумных изображений

Удобный вариант использования это img2img, но можно и txt2img, а картинка используется как референс по композиции.

Основные параметры:
* Замена деталей на фото (с раздеть есть сложности =3 )
    * Denoising strength: 0.8-1.0
    * Preprocessor: none
    * Model: ttplanetSDXLControlnet_v10F16.safetensors
    * Control Weight: 0.6-0.9
    * Control Mode: My prompt is more important
* Апскейл, например из 232x178 в 1856x1424 (надо разобраться в оптимальных параметрах и процессе)
    * Resize By: 2-4
    * Denoising strength: 0.1-0.3 (надо смотреть чтобы не потерялись основные детали)
    * Preprocessor: none
    * Model: ttplanetSDXLControlnet_v10F16.safetensors
    * Control Weight: 1-1.5
    * Control Mode: My prompt is more important
    * Script: SD Upscale

* Тайлинговый апскейл, должно решать вопрос с появлением артефактов, плюс сам апскейлер может терять детали \
    Нужно тестить
    * Resize By: 1
    * Denoising strength: 0
    * Preprocessor: none
    * Model: ttplanetSDXLControlnet_v10F16.safetensors
    * Control Weight: 1-1.5
    * Control Mode: My prompt is more important
    * Script: SD Upscale
    * Scale factor: 1.5-2
    * Upscaler: выбирайте сами, например  `R-ESRGAN 4x+`


#### ЧАВО

Q: `ModuleNotFoundError: No module named 'insightface'`\
A: https://github.com/Mikubill/sd-webui-controlnet/issues/2640
```
source venv/bin/activate
pip install insightface
```

### Гайды

* [Скрытый текст и оптические иллюзии с помощью ControlNet в Automatic 1111](https://dtf.ru/howto/2152000-skrytyy-tekst-i-opticheskie-illyuzii-s-pomoshchyu-controlnet-v-automatic-1111)
* [Делаем скрытый текст](https://takin.ai/learn/generate-images-with-hidden-text-using-stable-diffusion-and-controlnet)

score_9, score_8_up, score_7_up, score_6_up, 1girl, Japanese cartoon,  fox ears, small chest, perfect detailed hands, standing, surrounded by flowers, short hairs,
Nipples, pussy, nudity, spread own pussy, wet pussy, pussy juice, semi-realistic (detailed face:1.3), low angle, shy weak smile, line art, teeths,  ((paint outline:1.2)),
big green eyes,
<lora:Digital Art Style SDXL_LoRA_Pony Diffusion V6 XL:0.65> ,
<lora:add-detail-xl:1>,
<lora:xl_more_art-full_v1:0.1> ,
Negative prompt: (worst quality, low quality, ugly:1.4), poorly drawn hands, poorly drawn feet, poorly drawn face, out of frame, mutation, tail, furry, mutated, extra limbs, extra legs, extra arms, disfigured, deformed, cross-eye, blurry, (bad art, bad anatomy:1.4), blurred, text, watermark, tattoo,  kid, loli, poorlo drawn face, paint on face, colored nails,
Steps: 30, VAE: sdxl_vae.safetensors, Size: 960x1440, Seed: 132274579, Model: ponyDiffusionV6XL_v6StartWithThisOne, Version: f0.0.17v1.8.0rc-latest-269-gef35383b, Sampler: Euler a, VAE hash: 235745af8d, CFG scale: 7, Clip skip: 2, Mask blur: 4, Model hash: 67ab2fd8ec, add-detail-xl: 9c783c8ce46c, Denoising strength: 0.35, xl_more_art-full_v1: fe3b4816be83", "Digital Art Style SDXL_LoRA_Pony Diffusion V6 XL: 0cf042b134da

## Ссылки

* https://github.com/lllyasviel/ControlNet-v1-1-nightly
* [[Tutorial] Complete Guide to ControlNet for Stable Diffusion img2img](http://webcache.googleusercontent.com/search?q=cache%3Ahttps%3A%2F%2Faituts.com%2Fcontrolnet%2F&oq=cache%3Ahttps%3A%2F%2Faituts.com%2Fcontrolnet%2F&aqs=chrome..69i57j69i58.2752j0j4&sourceid=chrome&ie=UTF-8)
* [ControlNet: Control human pose in Stable Diffusion](https://stable-diffusion-art.com/controlnet/)
* [ControlNet and T2I-Adapter, the icebreaker solution for precise control of AI image generation](https://medium.com/@catmus2048/controlnet-and-t2i-adapter-the-icebreaker-solution-for-precise-control-of-ai-image-generation-ef61258139c3)
* [Как работает ControlNet: сервис для контролируемой генерации изображений](https://journal.tinkoff.ru/controlnet/)
* https://civitai.com/models/136070?modelVersionId=267533