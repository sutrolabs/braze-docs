---
nav_title: RudderStack
article_title: RudderStack
description: "This article outlines the partnership between Braze and RudderStack, an open-source customer data infrastructure that offers a seamless Braze integration for your Android, iOS, and web applications. With RudderStack, you can now send your in-app customer event data directly to Braze for contextual analysis."
page_type: partner
search_tag: Partner

---

# RudderStack

> [RudderStack][1] is an open-source customer data infrastructure for collecting and routing customer event data to your preferred data warehouse and dozens of other analytics providers, such as Braze. It is enterprise-ready and offers a robust transformation framework to process your event data on the fly.

The Braze and RudderStack integration offers a native SDK integration for your Android, iOS, and web applications, as well as a server-to-server integration from your backend services.

## Prerequisites

| Requirement | Description |
| --- | --- |
| RudderStack account | A [RudderStack account](https://app.rudderstack.com/) is required to take advantage of this partnership. |
| Configured source | A [source][3] is essentially the origin of any data sent to RudderStack, such as websites, mobile apps, or backend servers. You are required to configure the source before setting up Braze as a destination in RudderStack. |
| Braze REST API key | A Braze REST API key with `users.track`, `users.identify`, and `users.alias.new` permissions.<br><br>This can be created within the **Braze Dashboard > Developer Console > REST API Key > Create New API Key**. |
| Braze app key | To get your app key, navigate to **Braze Dashboard > Developer Console > Identification** and find your app name. Save the associated identifier string.
| Data center | Your data center aligns with your Braze dashboard [instance][15].  |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

## Integration

### Step 1: Add a source

To start sending data to Braze, you first need to make sure a source is set up in your RudderStack app. Visit [RudderStack][22] to learn how to set up your data source.

### Step 2: Configure destination

Now that you have your data source set up, in the RudderStack dashboard, select **ADD DESTINATION** under **Destinations**. From the list of available destinations, select **Braze** and click **Next**.

In the Braze destination, provide the app key, Braze REST API key, data cluster, and native SDK option (device mode only). The native SDK option will use the Braze native SDK to send events if toggled on. 

![][0]{: style="max-width:40%;margin-bottom:15px;"}

## Step 3: Choose the type of integration

You can choose to integrate RudderStack's web and native client-side libraries with Braze using either a side-by-side (device mode) integration or a server-to-server (cloud mode) integration.

- Integration type
  - [Side-by-side / device mode](#device-mode): RudderStack will send the event data to Braze directly from your client (browser or mobile application).
  - [Server-to-server / cloud mode](#cloud-mode): The Braze SDK sends the event data directly to RudderStack, which is then transformed and routed to Braze.

{% alert note %} 
Learn more about RudderStack's [connection modes](https://www.rudderstack.com/docs/destinations/rudderstack-connection-modes/) and the benefits of each.
{% endalert %}

### Step 3a: Side-by-side integration (device mode) {#device-mode}

With this mode, you can send your events to Braze using the Braze SDK set up on your website or mobile app.

Set up the mappings to the RudderStack SDK for [Android](https://github.com/rudderlabs/rudder-integration-braze-android), [iOS](https://github.com/rudderlabs/rudder-integration-braze-ios), or [React Native] on Braze's GitHub repository, as described in step 4. 

To complete the device mode integration, refer to the detailed RudderStack instructions for [adding Braze to your project](https://rudderstack.com/docs/destinations/marketing/braze/#adding-device-mode-integration).

### Step 3b: Server-to-server integration (cloud mode) {#cloud-mode}

In this mode, the SDK sends the event data directly to the RudderStack server. RudderStack then transforms this data and routes it to the desired destination. This transformation is done in the RudderStack backend, using RudderStack's Transformer module.

To enable the integration, you will need to map the RudderStack methods to Braze, as described in step 4.

{% alert note %} 
RudderStack's server-side SDKs (Java, Python, Node.js, Go, Ruby) support only cloud mode. This is because their server-side SDKs operate in the RudderStack backend and cannot load any Braze-specific SDK. 
{% endalert %}

{% alert important %} The server-to-server integration does not support Braze's UI features, such as push notifications or in-app messaging. These features are, however, supported by the Device Mode integration. 
{% endalert %}

## Step 4: SDK methods

Braze supports the RudderStack methods identify, track, page, and group.

### Identify

The RudderStack [`identify` method](https://rudderstack.com/docs/destinations/marketing/braze/#identify) associates a user to their actions. RudderStack captures a unique user ID and optional traits associated with that user, such as name, email, IP address, etc.

### Track

RudderStack's [`track` method](https://rudderstack.com/docs/destinations/marketing/braze/#track) captures all the user activities, along with the properties associated with those activities.

**Order completed**<br>
On using the [RudderStack eCommerce API][20] to call the track method for an event with the name `Order Completed`, RudderStack sends the products listed in that event to Braze as [`purchases`][21].

### Page

RudderStack's [`page` method](https://rudderstack.com/docs/destinations/marketing/braze/#page) allows you to record your website's page views. It also captures any other relevant information about that page.

### Group

RudderStack's [`group` method](https://rudderstack.com/docs/destinations/marketing/braze/#group) allows you to associate a user with a group.

[0]: {% image_buster /assets/img/RudderStack/braze_settings.png %}
[1]: https://rudderstack.com/
[3]: https://www.rudderstack.com/docs/dashboard-guides/sources/adding-source-and-destination-rudderstack
[15]: {{site.baseurl}}/user_guide/administrative/access_braze/braze_instances/
[20]: https://www.rudderstack.com/docs/event-spec/ecommerce-events-spec/
[21]: {{site.baseurl}}/user_guide/data_and_analytics/export_braze_data/exporting_revenue_data/#revenue-data
[22]: https://www.rudderstack.com/docs/destinations/streaming-destinations/braze/#getting-started
