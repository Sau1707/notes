Created for React, add a way to directy style componets. It manage automatically classnames

- [Website](https://styled-components.com/)
- [Documentation](https://styled-components.com/docs)

## Installation
```bash
npm install --save styled-components
```


## Next render error
Add a page called `_document.js` into the `pages` folder with:
```jsx
import Document from 'next/document';
import { ServerStyleSheet } from 'styled-components';

export default class MyDocument extends Document {
	static async getInitialProps(ctx) {
		const sheet = new ServerStyleSheet();
		const originalRenderPage = ctx.renderPage;

		try {
			ctx.renderPage = () =>
				originalRenderPage({
					enhanceApp: (App) => (props) => {
					return sheet.collectStyles(<App {...props} />)
					},
				});

			const initialProps = await Document.getInitialProps(ctx);
			return {
				...initialProps,
				styles: (
					<>
						{initialProps.styles}
						{sheet.getStyleElement()}
					</>
				),
			};
		} finally {
			sheet.seal();
		}
	}
}
```

And in the `package.json`
```json
"babel": {
		"env": {
			"development": {
				"presets": [
					"next/babel"
				],
				"plugins": [
					[
						"styled-components",
						{
							"ssr": true,
							"displayName": true
						}
					]
				]
			},
			"production": {
				"presets": [
					"next/babel"
				],
				"plugins": [
					[
						"styled-components",
						{
							"ssr": true,
							"displayName": false
						}
					]
				]
			}
		}
	}
```

This will make styled components render on the server side and prevent missing classname on page reload