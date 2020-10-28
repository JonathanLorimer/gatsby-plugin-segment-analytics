# gatsby-plugin-segment-analytics

A [Gatsby](https://www.gatsbyjs.org) plugin to add
[Segment’s](https://segment.com/) Analytics.js integration.

This is designed to work with Gatsby versions ≥ 2.0.0.

## Installation

Install with yarn...

```sh
yarn add gatsby-plugin-segment-analytics
```

or NPM...

```sh
npm i gatsby-plugin-segment-analytics
```

### Configure

In your `gatsby-config.js`, add the `gatsby-plugin-segment-analytics` plugin and
provide your Segment Analytics.js write key as an option:

```js
module.exports = {
  plugins: [
    {
      resolve: "gatsby-plugin-segment-analytics",
      options: {
        writeKey: "YOUR WRITE KEY",

        // Note: if no eventName is provided then the eventName will be set to
        // "Page" in development mode (viewable from the console) and will be omitted
        // in production. The properties object will still be automatically populated
        // by segment's Analytics.js snippet.
        eventName: "YOUR PAGE EVENT NAME",
      },
    },
  ],
}
```

## Usage

The latest version of the Segment tracking snippet will automatically be
generated and injected into the `<head>` of your layout using Gatsby's SSR API
hooks. When a page is loaded, and Gatsby's `onRouteUpdate` API is called,
`analytics.page` will be fired.

In development, `window.analytics` is a shim that simply logs calls to the
console rather than sending noise to Segment.

### Outbound Link Tracking

To make it easy to track clicks on outbound links, this plugin provides an
`OutboundLink` component similar to the one provided by
[gatsby-plugin-google-analytics](https://github.com/gatsbyjs/gatsby/tree/master/packages/gatsby-plugin-google-analytics#outboundlink-component).

To use it, simply import it and use it like you would the `<a>` element e.g.

```js
import React
import { OutboundLink } from "gatsby-plugin-segment-analytics"

export default () => {

  <div>
    <OutboundLink
      href="https://www.gatsbyjs.org/packages/gatsby-plugin-segment-analytics/"
    >
      Visit the Segment Analytics plugin page!
    </OutboundLink>
  </div>
}
```

You can optionally provide an `eventName` and `categoryName` prop to
OutboundLink. This will change the segment event name (which is defaulted to
"Click"), and the category name (which is a property of the segment event),
respectively.

```js
<OutboundLink
  href="https://www.gatsbyjs.org/packages/gatsby-plugin-segment-analytics/"
  eventName="Visit External Link"
  categoryName="Gatsby Resource"
>
  Visit the Segment Analytics plugin page!
</OutboundLink>
```

## Special Thanks

This plugin was inspired by
[work from Stephen Mathieson](https://github.com/stephenmathieson/gatsby-plugin-segment).

## License

MIT
