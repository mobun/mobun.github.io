---
title: Showing RSS News with PnP Search
categories:
    - Microsoft 365
    - PnP Search
    - Power Automate
    - Microsoft Graph
---

Anyone who wants to make news from an RSS feed visible in Microsoft 365 quickly runs into the question of how those entries can be integrated into an existing search or portal experience in a sensible way. That is exactly where PnP Search becomes a pragmatic building block: there are several ways to prepare RSS content so that it appears as news or search results.

In practice, three approaches are worth considering. The first is to provide a custom datasource for PnP Search. The second is an indirect route through Power Automate, where RSS entries are turned into usable news links. The third option is to integrate the content through a Graph Connector when it should become a permanent and more structured part of Microsoft 365 search.

## 1. Custom Datasource in PnP Search

The most direct approach is to provide a custom datasource for PnP Search. This allows the search experience to be aligned closely with your own data model. The RSS feed is not just read as-is, but transformed into a shape that PnP Search can render directly.

At first glance, this may sound like the cleanest solution because everything stays under your own control. In practice, however, there is an important drawback: if the datasource accesses the RSS feed from the client side or from a browser-based environment, CORS errors can occur. Many RSS sources do not provide the necessary CORS headers, or they only allow requests from very restricted contexts.

That is the core risk. What still works in a local test may suddenly fail in the browser or in the production portal with a cross-origin issue. In that case, the search itself is not the problem; the direct access to the feed is.

Anyone choosing this route should therefore verify early whether the RSS endpoint is even reachable for direct requests. If it is not, you need either a proxy service or server-side processing so that search does not have to talk to the feed directly.

## 2. Processing RSS with Power Automate

A very practical alternative is Power Automate. The flow periodically reads the RSS feed and handles the processing of the entries. Each RSS item is then turned into a news link or a searchable record that can be reused in PnP Search.

The advantage of this approach is that it decouples the solution from direct feed access. Power Automate runs server-side and can collect the content, format it, and write it to a suitable target, for example a SharePoint list or another repository that PnP Search can read from.

This turns an unreliable real-time request into a robust processing pipeline. New RSS entries do not appear as a direct browser fetch from the feed, but as a controlled news item with title, link, date, and summary. That is especially useful when the news should feel like editorial content rather than technical raw data.

This approach is often the best compromise when you need results quickly and still want to avoid the typical CORS issues.

## 3. Integration through a Graph Connector

The cleanest long-term option is to integrate the RSS content through a Graph Connector. This brings the content into Microsoft 365 search in a structured way so that it can be queried and displayed consistently.

The major advantage of this option is that the data is not prepared for just one frontend. Instead, it becomes part of the Microsoft 365 search model. That makes it more robust, easier to maintain, and much better suited for larger scenarios than a purely client-side approach.

A Graph Connector is especially useful when RSS content should be more than just a display channel. If it needs to be available through search results, relevance ranking, metadata, and long-term discoverability, this is the most professional route.

The downside is the additional effort. Connectors need to be configured, maintained, and modeled properly. In return, you get a solution that fits cleanly into Microsoft 365 search and remains stable even as content volume grows.

## Conclusion

If the main goal is a quick and flexible display, Power Automate is often the most pragmatic starting point. If maximum control over the presentation matters, a custom datasource in PnP Search can make sense as long as RSS access does not fail because of CORS. And if the RSS content should become a permanent and structured part of Microsoft 365 search, a Graph Connector is the best choice.

Bottom line: the closer the solution needs to stay to the actual search experience, the more important reliability, data modeling, and authentication become. The RSS feed itself is usually not the problem. What matters is how you shape it into something that PnP Search and Microsoft 365 search can process safely.

Examples for all three approaches will be published in the coming weeks, with concrete samples for datasource configuration, Power Automate flows, and Graph Connector mappings.