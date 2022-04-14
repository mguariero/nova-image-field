# Nova Image Field

This package provides an image field for Nova resources allowing you to upload, crop and resize any image.

It uses [Cropper.js](https://fengyuanchen.github.io/cropperjs) with [vue-cropperjs](https://github.com/Agontuk/vue-cropperjs) on the client and [Intervention Image](http://image.intervention.io) on the server.

![screenshot of the advanced image field](https://github.com/mguariero/nova-image-field/blob/master/screenshot.png?raw=true)

## Requirements

In order to work, this package requires the following components:
- Laravel & Nova (2, 3 or 4)
- Fileinfo Extension

And **one of** the following libraries:
- GD Library >=2.0 (default)
- Imagick PHP extension >=6.5.7

See [Intervention requirements](https://image.intervention.io/v2/introduction/installation) for more details.

## Code examples

Nova`ImageField` extends from `Image` so you can use any methods that `Image` implements. See the documentation [here](https://nova.laravel.com/docs/3.0/resources/file-fields.html).

```php
// Show a cropbox with a fixed ratio
NovaImageField::make('Photo')->croppable(16/9),

// Resize the image to a max width
NovaImageField::make('Photo')->resize(1920),

// Override the image processing driver for this field only
NovaImageField::make('Photo')->driver('imagick'),
```

## API

### `driver(string $driver)`

Override the default driver to be used by Intervention for the image manipulation.

```php
NovaImageField::make('Photo')->driver('imagick'),
```

### `croppable([float $ratio])`

Specify if the underlying image should be croppable.

If a numeric value is given as a first parameter, it will be used to define a fixed aspect ratio for the crop box.

```php
NovaImageField::make('Photo')->croppable(),
NovaImageField::make('Photo')->croppable(16/9),
```

### `resize(int $width = null[, int $height = null])`

Specify the size (width and height) the image should be resized to.

```php
NovaImageField::make('Photo')->resize(1920),
NovaImageField::make('Photo')->resize(600, 400),
NovaImageField::make('Photo')->resize(null, 300),
```

*Note: this method uses [Intervention Image `resize()`](https://image.intervention.io/v2/api/resize) with the upsize and aspect ratio constraints.*

### `autoOrientate()`

Specify if the underlying image should be orientated.

Rotate the image to the orientation specified in Exif data, if any.

```php
NovaImageField::make('Photo')->autoOrientate(),
```

*Note: PHP must be compiled in with `--enable-exif` to use this method. Windows users must also have the mbstring extension enabled. See [the Intervention Image documentation](https://image.intervention.io/v2/api/orientate) for more details.*
