# Message to Contributors/Сообщение тем кто хочет помочь
Для поддержания организованности перевода и для исключения ситуаций, когда 2 и более людей работают над переводом одного и того же абзаца/главы, пожалуйста, отпишитесь в соответсвующем тикете в разделе Issues.  

# How Skype fixes security vulnerabilities

![](https://habrastorage.org/files/09a/f14/e02/09af14e02e2b40178b7f543e83707803.png)

### In a nutshell: they don't

This post describes my fruitless effort to convience Microsoft employees that their service is vulnerable, and humiliation one has to go through should one's account be blocked by a hacker. This is a story of ignorance, pain and despair.

#### TL;DR

* *Anyone* can block your account permanently and you can't do anything about it. The only thing that's a hacker needs to know is your Skype login. In most cases Skype will refuse to unblock your account. Microsoft have known about the probem for years.

* 8-digit  authentication code (Microsoft Security Code) generation algorithm is vulnerable. These codes are used for password restore and the hacker can just guess the code without having access to your email account.

* Skype tech support is vulnerable to social engineering and Microsoft is perfectly OK with that.

* Skype tech support doesn't even know what's going on with your account and why it was blocked in the first place. Regardless of the reason you'll get a standard response that your account was blocked for "violating terms and conditions" even if it was you who clicked "Block account" button in their web interface.

* Skype still disclosures your public and private IP addresses, in some cases it's possible to disclosure other contacts that are using the same network (e. g. your family members using same Wi-Fi)

* A hacker can hide an active Skype session from the session list (it's available via /showplaces command) using old SDK versions. That allows to stealthly read your messages if one have managed to obtain your password.

### About me

I've been using Skype for 10 years. I'm used to be a Skype fanboy. When jira.skype.com (Skype's public bug tracker) was still available, I've been trying to improve skype and reporting bugs. 

SCW-2778 Remote DoS exploit for example. That vulnerability allowed to crash desktop version of Skype, so one couldn't without clearing history. Or SCW-3328 that allowed to remotely turn on your muted microphone during the call.

Even at that time I was worried by Skype's approach to fixing bugs. I had to literally beg developers to fix a problem that was there for years.

I was using all Skype's products, developer instruments (Skype4COM, SkypeKit), premium-subscriptions, Skype For Business. I have created bots, custom emoticon generation service, etc.

But today I sincerely hate Skype. It's a horrible service drown in bureucracy and ignorance of employees, that ignores the real problems and adds 3D emoticons as a major feature. Today Skype is not only insecure, but hazardous to its users, since security procedures are not only inefficient, they are working against users.

### Хронология событий

Уже на протяжении нескольких лет существуют уязвимости, приводящие к блокировке произвольного Skype-аккаунта. Их несколько, ими активно пользуются злоумышленники и предоставляют в качестве сервиса.

Раньше я много писал про уязвимости скайпа, и ко мне стали обращаться жертвы блокировок, которые находили меня через поиск.

Я видел разные случаи блокировок Skype-аккаунтов. Пытался помочь людям восстановить доступ и умолял Skype сделать с этим хоть что-то. 
Обычно это были блокировки через массовые жалобы. Это давно известный способ, который существует уже много лет. Он настолько старый, что стал частью детской субкультуры, ведущей войны друг с другом в Skype. Но за последний год случилось нечто вопиющее, о чем я не могу молчать. 

### Способ 1 — абузы (классический)

В Skype аккаунт блокируется автоматически, если на него поступило достаточное количество жалоб от других пользователей. Предположительно, более 20 штук. 
Для того, чтобы отправить жалобу, не нужно даже добавлять аккаунт в контакт-лист, это можно сделать, найдя аккаунт через поиск и кликнув «заблокировать → сообщить о нарушении».
Таким образом, жертва может не знать об отправленных в ее адрес жалобах.

Этой технике уже много лет. О ней писали на Хабре, о ней знают даже дети, которые собираются в группы для совместного накручивания жалоб.
Вот, например, найденные беглым поиском по vk.com:
vk.com/block_pidaram_skype
vk.com/skype_delete
vk.com/blacklistskype
vk.com/blockskyp
vk.com/eds_snos
vk.com/club58649499
vk.com/club49404483

Таких сообществ много и в самом Skype. Существует даже отдельная субкультура «вкачивателей». Обычно это дети 12-19 лет, которые объединяются в кланы. Суть их деятельности состоит в максимальном нанесении вреда оппоненту, который выбирается случайным образом.

Основные баталии происходят в виде словесных дуэлей в групповых звонках. Смысл в том, чтобы максимально унизить собеседника за короткий период времени и зафиксировать это на видео.

#### Видеозаписи дуэлей (Осторожно: мат и крики)
www.youtube.com/watch?v=F3mDFk5m_Hs
www.youtube.com/watch?v=cwNixaAML4I
www.youtube.com/watch?v=zWhCcqTnjxw
Запечатлен момент блокировки skype-аккаунта www.youtube.com/watch?v=4vhy-J-kQtk

Некоторые кланы вкачиваетелей выпускают свой фирменный софт для автоматизации вредоносной деятельности.

Демонстрация программы для массовой рассылки жалоб (Видео). Получается подобие ботнета из собственного контакт-листа, который добровольно абузит присланные аккаунты. Напомню, что для жалобы не нужно добавлять аккаунт жертвы к себе в контакты. То есть на вас может пожаловаться сотня школьников, с которыми вы никогда не общались, и вы этого не узнаете.

Я лично знаю десяток жертв, чьи аккаунты были удалены таким образом. На все обращения в поддержку Skype отвечают стандартной отпиской:

>I understand that your Skype account was blocked. I apologize for any inconvenience that this may have caused, but I will >be more than happy to look into this for you.
>Our automatic systems detected that activities which are contrary to Skype’s Terms and Conditions have taken place via your >Skype account. As a result, your account has been restricted and will remain restricted until further notice.

Угадайте, исправлена ли эта уязвимость на текущий момент? Конечно же нет!

### Блокировка через техподдержку

Осенью 2015 года мне стали писать люди, пострадавшие от нового вида атаки.
На этот раз перед блокировкой аккаунта жертве приходили письма от Microsoft с восьмизначным кодом. Письма были отправлены с ящика verifyme@microsoft.com и имели корректную DKIM-подпись, то есть были точно от Microsoft.

![Skype Security Code Attack](https://habrastorage.org/getpro/habr/post_images/c3f/a93/594/c3fa93594abc59015f23a6324442f503.png)

Проведя с друзьями собственное расследование, мы нашли исполнителя атаки. Его объявлениями были заполнены все форумы для малолетних кулхацкеров. 

Вот его реквизиты:

* ICQ: 676061500
* Skype: alaaasddsa1.as
* Jabber: block_service@xmpp.jp

Вот одно из объявлений удалятора:

![skype block service](https://habrastorage.org/getpro/habr/post_images/b38/74d/8a7/b3874d8a718696ddc3f6fadf8e80b688.png)

Чтобы проверить, как происходит удаление, я заказал у него удаление моего тестового аккаунта. 
Для чистоты эксперимента были соблюдены такие условия:

* Аккаунт был зарегистрирован на свежесозданный почтовый ящик, никак не связанный с аккаунтом. Угадать или найти почту от аккаунта в открытых источниках было невозможно.
* Был установлен сложный пароль из длинной последовательности цифр и букв в разном регистре
* В контакт-листе были добавлены только доверенные контакты.
* Аккаунт не состоял в конференциях и почти не использовался для переписки и звонков

На протяжении всего процесса удаления я мониторил почтовый ящик и был авторизован в десктопном Skype клиенте.

Через несколько часов после оплаты на почту посыпались письма с Microsoft Security Code, как на скриншоте выше. 

За 10 часов пришло 24 письма с кодами. Забегая вперед скажу, что атакующий в итоге угадывал код подтверждения.

Вот все коды из писем, пришедшие за время атаки, с привязкой ко времени получения письма.
Видно, что отправка происходит короткими всплесками в пределах нескольких минут.
```
Microsoft Support Code: 41917837 Fri, 26 Feb 2016 04:25:54 -0800 (PST)
Microsoft Support Code: 14793784 Fri, 26 Feb 2016 04:27:32 -0800 (PST)
Microsoft Support Code: 58837293 Sat, 27 Feb 2016 03:29:18 -0800 (PST)
Microsoft Support Code: 68871688 Sat, 27 Feb 2016 03:29:33 -0800 (PST)
Microsoft Support Code: 38424446 Sat, 27 Feb 2016 03:30:33 -0800 (PST)
Microsoft Support Code: 25068066 Sat, 27 Feb 2016 03:35:39 -0800 (PST)
Microsoft Support Code: 27311897 Sat, 27 Feb 2016 03:58:58 -0800 (PST)
Microsoft Support Code: 93194445 Sat, 27 Feb 2016 04:02:43 -0800 (PST)
Microsoft Support Code: 32506812 Sat, 27 Feb 2016 04:03:36 -0800 (PST)
Microsoft Support Code: 33627494 Sat, 27 Feb 2016 04:05:40 -0800 (PST)
Microsoft Support Code: 98350414 Sat, 27 Feb 2016 09:00:03 -0800 (PST)
Microsoft Support Code: 12437217 Sat, 27 Feb 2016 11:41:04 -0800 (PST)
Microsoft Support Code: 42078695 Sat, 27 Feb 2016 11:42:45 -0800 (PST)
Microsoft Support Code: 41321028 Sat, 27 Feb 2016 11:43:09 -0800 (PST)
Microsoft Support Code: 44964659 Sat, 27 Feb 2016 11:43:19 -0800 (PST)
Microsoft Support Code: 90692933 Sat, 27 Feb 2016 12:50:21 -0800 (PST)
Microsoft Support Code: 23696204 Sat, 27 Feb 2016 12:55:18 -0800 (PST)
Microsoft Support Code: 60212551 Sat, 27 Feb 2016 12:55:25 -0800 (PST)
Microsoft Support Code: 81725942 Sat, 27 Feb 2016 12:58:04 -0800 (PST)
Microsoft Support Code: 29172590 Sat, 27 Feb 2016 14:26:54 -0800 (PST)
Microsoft Support Code: 28091548 Sat, 27 Feb 2016 14:30:38 -0800 (PST)
Microsoft Support Code: 55969586 Sat, 27 Feb 2016 14:54:21 -0800 (PST)
Microsoft Support Code: 12424717 Sat, 27 Feb 2016 14:57:59 -0800 (PST)
Microsoft Support Code: 36300450 Sat, 27 Feb 2016 14:58:16 -0800 (PST)
```

После того, как письма прекратились, в профиле аккаунта удалились личные данные (имя, фамилия, пол). Остался только логин. В настройках аккаунта на сайте skype.com почтовый ящик сменился с моей почты на deleted@skype.com. Меня разлогинило из десктопного клиента.

На тот момент мы имели следующие данные:

* Атакующий не знает почту от аккаунта. Учитывая предыдущие инциденты со взломом аккаунтов, от которых была известна почта, можно было предположить похожую атаку.
* Пароль от аккаунта достаточно надежен и подбор исключен.
* Запросов авторизации от незнакомых контактов не происходило. В Skype-клиенте никакой активности не было. Атакующий никак не контактировал с жертвой.

Из этого не было понятно, как именно происходит удаление. Не удавалось найти форму, которая генерирует письма с Microsoft Security Code. Ничего не оставалось, кроме как пытаться выудить информацию у взломщика. Мы с друзьями продолжили заказывать удаление тестовых аккаунтов, и в один момент взломщик, в качестве доказательства выполнения атаки, показал скриншот, на котором оператор техподдержки подтверждает, что аккаунт успешно удален:

![skype chat support]https://habrastorage.org/getpro/habr/post_images/fec/2ff/787/fec2ff787f245cd7203c7d585371b7a8.png

Это была форма Live Chat Support, доступная аккаунтам с подпиской. Найти ее можно на сайте skype.com, пройдя несколько раз мастер решения проблем. Если выбирать все время «проблема не решена», то на последнем шаге предлагается открыть чат. 

Чат открывался со стороннего домена https://sales.liveperson.net. Из описания на сайте видно, что это сторонняя компания, предлагающая услуги поддержки для вашего продукта.

В итоге процедура удаления аккаунта через чат тех. поддержки выглядела так:

1. Атакующий говорит: «Пожалуйста, удалите мой аккаунт accountname, потому что я завел другой.
2. Оператор просит подтвердить владение аккаунтом, назвав код, который был выслан на почту, привязанную к аккаунту. При этом оператор не называет почты, а только ожидает правильный код.
3. После того, как оператор получит правильный код, аккаунт удаляется. При этом оператор соглашается выслать код повторно несколько раз и не возражает, если названный ему код не подходит.

Забавно, что в форму чата с поддержкой передается логин, под которым был авторизован клиент на skype.com. То есть оператор, в теории, должен видеть, с каким именно пользователем он общается. От того особенно странно, что можно назвать совершенно любой аккаунт для удаления и оператор послушно согласится начать процедуру удаления. 

В этот момент все еще неясно, как конкретно атакующий успешно завершает процедуру удаления. 

### Эй, Microsoft!

Уязвимость очевидна. Бежим кричать тревогу в Skype. 
Ведь такую серьезную уязвимость обязательно должны исправить, не так ли?

Так как у Skype нет каких-то публичных контактов для сообщений об уязвимостях, пробую написать на форум:
community.skype.com/t5/Security-Privacy-Trust-and/Vulnerability-allows-to-permanently-delete-any-skype-account-by/td-p/4222445
Никто не реагирует, зато в теме отметились другие жертвы этой атаки.

Через друзей мне удалось связаться напрямую с сотрудниками Microsoft. Я подробно описал все этапы уязвимости, приложил скриншоты, листинги кодов. Меня заверили, что начато внутреннее расследование. Серьезная компания ведь.

Однако спустя пару месяц ко мне снова обратились новые жертвы этой атаки. Сотрудники Microsoft сообщили, что расследование еще не закончено.

Пробую написать в secure@microsoft.com. Это специальный ящик для быстрого реагирования на критические уязвимости. Гарантируется ответ в течение 24 часов. В письме я подробно описываю этапы удаления аккаунта со скриншотами.

Ответ Microsoft Security Response Center:
![skype Microsoft Security Response Center](https://habrastorage.org/getpro/habr/post_images/f3d/4ae/d26/f3d4aed268ea20caf35fe040da0a4806.png)

Вольный перевод: это не уязвимость, вы просто дурак.

Раз в неделю я спрашивал, как продвигается расследование у ребят из Microsoft, на что получал ответ, что результата нет.
Так продолжалось около ШЕСТИ МЕСЯЦЕВ!!!. 

Было достоверно известно, что атакующий называет правильный код оператору. Иногда со второй-третьей попытки. Стыдно признаться, но мне так и не удалось выяснить как, именно это происходило. Сперва мне казалось, что код генерируется от времени, и поэтому атакующий пытается запросить как можно больше кодов в течение одной минуты, что видно по времени получения писем, но я не смог найти зависимости кода от времени. Возможно, был уязвим сам сервис чатов liveperson.net. 

Недавно Skype отказались от сервиса liveperson.net, и чат с агентом поддержки происходит на домене microsoft.com. Процедура удаления скайп-аккаунта теперь недоступна оператору тех. поддержки, и ее нужно выполнять самостоятельно через форму.

Наверное, тут вы подумаете, что уязвимость закрыта. Как бы не так.

### Эксперимент — умереть за ваши грехи

Спустя год после описанных выше событий, ко мне снова обратились жертвы нашего удалятора скайпов. Теперь письма с Security Code не приходили, очевидно был найден другой способ. 

Признаться, мне вся эта история уже порядком надоела. Я устал умолять, унижаться и выпрашивать исправить уязвимости по многу месяцев.

Как я уже говорил, я пользуюсь скайпом около десяти лет. Моему основному аккаунту **zhovner** примерно столько же. Мне показалось, что будет нечестно только смотреть на страдания других людей, не пережив этого самому. Тогда я решил провести эксперимент и заказать сразу удаление своего аккаунта.

![заказ удаления](https://habrastorage.org/files/eef/59b/d97/eef59bd9743046ca9037adae00ee7e23.png)

Стоимость работ — 2 тысячи рублей (примерно $30).
На этот раз удалятор обозначил три дня на выполнение работы. И действительно, через несколько дней меня разлогинило из скайпа, и больше я не мог в него войти. 

![успешное удаление](https://habrastorage.org/files/992/78b/2b5/99278b2b5d2048caad787812a7922eb0.png)

### Общение с техподдержкой Skype

Сразу после блокировки аккаунта я написал в техподдержку Skype. Предположив, что аккаунт был заблокирован старым добрым способом через массовые жалобы, я подробно описал ситуацию.

Оригинал переписки можно посмотреть здесь: telegra.ph/Account-blocked-by-mass-abuse-reporting (Читать сверху вниз)
Я рекомендую прочитать именно оригинал, чтобы ощутить полностью унижение, которое испытывают невинные жертвы блокировок.

Краткая выдержка из переписки:

```
<Я> Почему мой аккаунт заблокирован? Я предполагаю, что это результат массовых поддельных жалоб. 

<Skype> Наша автоматическая система заблокировала ваш аккаунт за нарушение правил использования Skype.

<Я> Ваша система уязвима, с помощью поддельных жалоб можно заблокировать чужой аккаунт, даже если он не выполняет никаких действий и не нарушает правила. Мой аккаунт был заблокирован именно таким образом. Пожалуйста, проверьте тщательно.

<Skype> Мы проверили, наша система не ошибается, вы точно нарушили правила. Наша система очень точна, и все действия логируются. Мы точно видим, что вы нарушили правила, ваш аккаунт не будет разблокирован никогда. Если хотите пользоваться скайпом дальше — заводите новый.

<Я> Ваша система подвержена мошенническим манипуляциям. Вот доказательства.

<Skype> Нет, наша система не ошибается, инфа 100%

<Я> Хорошо, назовите мои конкретные действия, которые привели к блокировке.

<Skype> Вы уже описали эти действия в предыдущих письмах. Вы правы насчет причин блокировки.

<Я> Вы что, сумасшедшие? Получается, вы подтверждаете, что любой аккаунт может быть удален, если злоумышленник отправит достаточное количество жалоб? И вы даже не знаете о причинах этих жалоб? Вы знаете, что эти абузы могут быть отправлены даже без добавления жертвы в контакт-лист. То есть их можно отправить с аккаунта, который никогда даже не общался с тем, на кого он жалуется. Получается, вы фактически подтверждаете существование такой уязвимости. Это вообще законно? Я планирую обратится в суд.

<Skype> Мы считаем, что предоставили вам достаточно информации. Вы просто говно и все тут.

<Я> Это очень серьезная уязвимость. Я считаю, что вы должны тщательно расследовать ее. У меня достаточно данных для воспроизведения этой уязвимости. Мы можем повторить ее на аккаунте, который вы предоставите, который точно не нарушает правила, и который вы полностью контролируете. Я оплачу удаление этого аккаунта атакующему, и вы сможете расследовать эту проблему.

<Skype> Мы понимаем, что вы хотите узнать точную причину удаления вашего аккаунта. Мы уже сообщали вам ранее, что наша автоматическая система выявления мудаков очень точна. Так вот, вы — мудак. У нас все записано!

<Я> Хорошо, что если я хочу сообщить об уязвимости? Вот ее подробное описание…

<Skype> Да нам пофиг вообще, идите в суд или полицию.
```

### Resume

It is already 15 days since my Skype account was banned. Out from the chat with support it is clear that nobody is trying to return my account back. I am really looking forward to receive my account back and get regrets from Skype for all the humiliations I need to get through, trying to make their services more secure.

Unfortunately Skype is big bureaucratic machine, which is not able to detect and react on the problems in their service due to poor organization, big and complex management structure. I have no doubt that anything will change here in the nearest future.

In this article I have described only problems which I know. I can assume that there exist much more exploits, which are in use, but I have no clue about them.

It is essential to understand that it is not ONLY Skype problem. This issues could be applied to ANY messenger with centralized control, where all security is based only on trust and authority of administration e.g. [Uber](http://www.foxnews.com/tech/2016/12/13/uber-allegedly-spied-on-users-including-celebrities-like-beyonc.html).
If you think that your lovely messenger is much more secure than Skype, just because the employees are "good guys", you are just fooling yourself.
People who have infinite access to the user information, could be vulnerable for different kind of pressure, blackmailing or deception. No one is ready to go to the jail or even to give their lives for the safety of users messages. As far as unlimited access exists, there will always be temptation to use this access wrongfully.

Truly safe messenger must be built on the impossibility of unauthorized access on a level of a specification, but not on a trust to an any group of people.
