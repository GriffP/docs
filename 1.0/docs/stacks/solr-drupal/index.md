# Solr for Drupal stack documentation

The only difference from the generic Solr stack is that core created with a config set from [Search API Solr module](https://www.drupal.org/project/search_api_solr) by default.

!!! info "Default core"
    We automatically create a default solr core named `default` when no cores found.

See generic [Solr stack](../solr/index.md) documentation to learn how to create and customize cores.

### Drupal 8/9

Make sure Solr you've deployed has a compatible default config set version (e.g.  `search_api_solr 4` or `search_api_solr-8.x-3.9`), if not – change the implementation to the appropriate (implementation differs in a Solr version and a default config set). Please note, if you change the implementation you'll have to [recreate cores](../solr#creating-solr-core) to change their config set because the existing cores will still use the same config set. You can find the list of supported config sets in [here](https://github.com/wodby/solr#config-sets).

Install [Search API Solr module](https://www.drupal.org/project/search_api_solr). Go to `Home » Administration » Configuration » Search and metadata » Search API`, create a new core or edit the default one. In expanded `CONFIGURE SOLR BACKEND` field set specify:

```
HTTP protocol: http
Solr host: solr
Solr port: 8983
Solr path: [LEAVE IT BLANK]
Solr core: [NAME OF YOUR CORE (usually "default")]
```

If your Solr config set version is older than `search_api_solr 8.x-3.0` you should specify `/solr` as a solr path.

If you're connecting externally to the solr server you can use a technical domain as your host and port `80` (exposed via edge). If you're connecting from the same server but a different application you can use `Internal hostname` that can be found on `App instance > Stack > [Solr Service]` page.

### Drupal 7

Install [Search API Solr module](https://www.drupal.org/project/search_api_solr). Go to `Configuration » Search and metadata » Search API` and select Service class to "Solr service". In expanded settings field set specify:

```
HTTP protocol: http
Solr host: solr
Solr port: 8983
Solr path: /solr/[NAME OF YOUR CORE]
```

!!! warning "Different hostname for stand-alone stacks"
    If you use a stand-alone Solr for Drupal stack for `Solr host` use `Internal hostname` from `[Instance] > Stack > Search Engine` page in case Drupal and Solr stacks deployed on the same server. 

## Changelog

This changelog is for Solr for Drupal stack on Wodby, to see image changes see tags description on [repository page](https://github.com/wodby/solr/releases).

### 2.3.22

⬆️ Solr 8.11.1

### 2.3.21

- 🚨 Fix for [CVE-2021-44228 ](https://github.com/advisories/GHSA-jfh8-c2jp-5v3q)
- 🥶 Base image ([wodby/base-solr](https://github.com/wodby/base-solr)) rebased to [wodby/openjdk](https://github.com/wodby/openjdk) with frozen Alpine 3.13
- 📜 Default config set for Solr 8 has been updated to `search_api_solr_4.2.3` (from 4.1.6), please note you have to recreate your solr cores to update their config set

### 2.3.20

⬆️ Solr 8.11.0

### 2.3.19

⬆️ Solr 8.10.1

### 2.3.18

⬆️&nbsp; Solr 8.10.0

### 2.3.17

- ⬆️&nbsp; Solr rebuilt for new config sets
- ⬆️&nbsp; Base image Alpine Linux updated to 3.13.5

### 2.3.16

⬆️&nbsp; Solr 8.8.2

### 2.3.15

⬆️&nbsp; Solr 8.8.1

### 2.3.14

⬆️&nbsp; Solr 8.8.0

### 2.3.13

- ⬆️&nbsp; Base image Alpine Linux updated to 3.12.3
- 🦴&nbsp; `ImagePullPolicy` changed to `IfNotPresent`

### 2.3.12

Solr 8.7.0

### 2.3.11

Solr now supports Search API Solr jump start configsets https://github.com/wodby/solr/issues/14

### 2.3.10

Solr 8.6.2

### 2.3.9

Solr 8.6.0

### 2.3.8

- Bugfix: invalid Solr image for Drupal 9 Solr 8
- Added Solr 8 variant with `search_api_solr_4.0` default config set

### 2.3.7

- Updated to 8.5.2
- Added new config set `search_api_solr_4.0`

### 2.3.6

Solr 8.5.1, 7.7.3

### 2.3.5

- Solr 8.5.0
- Added `search_api_solr` 3.9 config sets

### 2.3.4

Solr 8.3.1

### 2.3.3

Solr 8.3.0

### 2.3.2

Alpine Linux updated to 3.10.2 for Solr images

### 2.3.1

- Solr updated to 8.2.0
- We now run upgrade action that removes `default` core if it has a broken config set (so it can be automatically recreated). NOT applicable to EOL versions (6.4, 7.1, 7.2, 7.3, 7.4)

### 2.3.0

- Solr updated to 7.7.2
- Added new Solr 8.1 variant with search_api_solr 8.x-3.x configset https://github.com/wodby/solr/issues/8 
- Bugfix: `$SOLR_HEAP` did not have any effect
- Images rebased to wodby/base-solr (see README at https://github.com/wodby/base-solr)

### 2.2.2

- Solr updated to 6.6.6
- Alpine Linux updated to 3.9.4

### 2.2.1

Alpine Linux updated to 3.9.3

### 2.2.0

- Versions 5.4, 6.4, 7.1-7.4 no longer supported (marked as EOL)
- Versions 7.6, 7.7 added (and 5.5 for Drupal 7)
- Added new search_api_solr config sets (Drupal 8 default config set updated to `8.x-2.7`)    
- Bugfix: attachments indexation did not work in Drupal 7 https://github.com/wodby/solr/issues/5

### 2.1.0

* Added version 7.5
* Add Solr 6/7 variants for Drupal 7 
* search_api_solr version used for config sets now shown in titles and have been updated:
    * Drupal 7: 7.x-1.14 
    * Drupal 8: 8.x-1.2 for Solr 5, 8.x-2.1 for others

### 2.0.1

Solr patch update: 6.6.5

### 2.0.0

* Image `wodby/drupal-solr` now replaced with `wodby/solr` and `$SOLR_DEFAULT_CONFIG_SET`, see [versions matrix](https://github.com/wodby/solr#drupal-search-api-solr) 
* New Solr versions added: 7.4, 7.3 
* Dropped versions 6.3, 6.5, 7.0 
* Config sets and `solr.xml` now symlinked to volume, existing cores won't be affected
* Core directory get deleted when you delete a core via orchestration actions
* Bugfix: duplicated `configsets/configsets` directory

### 1.2.1

* New 7.2 version added
* Patch update: 6.6.3
* Solr 7.x config sources updated to search_api_solr `8.x-2.0-alpha3`

### 1.2.0

* Default [memory request](../config.md#resources) set to 256m

### 1.1.0

* New Solr versions 7.0.1 and 7.1.0 have been added with a config set from search_api_solr `8.x-2.0-alpha2`
* Solr versions updated and freezed: 6.6.2, 6.5.1, 6.4.2, 6.3.0, 5.5.5, 5.4.1
* Config set source search_api_solr updated to `8.x-1.2`
* We now create a default solr core named `default` automatically if no cores found
* Health check timeouts increased to 30 seconds

### 1.0.4

* Solr: fixed persistent data paths configuration

### 1.0.1

* Solr: new versions 6.6 and 6.5 for Drupal 8
* Solr: search_api_solr version updated from to 8.x-1.0 (default solr configs used from this module)
* Solr versions are now frozen https://github.com/wodby/solr#versions

### 1.0.0

Initial release