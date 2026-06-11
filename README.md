![marshmallow.](https://marshmallow.dev/cdn/media/logo-red-237x46.png "marshmallow.")

# SignRequest PHP Client

[![Latest Version on Packagist](https://img.shields.io/packagist/v/marshmallow/signrequest-client.svg?style=flat-square)](https://packagist.org/packages/marshmallow/signrequest-client)
[![Total Downloads](https://img.shields.io/packagist/dt/marshmallow/signrequest-client.svg?style=flat-square)](https://packagist.org/packages/marshmallow/signrequest-client)
[![License](https://img.shields.io/packagist/l/marshmallow/signrequest-client.svg?style=flat-square)](https://packagist.org/packages/marshmallow/signrequest-client)

Official PHP client for [SignRequest.com](https://signrequest.com) — send documents for digital signing, manage templates, teams and webhooks through the SignRequest REST API.

> **Why this fork?** This is a published fork of [`SignRequest/signrequest-php-client`](https://github.com/SignRequest/signrequest-php-client), republished so it can be installed on PHP 8+ projects. We opened a pull request against the original package but couldn't wait for it to be processed. Once the upstream package supports PHP 8+, this fork will be removed.

This is a plain PHP SDK generated with [Swagger Codegen](https://github.com/swagger-api/swagger-codegen) on top of [Guzzle](https://github.com/guzzle/guzzle). It is framework-agnostic — there is no Laravel service provider, config publishing or facade.

## Requirements

- PHP `^7.2.5 || ^8.0`
- Extensions: `ext-curl`, `ext-json`, `ext-mbstring`
- [`guzzlehttp/guzzle`](https://github.com/guzzle/guzzle) `^7.3`

## Installation

Install the package via Composer:

```bash
composer require marshmallow/signrequest-client
```

The package is autoloaded under the `SignRequest\` namespace (PSR-4). If you are not using Composer's autoloader yet, require it:

```php
require_once __DIR__ . '/vendor/autoload.php';
```

## Authentication

All requests are authenticated with a SignRequest API token, sent as an `Authorization: Token <your-api-key>` header. You can find your token in your SignRequest account settings.

Configure it once on the shared `Configuration` instance:

```php
$config = SignRequest\Configuration::getDefaultConfiguration()
    ->setApiKey('Authorization', 'YOUR_API_KEY')
    ->setApiKeyPrefix('Authorization', 'Token');
```

The default API base URL is `https://signrequest.com/api/v1`. You can override it with `$config->setHost('https://...')` if needed.

## Usage

Each resource has its own API class under `SignRequest\Api`. Instantiate it with a Guzzle client and your configured `Configuration`, then call the typed methods. Example — creating a document:

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

// Configure API key authorization: Token
$config = SignRequest\Configuration::getDefaultConfiguration()
    ->setApiKey('Authorization', 'YOUR_API_KEY')
    ->setApiKeyPrefix('Authorization', 'Token');

$apiInstance = new SignRequest\Api\DocumentsApi(
    // If omitted, a default GuzzleHttp\Client is used.
    new GuzzleHttp\Client(),
    $config
);

$data = new \SignRequest\Model\Document();
// ...populate $data...

try {
    $result = $apiInstance->documentsCreate($data);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling DocumentsApi->documentsCreate: ', $e->getMessage(), PHP_EOL;
}
```

Every API method also has an asynchronous counterpart (e.g. `documentsCreateAsync()`) returning a Guzzle promise.

## Available API classes

All classes live in the `SignRequest\Api` namespace. See the linked docs for every method, parameter and return type.

| API class | Description | Docs |
| --- | --- | --- |
| `ApiTokensApi` | Manage API tokens | [docs](docs/Api/ApiTokensApi.md) |
| `DocumentsApi` | Create, read, list and delete documents | [docs](docs/Api/DocumentsApi.md) |
| `DocumentAttachmentsApi` | Manage document attachments | [docs](docs/Api/DocumentAttachmentsApi.md) |
| `DocumentsSearchApi` | Search documents | [docs](docs/Api/DocumentsSearchApi.md) |
| `EventsApi` | Read account events | [docs](docs/Api/EventsApi.md) |
| `SignrequestsApi` | Send and manage sign requests | [docs](docs/Api/SignrequestsApi.md) |
| `SignrequestQuickCreateApi` | Create a sign request in one call | [docs](docs/Api/SignrequestQuickCreateApi.md) |
| `TemplatesApi` | Manage templates | [docs](docs/Api/TemplatesApi.md) |
| `TeamsApi` | Manage teams | [docs](docs/Api/TeamsApi.md) |
| `TeamMembersApi` | Manage team members | [docs](docs/Api/TeamMembersApi.md) |
| `WebhooksApi` | Manage webhooks | [docs](docs/Api/WebhooksApi.md) |

Request/response models live in the `SignRequest\Model` namespace and are documented under [`docs/Model`](docs/Model).

## Documentation

- Generated client reference: [`docs/Api`](docs/Api) and [`docs/Model`](docs/Model)
- SignRequest REST API: <https://signrequest.com/api/v1>
- Upstream package: [SignRequest/signrequest-php-client](https://github.com/SignRequest/signrequest-php-client)

## Testing

```bash
composer install
./vendor/bin/phpunit
```

## Credits

- [SignRequest](https://signrequest.com/) — original author of the client
- [Stef van Esch](https://marshmallow.dev/) / [Marshmallow](https://marshmallow.dev/) — PHP 8+ fork
- [All Contributors](https://github.com/marshmallow-packages/signrequest-php-client/contributors)

## License

The MIT License (MIT). Please see the [License File](LICENSE) for more information.
