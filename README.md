# Awqat

Awqat is a package to calculate the 5 daily prayer times in Emacs.

## Installation

This package is currently not located on MELPA. To use it you should include the source file awqat.el in your source path.

## Setup

You should have your calendar latitude and longitude variables set up. Execute the commands `(calendar-latitude)` and `(calendar-longitude)` to see if these are set properly.

The prayer times can be configured in the following ways:
- Fajr
  - If using angle-based method, you can set the angle to calculate Fajr with the `awqat-fajr-angle` variable. (used in conjunction with the `awqat-use-angle-based-method` function)
  - If using offset-based method, you can set the hours before sunrise via the `awqat-fajr-before-offset` variable. (used in conjunction with the `awqat-use-time-offset-method` function)
- Sunrise
  - You can set the angle that the sun should be below the horizon with the `awqat-sunrise-sunset-below-angle` variable. Defaults to -1.66.
- Dhuhr (only safety offset, see below)
- Asr
  - You can set the flag `awqat-asr-hanafi` to true for hanafi based calculation method, or nil for Hanbali, Shafii, and Maliki. The Hanafi method will be later than the other.
- Maghrib
  - Like for sunrise you can set `awqat-sunrise-sunset-below-angle`.
- Isha
  - Like for Fajr you can set the angle for calculation with the `awqat-isha-angle` variable. (used in conjunction with the `awqat-use-angle-based-method` function)
  - If using the offset-based method, you can set the hours after sunset via the `awqat-isha-after-sunset` variable. (used in conjunction with the `awqat-use-time-offset-method` function)

You can add a safety offset to all times via the `awqat-prayer-safety-offsets` variable. For example, to have sunrise be one minute sooner, Dhuhr two minutes later, and Maghrib one minute later you can add `(setq awqat-prayer-safety-offsets '(0 -1 2 0 1 0))`.

There are presets with the angles for various organizations. You can call these functions to configure the various variables. The following presets exist: `awqat-set-preset-muslim-pro`, `awqat-set-preset-muslim-world-league`, `awqat-set-preset-karachi-university-of-islamic-sciences`, `awqat-set-preset-umm-al-qura`, `awqat-set-preset-jakim`, `awqat-set-preset-spiritual-administration-of-musilms-russia`, `awqat-set-preset-union-des-organisations-islamiques-de-france`. Please note that these presets **only** configure the angles for Isha and Fajr and may or may not reflect the actual times of the organization.

The following is an example configuration:
```lisp
(require 'awqat)
(setq awqat-asr-hanafi nil)
(setq awqat-fajr-angle -18.0)
(setq awqat-isha-angle -16.0)
```

## Viewing the times

By calling `M-x awqat-times-for-day` you can see the various times for the day with the time remaining for the next prayer.

## A note on the calculation

Please be warned that this package may contain bugs and may not reflect the times of the particular organization that you follow. The calculations for Isha and Fajr for high latitudes can especially be erronious as no special calculation methods have been implemented. The site http://praytimes.org/calculation mentions the *middle of night*, *one-seventh of the night*, and *angle-based* methods for calculating times at higher latitudes. None of these methods are implemented yet.