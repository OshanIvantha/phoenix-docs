## Booting your app

Your app is eligible if it presents the `js/boot.js` file and a few needed methods therein.
Bootfiles are writen as requirejs modules.

#### boot.js

The example contains all mandatory objects and methods.

```
define({
	info: {
		id: 'my_app',
		name: "My App",
		author: "It's-a me Mario!",
		version: "0.1.0"
	},

	/**
	 * allow to setup the application
	 *
	 * @return promise
	 * @param self will feed back 'this' object
	 */

	setup: (self) => {
		var p = new Promise((resolve, defer) => {

			/**
			 * Here you can register Menu elements
			 * If your app is a plugin that waits
			 * for an event, you can start here silently
			 */

			resolve();
		});
		return p;
	},


	/**
	 * Start the application by mounting it to the DOM ID provided
	 *
	 * @return promise
	 * @param container dom-node ID to attach to
	 * @param self will feed back 'this' object
	 */

	boot: (container, self) => {
		var id = self.info.id;
		var p = new Promise((resolve, defer) => {

			requirejs([OC.appJS(id, id + '.bundle')], (app) => {

				// mount the app
				app.$mount(container);

				// listen to 'mounted' event
				app.$once('mounted', resolve());
			});
		});
		return p;
	}
});
```