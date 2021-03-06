# Configuration

A configuration file must be specified when using lighthouse-inspector.

*sample-config.json*
```json
{
	"pages": [
		"https://google.com/"
	],
	"expectations": {
		"categories": {
			"pwa": 90,
			"best-practices": 90,
			"performance": 90,
			"accessibility": 90
		},
		"audits": {
			"first-meaningful-paint": 30,
			"load-fast-enough-for-pwa": true
		}
	},
	"lighthouseParams": {
		"flags": {
		  "chromeFlags": ["--headless"]
		},
		"config": {
		  "extends": "lighthouse:default"
		}
	}
}
```

*CLI*
```sh
lighthouse-inspector --config /path/to/config
```

## Properties

| Name | Type |
| - | - |
| pages | <code>string[]</code> |
| expectations | <code>Object</code> |
| lighthouseParams | <code>Object&#124;undefined</code> |
| failOnUnmetExpectation | <code>boolean</code> |

### `pages: string[]`

The `pages` property specifies a set of URLs to inspect with Lighthouse. At least one URL must be specified.

### `expectations: Object`

The `expectations` property specifies the expected score for certain Lighthouse categories and audits.
The expected score for categories must be a number. The expected score for audits must be a number or a boolean.
The categories and audits declared in the `expectations` object will be used to tell Lighthouse which categories and audits to test, by implicitly setting Lighthouse's configuration `settings.onlyCategories` and `settings.onlyAudits` (see [Lighthouse settings property documentation](https://github.com/GoogleChrome/lighthouse/blob/master/docs/configuration.md#settings-objectundefined)).

#### Options

| Name | Type | Description |
| - | - | - |
| categories | <code>Object</code> | An object where the key is the category id (as defined by the [Lighthouse categories configuration](https://github.com/GoogleChrome/lighthouse/blob/master/docs/configuration.md#categories-objectundefined)), and the value is the expected score for that category. |
| audits | <code>Object</code> | An object where the key is the audit name (as defined by the [Ligthouse audits configuration](https://github.com/GoogleChrome/lighthouse/blob/master/docs/configuration.md#audits-string)), and the value is the expected score for the audit. |

### `lighthouseParams: Object`

The `lighthouseParams` property specifies the flags and configuration for Lighthouse.

#### Options

| Name | Type | Description |
| - | - | - |
| config | <code>Object</code> | A Lighthouse configuration object as specified in the [Lightouse configuration file documentation](https://github.com/GoogleChrome/lighthouse/blob/master/docs/configuration.md). If `settings.onlyCategories` or `settings.onlyAudits` are set, the implicit configuration of these properties derived from the `expectations` object will be overriden. |
| flags | <code>Object</code> | An object containing Lighthouse flags, as specified in the [Lighthouse CLI options](https://github.com/GoogleChrome/lighthouse#cli-options). |

### `failOnUnmetExpectation: boolean`

The `failOnUnmetExpectation` property indicates whether the program will return with an error code when an expectation is unmet. Defaults to `false`.
