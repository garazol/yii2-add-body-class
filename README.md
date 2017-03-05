# yii2-add-body-class
This Yii2 behavior class allows us to assign CSS classes to the layout HTML body element from controllers.

### 1. Download

Yii2-add-body-class can be installed using composer. Run following command to download and
install Yii2-add-body-class:

```bash
composer require garazol/yii2-add-body-class
```

### 2. Configure

In the base controller place the behavior definition:

(For detailed examination of special parameters see comments in this block.)

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
            // you can define here what kind of classes should be rendered automatically
            // key: AUTO_GENERATE_USER_LOGGED_STATUS can provide user-logged-in or user-logged-out
            // key: AUTO_GENERATE_CONTROLLER_ACTION can provide the current controller and action name classess, e.g.: controller-site and action-index
            // key: AUTO_GENERATE_MODULE can provide the current module, e.g.: module-example
            'autoGeneratedClassTypes' => [
                BodyClassBehavior::AUTO_GENERATE_USER_LOGGED_STATUS,
                BodyClassBehavior::AUTO_GENERATE_CONTROLLER_ACTION,
                BodyClassBehavior::AUTO_GENERATE_MODULE,
            ],
            // you can control the class style 
            // for hyphen separated classes use this (default) (results: user-logged-in)
            'classStyle'=>BodyClassBehavior::CLASS_STYLE_HYPHEN,//default
            // for camel case classes use this constant (results: userLoggedIn)
            //'classStyle'=>BodyClassBehavior::CLASS_STYLE_CAMEL_CASE,
        ],
    ];
}
```
In the layout template you can render the composed body classes:
```php
<body class="<?= Html::encode($this->context->renderBodyClasses()); ?>">
```
In any controller (which is extended from the base controller or ) you can add extra classes to body easily, just use: 
```php
public function actionExample()
{
    // code here...
    $this->addBodyClass('example');
    // or multiple classes
    $this->addBodyClass(['example', 'something']);
    // remove addded class
    $this->removeBodyClass('example');
    //remove multiple classes
    $this->removeBodyClass(['example', 'something']);
}
```