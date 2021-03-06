# Внести свой вклад с помощью шаблона

Чтобы внести свой вклад с помощью шаблона CodeSandbox, необходимо выполнить несколько шагов и отправить два запроса Pull. 
Мы создали это руководство, чтобы помочь вам в этом.
Здесь вы найдете описания и объяснения того, что вам нужно сделать, а также некоторые примеры, которые мы добавили в качестве ссылок.

Мы понимаем, что процесс подачи шаблона не является простым, и надеемся, что это руководство поможет вам на этом пути. 
Мы работаем над системой, которая сделает это проще.

Если вы считаете, что мы что-то пропустили в этом руководстве, или считаете, что мы могли бы объяснить что-то получше, 
пожалуйста, сообщите нам об этом, отправив [вопрос](https://github.com/codesandbox/codesandbox-client/issues/new/choose) с вашими отзывами.

## Что такое шаблон?

Шаблон - это идентификатор для конкретного типа проекта песочницы, который вы можете создать на [codesandbox.io](https://codesandbox.io), 
как и проекты, использующие `Gatsby`, `React` или `Vue.js`.

Когда вы создаете шаблон, вы можете настроить поведение шаблона, чтобы улучшить пользовательский опыт вашего шаблона в редакторе CodeSandbox и в предварительном просмотре. 
Примером может служить настройка того, какой файл должен быть открыт в редакторе по умолчанию при выборе шаблона, 
или изменение правил `eslint` по умолчанию в шаблоне, например, с помощью `vue-cli`.

Мы призываем создателей шаблонов улучшать редактирование своих шаблонов, чтобы дать всем желающим лучший опыт при использовании шаблонов.

## Типы шаблонов

Шаблоны могут быть разных типов: **Песочницы** или **Контейнеры**, и имеют значительные различия в функциональности. 
Важно знать эти различия до начала работы над новым шаблоном.

### Sandboxes

CodeSandbox выполняет проекты в браузере, которые мы называем песочницами. 
Это означает, что перенос, объединение, разрешение зависимостей и многое другое происходит в самом браузере, без участия сервера. 
Это имеет некоторые преимущества перед традиционными подходами; он работает в автономном режиме, более производительный и не дает нам затраты на сервер, что означает, что мы можем иметь много песочниц, не беспокоясь (много ;-)).

Есть также некоторые недостатки этого подхода. Когда песочницы работают в браузере, мы теряем гибкость. 
Теряется возможность выполнять команды интерфейса командной строки (CLI), а в некоторых случаях пользовательские конфигурации не поддерживаются, 
например, пользовательская настройка web-пакета. 
Вот почему мы разработали новый вид песочницы под названием **Контейнер**, который выпустили в сентябре 2018 года.

### Контейнеры

В отличие от песочницы, **контейнеры** выполняются на сервере. 
Это позволяет создавать проекты, которые являются сквозными, например `Next.js` с CodeSandbox, а также дает возможность строить более крупные проекты. 
**Контейнеры** позволяют выполнять любую команду, и все, что работает локально, также будет работать в контейнере.

Однако, как и песочницы, **контейнеры** также поставляются с некоторыми ограничениями. 
Для того, чтобы работать над контейнером, вам нужно быть зарегистрированным пользователем, вы не можете редактировать контейнеры в автономном режиме, 
невозможно редактировать их из встраиваемого модуля, и вы можете иметь только ограниченное количество проектов, основанных на контейнере.

### Какой из них выбрать?

Как вы уже читали выше, тип шаблона определяет, выполняется ли проект в _sandbox в браузере или в _container на сервере. 
Это означает, что тип шаблона, который вы должны выбрать, зависит от вашего конкретного варианта использования и того, где вы хотите, чтобы ваш проект был выполнен.

Если вы хотите продемонстрировать функциональность CLI, мы рекомендуем использовать шаблон типа **контейнер**, 
а если вы хотите продемонстрировать фреймворк JavaScript (например, `React`), мы рекомендуем использовать шаблон типа **sandbox**.

Мы призываем всех сначала оценить, работает ли шаблон как песочница, прежде чем принимать решение об использовании контейнера.

## Добавление нового шаблона

Для того, чтобы добавить новый шаблон, необходимо пройти ряд шагов. 
Некоторые из этих шагов должны сделать вы, другие зависят от типа шаблона, который вы хотите добавить (**sandbox** vs. **контейнер**).

Для начала вы должны выполнить шаги, описанные в наших рекомендациях по вкладу, чтобы [настроить CodeSandbox локально](https://github.com/codesandbox/codesandbox-client/blob/master/CONTRIBUTING.md#setting-up-the-project-locally).

### 1. Добавить логотип шаблона

Добавьте логотип для вашего шаблона в [templates repo](https://github.com/codesandbox/codesandbox-client/tree/master/packages/template-icons/src) (`codesandbox-templates/packages/template-icons/src`).

#### Логотипы SVG

Создайте `.tsx` файл в каталоге `/src` с соответствующим именем и содержанием. Если ваш шаблон называется "Banana", назовите ваш файл с логотипом "BananaIcon".

Примеры:

- [Vue logo](https://github.com/codesandbox/codesandbox-client/tree/master/packages/template-icons/src/VueIcon.tsx)
- [React logo](https://github.com/codesandbox/codesandbox-client/tree/master/packages/template-icons/src/ReactIcon.tsx)

### 2. Добавить определение шаблона

Для того, чтобы CodeSandbox мог распознать ваш шаблон, вам нужно добавить новое определение в `codesandbox-client/packages/common/src/templates` [каталог](https://github.com/codesandbox/codesandbox-client/tree/master/packages/common/src/templates).
Вы делаете это, создавая новый `.ts` файл с именем вашего шаблона.

Примеры:

- [Parcel](https://github.com/codesandbox/codesandbox-client/blob/master/packages/common/src/templates/parcel.ts)
- [Gatsby](https://github.com/codesandbox/codesandbox-client/blob/master/packages/common/src/templates/gatsby.ts)

Определение шаблона может иметь различные опции, более подробную информацию о которых вы можете найти в 
[template.ts](https://github.com/codesandbox/codesandbox-client/blob/master/packages/common/src/templates/template.ts).

Мы рекомендуем вам улучшить пользовательский опыт ваших шаблонов, воспользовавшись доступными опциями во время написания определения шаблона.

Примеры:

- Какой редактор должен открыть файл по умолчанию
- Правила по умолчанию, которые шаблон должен использовать

<!-- TODO: Добавить дополнительные примеры -->

После написания определения Вашего шаблона, Вам также необходимо добавить его в файл [index.js](https://github.com/codesandbox/codesandbox-client/blob/master/packages/common/src/templates/index.ts) в том же каталоге (`codesandbox-client/packages/common/src/templates`), чтобы CodeSandbox мог извлечь Ваш шаблон.

### 3. Определение транспилеров для песочницы

_Если вы добавляете шаблон для песочницы **контейнера**, вы можете пропустить это, перейдя к шагу 4._

Для песочниц, которые запускаются в браузере, нам нужно определить, какие транспайлеры нужно запустить. 
Шаблон не будет работать в пакете, если он не имеет предустановленных настроек.

Мы называем конфигурацию шаблона для бандлера в CodeSandbox 'Предустановленный'. Все установленные на данный момент предустановки определены в файле [index.ts](https://github.com/codesandbox/codesandbox-client/blob/master/packages/app/src/sandbox/eval/index.ts) под `codesandbox-client/packages/app/src/sandbox/eval/presets`.

Для того, чтобы понять, как работает эта конфигурация, мы рекомендуем вам взглянуть на уже реализованные шаблоны и их предустановки.

Примеры:

- [create-react-app-typescript](https://github.com/codesandbox/codesandbox-client/blob/master/packages/app/src/sandbox/eval/presets/create-react-app-typescript/index.js)
  (самый основной)
- [CxJS](https://github.com/codesandbox/codesandbox-client/blob/master/packages/app/src/sandbox/eval/presets/cxjs/index.js)
- [vue-cli](https://github.com/codesandbox/codesandbox-client/blob/master/packages/app/src/sandbox/eval/presets/vue-cli/index.js)

### 4. Добавить импортёра

Мы позволяем людям импортировать песочницы из GitHub/CLI/API, и чтобы убедиться, что импортирован правильный шаблон, 
мы имеем некоторую специфическую логику, определяющую шаблон для каждого шаблона. 
Эта логика **не** находится в `codesanbox-client`.

Это означает, что вы также должны добавить ваш шаблон в другой файл в репозитории `кодов и ящиков-импортеров` с названием [templates.ts](https://github.com/codesandbox/codesandbox-importers/blob/master/packages/import-utils/src/create-sandbox/templates.ts).

Когда вы создаете свой Pull Request в `codesanbox-client`, вам также нужно создать Pull Request в `codesandbox-импортере` и сослаться на него в вашем Pull Request for `codesandbox-client`. 
Пример:

- [Добавить VuePress](https://github.com/codesandbox/codesandbox-client/pull/1652) в [codesandbox-client](https://github.com/codesandbox/codesandbox-client)
- [Добавить VuePress support](https://github.com/codesandbox/codesandbox-importers/pull/30) в [codesandbox-importer](https://github.com/codesandbox/codesandbox-importers)

### 5. Протестируйте шаблон

Вы можете протестировать ваш новый шаблон песочницы, однако вы не можете предварительно просмотреть функциональность шаблонов с помощью контейнеров.

#### Шаблон песочницы

Чтобы протестировать новый шаблон, необходимо создать имитационный ответ из API и форсировать новую спецификацию шаблона. Для этого вы разряжаете комментарий [этой строки](https://github.com/codesandbox/codesandbox-client/blob/master/packages/app/src/app/store/actions.js#L17) и меняете `'custom'` на id/name вашего шаблона:

```diff
    .then(data => {
-     // data.template = 'custom';
+     data.template = 'templatename';
      const sandbox = data;
      return path.success({ sandbox });
    })
```

#### Шаблон контейнера

<!-- TODO: здесь ясно, что делать -->
<!-- TODO: Улучшить описание шага -->

В настоящее время невозможно протестировать функциональность предварительного просмотра песочницы-контейнера и мы рекомендуем Вам проверить, 
работает ли песочница в шаблоне `node`. 
Если Ваш шаблон работает с `node`, он будет работать и с Вашим новым шаблоном.

Для этого, пожалуйста, добавьте файл `sandbox.config.json` в корневую папку хранилища, которое вы используете в качестве основы для вашего шаблона, с содержимым:

```json
{
  "template": "node"
}
```

Чтобы протестировать его, вы используете CodeSandbox для доступа к хранилищу, которое будет использоваться для такого шаблона: `https://codesanbox.io/s/github/user/repo-name`, где `user` - это пользователь/организация, которому принадлежит репозиторий, а `repo-name` - это имя репозитория, используемого для шаблона.

После того, как ваш Pull Request для добавления нового шаблона был объединен, вы можете удалить этот `sandbox.json.config` файл из вашего репозитория.

### 6. Добавьте себя в качестве участника

Этот проект соответствует спецификации all-contributors. Приветствуются любые взносы! 
Чтобы добавить себя в таблицу участников в файле README.md, пожалуйста, используйте автоматизированный скрипт как часть вашего PR:

```
yarn add-contributor
```

Следуйте инструкциям и зафиксируйте .all-contributorsrc и README.md в PR.

Спасибо, что нашли время внести свой вклад! 👍

### Заключение

Если ваше тестирование прошло хорошо, поздравляю! Теперь вы создали новый шаблон для CodeSandbox!

Мы позаботимся об объединении и развертывании двух Pull Requests, которые вы сделали одновременно для `codesanbox-клиента` и `codesandbox-импортеров`.
