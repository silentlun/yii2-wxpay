yii2-alipay
===========
Wxpay extension for YII2

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist silentlun/yii2-wxpay "*"
```

or add

```
"silentlun/yii2-wxpay": "*"
```

to the require section of your `composer.json` file.


Usage
-----

Once the extension is installed, simply use it in your code by  :

```php
namespace app\controllers;

use yii\web\Controller;
use silentlun\wxpay\WxPay;

class SiteController extends Controller
{
	public $wxpayConfig = [
		'appid' => '公众号ID',
		'mch_id' => '商户号ID',
		'key' => '商户KEY',
		'app_secret' => '公众号SECRET',
	];
    public function actionPay()
    {
		$order = []; // 订单信息
        $payment = new WxPay($this->wxpayConfig);
		$result = $payment->createMiniPay($order);
		Yii::$app->response->format = \yii\web\Response::FORMAT_JSON;
		return $payment->GetJsApiParameters($result);
    }
}
```