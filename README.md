# Filament billing provider for Laravel Cashier

[![Latest Version on Packagist](https://img.shields.io/packagist/v/maartenpaauw/filament-cashier-billing-provider.svg?style=flat-square)](https://packagist.org/packages/maartenpaauw/filament-cashier-billing-provider)
[![Tests](https://img.shields.io/github/actions/workflow/status/maartenpaauw/filament-cashier-billing-provider/run-tests.yml?branch=main&label=tests&style=flat-square)](https://github.com/maartenpaauw/filament-cashier-billing-provider/actions/workflows/run-tests.yml)
[![Total Downloads](https://img.shields.io/packagist/dt/maartenpaauw/filament-cashier-billing-provider.svg?style=flat-square)](https://packagist.org/packages/maartenpaauw/filament-cashier-billing-provider)

Add Laravel Cashier Stripe support to Filament multi tenant panels.

## Support me

[<img src="https://filamentphp.com/images/content/plugins/images/maartenpaauw-pennant.jpg?t=1" width="700px" />](https://filamentphp.com/plugins/maartenpaauw-pennant)

You can support me by [buying Pennant feature flags for Filament](https://filamentphp.com/plugins/maartenpaauw-pennant).

## Installation

You can install the package via composer:

```bash
composer require maartenpaauw/filament-cashier-billing-provider
```

## Usage

Add plans to your `cashier.php` config file:

```php
'plans' => [
    'basic' => [
        'trial_days' => 14,
        'price_id' => ENV('CASHIER_STRIPE_SUBSCRIPTION_BASIC_PRICE_ID'),
    ],
],
```

> **Warning**
> The current implementation only supports recurring subscriptions with trial days required.

Add the following code to your `AdminPanelProvider` (or other panel providers):

```php
use Maartenpaauw\Filament\Cashier\Stripe\BillingProvider;

// ...

public function panel(Panel $panel): Panel
{
    return $panel
        // ...
        ->tenantBillingProvider(new BillingProvider('basic'))
        ->requiresTenantSubscription()
        // ...
}
```

> **Note**
> Requiring tenant subscription is optional. You can remove `->requiresTenantSubscription()` if you wish.

## Testing

```bash
composer test
```

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Security Vulnerabilities

Please review [our security policy](../../security/policy) on how to report security vulnerabilities.

## Credits

- [Maarten Paauw](https://github.com/maartenpaauw)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
