---

copyright:
  years: 2015, 2020
lastupdated: "2020-04-29"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: EventStreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note: .note}
{:deprecated: .deprecated}
{:important: .important}

# Upgrading to the new {{site.data.keyword.messagehub}} Standard plan 
{: #migrate_classic_plan}

This new release of the Standard multi-tenant plan offers significant improvements in resiliency, functionality, and usability. For more information, see [New Standard plan blog announcement ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/blog/announcements/ibm-event-streams-releases-a-new-and-enhanced-standard-plan).<br/>
As part of the upgrade to the Standard plan, you must create a new Standard plan instance. You cannot upgrade or change an existing instance of the Classic plan.
{:important}


To migrate applications from the previous Standard plan (now called the Classic plan and deprecated) to the new plan, consider the following information.

The Classic plan is deprecated. From November 1, 2019, you can no longer provision new instances of the Classic Plan. <br/>However, existing instances will continue to be supported.
From June 30, 2020, the Classic Plan will be retired and no longer supported. Any instance of the Classic Plan still provisioned at this date will be deleted. 
{:deprecated}

Service instances are now provisioned as {{site.data.keyword.cloud_notm}} Services rather than as Cloud Foundry Services. This enables the service to support the latest {{site.data.keyword.cloud_notm}} standards and capabilities, including multi-zone deployments and granular access controls, but has implications for how the service is used. In particular, consider the following aspects:

## Creating, deleting, and listing services
{: #create_services}

As before, you can manage the lifecycle of services using either the {{site.data.keyword.cloud_notm}} console or the {{site.data.keyword.cloud_notm}} CLI command line tool. If you're using the console, services are now listed under **Services** instead of **Cloud Foundry Services**. 

If you're using the CLI, instances are managed using the resource commands. For example,  <code>ibmcloud resource service-instance-create</code>. This is instead of the **cf** commands, for example <code>ibmcloud cf create-service</code>.

## Controlling access
{: #controlling_access}

Authentication and authorization are now managed using the Cloud Identity and Access Management (IAM) service. As well as controlling a user's ability to connect, IAM also enables you to configure granular access to underlying resources, such as topics. Access is controlled by assigning policies to users. For more information, see 
[Managing access to your {{site.data.keyword.messagehub}} resources](/docs/EventStreams?topic=EventStreams-security).

## Connecting applications
{: #connecting_apps}

The information that an application needs to connect has not changed, that is, a list of <code>bootstrap.servers</code>, <code>username</code>, and <code>password</code> is required. However, the way these properties are retrieved has changed.


* **For native applications**<br/>
You must create a Credentials object using the IBM Cloud console or a Service Key object using the CLI. You can then retrieve the required properties. For more information, see 
[Connecting applications](/docs/EventStreams?topic=EventStreams-connecting#connect_enterprise_external).

* **For Cloud Foundry applications**<br/>
You must first bind the service to the application's organization and space by creating a service alias. You can then retrieve the required properties from the VCAP_SERVICES environment variable as normal. For more information, see 
[Connecting to {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-connecting).

<br/>
Note that clients must support the SNI extension to TLS where the server's hostname is included in the TLS handshake. This feature is commonly available and is supported in all the client versions recommended in [Choosing a Kafka client to use with {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-kafka_using#kafka_clients).

<br>
You should also be aware of some other changes as follows:
## Kafka version
{: #kafka_version}

This plan provides access to the latest stable Kafka release 2.3. Applications developed against Kafka 1.1 can run unchanged, but refer to the following information for recommended client versions and tested combinations: [Choosing a Kafka client to use with {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-kafka_using#kafka_clients). 

## Supported regions
{: #supported_regions}

The plan is available in the following regions:
* Dallas (us-south)
* Washington (us-east)
* London (eu-gb)
* Sydney (au-syd)
* Frankfurt (eu-de)
* Tokyo (jp-tok)

## Integrations
{: #integrations}

Connection from other services, such as {{site.data.keyword.iot_short_notm}} or {{site.data.keyword.openwhisk_short}}, which bind to the service using a Cloud Foundry organization and space require a service alias to be created. For more information, see
[Connect Cloud Foundry applications to {{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-connecting#connect_enterprise_cf).

## Supported capabilities
{: #capabilities}

There are differences between the capabilities of the Classic plan and the new Standard plan. To align the product offerings, adopt new technology choices, and remove less-used features, not all capabilities are carried forward. A comparison of the features is available at [Choosing your plan](/docs/EventStreams?topic=EventStreams-plan_choose). If you rely on these functions, use the following information to help you migrate.

* If you currently use the REST APIs on the Classic plan, see [Migrating the REST APIs](/docs/EventStreams?topic=EventStreams-migrate_rest_apis).
* If you currently use the {{site.data.keyword.mql}} API on the Classic plan, see [Migrating MQ Light to Kafka](/docs/EventStreams?topic=EventStreams-migrate_mqlight).
* If you currently use the Cloud Object Storage bridge or the MQ bridge, see [Migrating bridges to Kafka Connect](/docs/EventStreams?topic=EventStreams-migrate_bridges).

<br/>
Small code deltas are shipped daily to production. As a result, you can expect to see many further improvements to our user experience (and other areas).

<br/>



