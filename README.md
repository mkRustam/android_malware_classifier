
https://github.com/bindog/ToyMalwareClassification

Структура датасета должна быть простой:
Класс_Вируса_1<br/>
  * файл1<br/>
  * файл2<br/>
  * ...<br/>
Класс_Вируса_2<br/>
  * файл1<br/>
  * файл2<br/>
  * ...<br/>

## Running
Pre-steps:
1. opcode_extractor <br/>
Решил вместо того, чтобы тащить за собой все apk файлы, сразу перевести их в opcode sequence и уже использовать их в качестве датасета
But don't delete APKs file

2. move all *.opseq files to 'train_opseq' folder <br/>
Тут нужно будет перенести все файлы (opcode sequence) в другую папку !СОХРАНИВ ПРИ ЭТОМ СТРУКТУРУ!

Steps:
1. csv_creator
2. randomsubset
3. Image-based approach
    - asmimage
    - firstrandomforest
4. Opcode N-gram based approach
    - opcode n-gram
    - secondrandomforest
5. combine

## Results
- firstrandomforest <br/>
  _Approach: imgfeature + subtrainLabels_
  <br/>
  _Score: 0.7403846153846154_
- secondrandomforest <br/>
  _Approach: 3gramfeature + subtrainLabels_
  <br/>
  _Score: 0.9083333333333333_  
- combine  <br/>
  _Approach: 3gramfeature + imgfeature + subtrainLabels_
  <br/>
  _Score: 0.9134615384615384_

**Комментарии:**<br/>
Небольшие проблемы вызвал csv файл imgfeature: в нем были проблем с NaN/null полями. Пришлось дропать эти поля. <br/>
<br/>
**Notes**<br/>
n-gram feature: N means how many lines will include in model as a one feature. For example:<br/>
Opcode:<br/>
_move 34<br/>
iput-oc asd<br/>
move 11<br/>
iput-cc asd<br/>
move 898<br/>
iput-c asd_<br/>
<br/>
with N = 3 opcode will be divided by blocks with 3 lines:<br/>
_move 34<br/>
iput-oc asd<br/>
move 11<br/>
<br/>
iput-cc asd<br/>
move 898<br/>
iput-c asd_<br/>
