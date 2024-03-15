+++
title = "Скрытый текст"
insert_anchor_links = "right"
weight = 500
+++

Методы скрытого текста

# [QRCode-monster](https://huggingface.co/monster-labs/control_v1p_sd15_qrcode_monster)

Модель для SD 1.5

Делаем скрытые но рабочие QR коды. И не только коды. 
Позволяет зашить реально рабочий QR код в изображение и можно даже не понять что там есть QR код.

Основные параметры:
* Preprocessor: none
* ContolNetModel: control_v10e_sdxl_opticalpattern
* Control Weight: 1
* Starting Control Step: 0.15
* Ending Control Step 0.75


Ссылки:

* https://huggingface.co/monster-labs/control_v1p_sd15_qrcode_monster
* https://civitai.com/models/111006/qr-code-monster
* https://learn.thinkdiffusion.com/hidden-faces-and-text-with-control-net-qr-code-monster/

# [OpticalPattern](https://huggingface.co/Nacholmo/controlnet-qr-pattern-sdxl)

Модель для SDXL

Основные параметры:
* Model: любая sdxl модель, с lighting работает но нужно подбирать параметры.
* Preprocessor: none
* ContolNetModel: control_v10e_sdxl_opticalpattern
* Control Weight: 1
* Starting Control Step: 0.15 
* Ending Control Step 0.75-0.90

[Повторить примерно как тут](https://civitai.com/images/2965250):
* Берем картинку из разряда "Искусство Мондриана", желательно с тонкими краями и без рамки
* Model: любая sdxl модель, с lighting не очень работает
* Size: хорошо срабатывает если размер меньше 1024
* Preprocessor: none
* ContolNetModel: control_v10e_sdxl_opticalpattern
* Control Weight: 0.70-0.95
* Starting Control Step: 0-0.1
* Ending Control Step 0.80-0.9
* Крутим рулеточку


Ссылки:
* https://civitai.com/models/161132/sdxl-controlnet-opticalpattern-optical-illusions