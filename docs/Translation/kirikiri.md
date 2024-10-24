# Перевод игр созданных на [KiriKiri Engine](https://en.wikipedia.org/wiki/List_of_visual_novel_engines#KiriKiri)
В этом весьма полезном руководстве я хочу рассмотреть такой сложный но важдый для переводчика движок как **kirikiri**, не беря в расчет его модификации ибо о работе с ними я поговорю как нибудь в другой раз.

Вся сложность работы с движком Kirikiri в том, что в отличии от более простого в понимании **Ren'Py**, в том, что, он и его архивы могут быть защищены DRM защитой, и ключами шифрования без которых он не станет воспринимать архив как нечто цельное. 

Однако я воспользуюсь тем, что до нас уже любезно создали другие энтузиасты и провели громадную работу по отладке всего и вся.

---
В первую очередь я хочу поблагодарить:

[UlyssesWu](https://github.com/UlyssesWu) - [FreeMote](https://github.com/UlyssesWu/FreeMote), что лежит в основе многих проектов по работе с движком **KiriKiri**. <br>
[arcusmaximus](https://github.com/arcusmaximus) - [KirikiriTools](https://github.com/arcusmaximus/KirikiriTools) для работы с движком KiriKiri. <br>
[xmoezzz](https://github.com/xmoezzz) - [KrkrExtract](https://github.com/xmoezzz/KrkrExtract), что лег в основу следующим творениям энтузиастов. <br>
[morkt](https://github.com/morkt) - [GARbro](https://github.com/morkt/GARbro) за создание вьювера и упаковщика ресурсов движков визуальных новелл. <br>
[storycraft](https://github.com/storycraft) - [scn-tool](https://github.com/storycraft/scn-tool) который помогает с легкостью извлекать текст из **.scn** файлов и упаковывать его обратно теми же инструментами без дополнительного головняка. 


[fuwanovel.net](https://forums.fuwanovel.net) - англоязычный форум, за непрямую помощь в составлении данного гайда.

---

## Кодекс значений
- `.xp3` - Архив ресурсов используемый [KiriKiri Engine](https://en.wikipedia.org/wiki/List_of_visual_novel_engines#KiriKiri), аналогичен файлу `.rpa` в Ren'Py.
- `*.scn` - Файл содержащий в себе текст сцены а также её скрипты, аналогичен файлу `.rpyc` в Ren'Py.

---

## Извлечение текста
В этом примере, я хочу быстро продемострировать как можно сделать быстрый перевод без больших временных вложений, и особо не морочась с командной строкой и её производными. *Хотя испачкаться придется всё равно.*

### Распаковка ресурсов
1. Вам потребуется загрузить все [инструменты](https://github.com/arcusmaximus/KirikiriTools/releases/tag/1.7) по ссылке в тексте, или по [данной]() ссылке если репозитория оригинального автора больше не существует на момент просмотра документации.
- Расположите файл `version.dll` в папке игры на движке KiriKiri которую вы хотите перевести или распаковать её ресурсы, как правило в главной папке игры должны быть архивы, что оканчиваются на `.xp3`.
- Создайте пустой файл `extract-unencrypted.txt` в папке игры. 
    * Благодаря данному файлу, при следующем запуске игры, вы запустите распаковку в папку `unencrypted` в которой будут все файлы которые успел захватить хук `version.dll` и которые прочитал. 
    * *Для полной распаковки мы будем использовать другие инструменты, это же лишь временный способ для быстрого перевода.*
- После запуска игры, начните новую игру и просмотрите немного текста. После чего закройте игру, и в папке `unencrypted` вы обнаружите множество файлов которые успел распаковать хук, но вам должен быть интересен лишь один, это файл `.scn` вы должны найти его, после чего перейти к следующему шагу.
    * Также вы можете удалить файл `extract-unencrypted.txt` если хотите, он требуется только для распаковки, и не нужен для работы перевода в дальнейшем.

Вы распаковали ресурсы игры, не все, лишь часть, потому как данный способ не поддерживает распаковку всего, что вы **не увидели** вы можете пробежаться по всей игре и распаковать все ресурсы, или воспользоваться дополнительным другим способом, о котором пойдет речь после *Быстрой распаковки* она же *Извлечение текста* а пока продолжаем.

### Работа с текстом - распаковка и запаковка назад
Если вы уже распаковали ресурсы игры, или уже имеете в закромах некие `.scn` файлы, вам может быть интересно, а как же извлечь из них текст для работы с ним?! Что же, я дам вполне легкое и доступное пояснение, что делать дальше.

1. Теперь нам потребуется другой инструменты такой как [scn-tool](https://github.com/storycraft/scn-tool/releases), загрузите его по ссылке, или по [данной]() ссылке если репозитория оригинального автора больше не существует на момент просмотра документации.
- Распакуйте скачанный архив в любую папку.
- Открыв ранее распакованную папку, перетащите на файл `scn-script-extractor.exe` файл `.scn` из папки `unencrypted`, в результате чего вы получите в папке `unencrypted` файл с названием аналогичным тому, что вы перетащили, но с окончанием `.toml`.
    * Можете открыть его любым текстовым редактором и убедиться, что это простой текстовый документ с определенными числовыми указателями рядом со строками. Не трогайте их.

    > Хотя я думаю, что тот кто решился на перевод игры на KiriKiri Engine достаточно осведомлен в вопросах работы с различными движками, и понимает программирование на хотя-бы базовом уровне, чтобы осознавать свои действия и то к чему они могут привести.
    
- После того, как вы перевели `.toml` файл, и готовы запаковать его обратно в `.scn` то вам потребуется, открыть командную строку:
    * Ввести путь до вашей папки с иструментом `scn-script-inserter.exe` через `cd {путь}`
    * Ввести команду `scn-script-inserter.exe <toml_путь_до_файла> <scn_файл> [конечный_файл]`
    * После чего получите финальный файл `.scn` с вашими измененными строками.
    * Если финальный файл `.scn` не находится в папке `unencrypted`, то переместите его туда, с заменой файла если потребуется.

Теперь вы можете запустить игру и проверить вашу работу, и то, что благодаря хуку `version.dll` игра считывает файлы из папки `unencrypted` за место тех, которые расположены в оригинальных архивах игры. 

Тем самым давая свободу в работе и легкость изменения онных.

---

## Полная распаковка игры
Теперь я хочу рассмотреть легчайший способ по полной распаковке всех ресурсов игры, не прибегая к отдельному просмотру их ресурсов или монотонной работе с ними, если же вам требуется ими это, то воспользуйтесь GARbro, а я продолжу гайд.
### Загрузка необходимых инструментов
1. Первым делом загрузите [KrkrExtract](https://github.com/xmoezzz/KrkrExtract) по ссылке в тексте, или по [данной]() ссылке если репозитория оригинального автора больше не существует на момент просмотра документации.

    > Проверьте ваш антивирус, вполне вероятно он мог изолировать файлы программы и сработать ложно-позитивно на неё и её ресурсы. Если это случилось, то вытащите файлы из карантина или перекачайте их заново если антивирус их уже удалил, предварительно отметив что данный файл не является вирусов в вашем антивирусе а также браузере.

- После загрузки, расположите файлы: `KrkrExtract.Lite.exe` | `KrkrExtract.Core.dll` | `KrkrExtract.UI.Lite.dll` в главной папке игры, рядом с `.exe` файлом запускающим игру.


### Распаковка игры
В отличии от уже поднятого мною выше способа распаковки игры, в этот раз я хочу получить абсолютно все файлы и весь арт, включая анимации и спрайты, а также текст из игры, дабы уже работать с ними для перевода, или просто чтобы распаковать игру.

1. Представим, что вы выполнили все условия выше, а потому продолжим, перетащите запускающий игру `.exe` файл на `KrkrExtract.Lite.exe`, и подтвердите запуск, у вас откроется окно интерфейса программы `KrkrExtract` а также откроется сама игра, кроме этого также создадутся `.sig` и `.index` файлы всех архивов игры, в большинстве случаев это архивы `.xp3`
- Теперь перетащите каждый `.xp3` файл в окно `KrkrExtract` и дождитесь распаковки всех ресурсов архива, и проделайте тоже самое с каждым из них, или не с каждым, смотря что именно вам нужно.
    
    > Обычно игры на этом движке содержат только файлы `data.xp3` но иногда это могут быть отдельные архивы такие как `scn.xp3`, если вы собираетесь переводить текст, то вам нужен именно файл сценариев (сцен) а именно `scn.xp3`, но если игра не содержит его, то вероятно придется распаковать каждый из `.xp3` файлов, чтобы найти текст игры.
        
- Каждый из распакованных вами архивов переместился в папку `KiriKiri-Output` или что-то похожее, там будут лежать все распакованные файлы игры.

И на этом, с полной распаковкой всё, так как более подробный гайд не покрывается нашим бюджетом.

---

## Обьединяй и властвуй
Теперь я хочу обьединить оба гайда, и слепить из них более нечто узконаправленное и цельное, с целью получить более мелкий гайд, по полному переводу игры на движке [KiriKiri Engine](https://en.wikipedia.org/wiki/List_of_visual_novel_engines#KiriKiri).

Для полного перевода нам понадобится:

1. Навыки владения фотошопом
- Навыки владения русским и английским и японским языком
- Переводчик в подвале или в нашем уме
- Запретная магия древних, как как литературная редактура
- Графический дизайнер который оживит всё

А если по серьезному, то вам придется **просмотреть** и **перерисовать** каждый спрайт игры, который связан с интерфейсом, например кнопки, и отдельные экраны игры в которых текст вставлен изображением, а не как текст.

Если вы выполнили эту непростую задачу по перерисовке интерфейса и уже готовы протестировать ваш перевод, то вам потребуется `version.dll` из гайда по *[Извлечению текста](#_1)* а также создать папку `unencrypted` в папке с игрой, после чего поместить в неё все переведенные ресурсы игры, аналогично примеру выше.

> Если вы хотите, вы можете упаковать папку `unencrypted` как архив `unencrypted.xp3` при помощи [GARbro](https://github.com/morkt/GARbro), чтобы не смущать ваших пользователей непонятными папками и ресурсами в них, но об этом речь пойдет как-нибудь в другой раз.

Если вы всё сделали правильно, то после запуска игры вы увидите переведенные вами изображения, и ресурсы, а также переведенный вами текст, но если вы что-то сделали неправильно, то ищите ошибку у себя или в тексте данного гайда.

> На этом всё, хороших переводов!

---