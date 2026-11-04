# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/)
and this project adheres to [Semantic Versioning](http://semver.org/).

## [1.6.0]

### Changed
* Upgrade phpseclib/phpseclib from 2.0 to 3.0 (phpseclib 2.x is affected by security advisories)
* Require PHP 5.6.1 or greater (required by phpseclib 3)

## [1.5.0]

### Added
* Add option to hardcode JWKs

## [1.4.1]
* Bug Fixed for PHP 7.4

## [1.4.0]

### Added
* Add (Client Initiated Backchannel Authentication) CIBA support: non signed request + signed request, token request
* documentation for ciba coming soon

## [1.3.0]

### Added
* Add PKCE support to prevent authorization code interception attack

## [1.2.0]

### Changed
* change the type hint to support old php

## [1.1.0]

### Added
* Add function to get impersonated user's identifier

## [1.0.0]

### Added
* Init package
