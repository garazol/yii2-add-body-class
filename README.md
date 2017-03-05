# yii2-add-body-class
For YII2, it allows us to assign classes to html body from controller

### 1. Download

Yii2-user can be installed using composer. Run following command to download and
install Yii2-user:

```bash
composer require garazol/yii2-add-body-class
```

### 2. Configure

In the base controller place the behavior definition:

```php
// reference to the behavior class:
use garazol\addBodyClass\components\BodyClassBehavior;

// add body class behavior configuration to the behaviors method:
    /**
     * @inheritdoc
     */
    public function behaviors()
    {
        return [
            'BodyClassBehavior' => [
                'class' => BodyClassBehavior::className(),
                // you can define here what kind of classes should be rendered
                'autoGeneratedClassTypes' => ['userLoggedIn', 'controllerAction'],
            ],
        ];
    }
```
In the layout template you can render the composed body classes:
```php
<body class="<?= Html::encode($this->context->renderBodyClasses()); ?>">
```