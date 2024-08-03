# Laravel Heymarket Notification Channel

A Laravel package for Heymarket API integration.

## Installation

```bash
composer require carpool-logistics/laravel-heymarket
```

## Configuration

Publish the configuration file:

```bash
php artisan vendor:publish --provider="CarpoolLogistics\Heymarket\HeymarketServiceProvider"
```

Set your Heymarket API key in the `.env` file:

```
HEYMARKET_API_KEY=your_api_key
```

## Usage

Use the package in your Laravel notifications:

```php
use CarpoolLogistics\Heymarket\HeymarketChannel;

class OrderShipped extends Notification
{
    public function via($notifiable)
    {
        return [HeymarketChannel::class];
    }

    public function toHeymarket($notifiable)
    {
        return [
            'to' => $notifiable->phone_number,
            'body' => 'Your order has been shipped!',
            'teamId' => 'your_team_id'
        ];
    }
}
```