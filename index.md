## REMP Technical news

**Technical announcements:** 

08-Aug-2022: Since CRM 2.0 and REMP 1.0 we've dropped support for PHP 7.4. Minimum supported version from now is PHP 8.0.

31-Mar-2022: Since CRM v1.0 and REMP tools v0.32 we've dropped support for MySQL 5.7. It's possible the CRM will work for you after this date, but you might encounter compatibility issues though.

### 23-Feb-2023: REMP tools release (1.2)

Today we also bring the new version of REMP tools. In Mailer we continue with internal updates (see info about `mail:migrate-user-subscriptions-and-variants`) and improve tracking of subscribe sources. In Campaign the most important feature is new set of settings for the campaign allowing you to configure what happens when users clicks/closes the banner (without using the Beam segments).

The full changelog is avilable [here](https://github.com/remp2020/remp/releases/tag/1.2.0).

### 23-Feb-2023: CRM release (2.3)

After some irregular updates in the recent months we will be trying to get back to more regular (monthly) release cycles. This CRM release might not look big, but for API-primary users of CRM it will be a huge performance improvement.

The full changelog is available [here](changelog/crm/2.3.md).

### 27-Jan-2023: REMP tools release (1.1)

This took a while, but there are features to look for. This release brings support for PHP 8.1 and couple of notable features:

- Campaign is now more focused on JS-banner use which is showing bigger potencial than we originally anticipated. We extracted JS editing from the inline input in the banner form to the separate modal window and added variable extraction for non-developers.
- Mailer now allows you to add your own variables that can be injected into the every email. See `ServiceParamsProviderInterface` in the Mailer's readme file.
- Mailer also need to make a bigger data migration in this release. The process is described in changelog. It's not blocking, but a bit time-intensive.

The full changelog is available [here](https://github.com/remp2020/remp/releases/tag/1.1.0).

### 27-Jan-2023: CRM release (2.2)

Main feature of this release is support for PHP 8.1, which can now safely to deploy the CRM. Otherwise this is again mainly stability release.

The full changelog is available [here](changelog/crm/2.2.md).

### 05-Jan-2023: CRM hotfix for Users and Subscriptions modules

The hotfix fixing the issues from 19-Dec-2022 should have included also release of Users and Subscriptions modules. We've just realized it was missing and it's available now for download.

### 19-Dec-2022: CRM hotfix for Admin, Application, REMP Mailer and SalesFunnel modules

Release is addressing changes in the `nette/di` package since version `3.1`. If you updated your project, you could see some deprecations that were fixed in this release.

### 30-Nov-2022: CRM hotfix for subscriptions, segment and salesfunnel modules (2.1.1)

Release is fixing bug preventing saving form when editing existing subscription type/segment/sales-funnel in administration.

### 25-Nov-2022: CRM release (2.1)

After the major release couple of months ago, we have a new version of CRM with performance and stability improvements.

- LazyWidgetManager is replacing old WidgetManager to handle widgets in CRM. Using "lazy widgets" should improve speed of your application, as only actually used widgets will now be initialized.
- We've improved processes behind scenarios pausing and removing.
- Also we've optimized evaluation of availability of upgrades.
- We attempted to clean address fields, which were not always handled as nullable in the past.

The full changelog is available [here](changelog/crm/2.1.md).

### 26-Sep-2022: REMP tools major release (1.0)

Finally, after few years of development, we have managed to release the first major stable release (1.0) of the REMP tools. 

The main change is that PHP 8.0 is now the required version in all tools.

The full changelog is available [here](https://github.com/remp2020/remp/releases/tag/1.0.0).

### 23-Sep-2022: Hotfix release of REMP tools (0.34.1)

Hotfix includes issue fix that prevents saving template with invalid syntax in Mailer.

The full changelog is available [here](https://github.com/remp2020/remp/releases/tag/0.34.1).

### 23-Sep-2022: New version of REMP tools (0.34)

This version is the last PHP 7.4 compatible release of the REMP tools. Changes:

- The only breaking change is in whitelisting of domains for replacers (e.g. RTM replacer) in Mailer.  
- Few minor fixes. 

The full changelog is available [here](https://github.com/remp2020/remp/releases/tag/0.34.0).

### 06-Sep-2022: CRM release (2.0)

Few months after the first major version comes CRM version 2.0, as we now follow semantic versioning more rigorously.
The two biggest changes are upgrade from PHP 7.4 to version 8.0 and switch from Latte v2 to v3.   

There are other major features added, such as:
- Universal search in the administration.
- Support for measurements - precalculated values which can be used in charts or any kind of period-based statistics.

The full changelog is available [here](changelog/crm/2.0.md).

[//]: # (Full changelog is available here and is split to the two sections: Nette 3 update-related section, and feature changes made since the 0.38. This update will be a bit harder due to the amount of breaking changes. Please follow the migration guide in order to successfully update your internal extensions.)

### 08-Aug-2022: New version of REMP tools (0.33)

This release includes couple of usability fixes and minor features, that were requested for a longer time:

- Mailer now finally has a delete features, so you can get rid old emails and templates which you don't need anymore.
- We've fixed the mobile layout, all of the tools should now look a bit better.
- Mailer has a new "allow list" feature that allows you to list patterns of emails eligible for receiving emails. This is primarily intended for staging and pre-production environments.
- Campaign now by default shows banner preview for mobile widths and allows you to toggle between desktop and mobile.

And more. You can check the full changelog [here](https://github.com/remp2020/remp/releases/tag/0.33.0).

### 13-Jul-2022: Hotfix release for CRM API module

We've identified an issue with `Access-Control-Allow-Credentials` header, which was not included in the all requests if it was configured. This release fixes the issue. ([info](https://github.com/remp2020/crm-api-module/releases/tag/1.2.1))

### 24-Jun-2022: CRM release (1.2)

This release is made primarily of one feature: Wallet pay support. Since this version, CRM contains new [wallet pay module](https://packagist.org/packages/remp/crm-wallet-pay-module), which brings support for Google pay and Apple pay payments through the gateway - mostly banks and big payment providers.

Our implementation brings the wallet pay payments with support of Tatrabanka (Slovak bank), but the module is extensible for other providers as well. Since the feature is new, please consider it as a nearly-production-ready and use with a bit of caution.

This version also brings German translations, kudos to [alexmerz](https://github.com/alexmerz) for all the effort.

The full changelog is available [here](changelog/crm/1.2.md).

### 10-Jun-2022: Hotfix version of REMP tools (0.32.6)

Since today, Mailgun started to enforce additional checks on their API which broke non-batch sending of emails. If you encounter an error when sending the system emails through the Mailgun, please update immediatelly.

The changelog and error description is [here](https://github.com/remp2020/remp/releases/tag/0.32.6), and [this is the commit](https://github.com/remp2020/remp/commit/dc1adc1f9752db5671f4e22c8bc5739b4ba515f7) explaining the issue.

### 02-Jun-2022: CRM release (1.1)

After more than a two months we bring new version of the CRM. This is more-or-less stability / minor features release. Make sure you go through the changelog to see if any of the features/changes interest you.

Full changelog is available [here](changelog/crm/1.1.md).

### 26-May-2022: Hotfix version of REMP tools (0.32.5)

The newest version of Latte templating engine started to trigger deprecation notices for one of the Mailer internal features. This version fixes the deprecation warning and filterLoader issue.

See the changelog [here](https://github.com/remp2020/remp/releases/tag/0.32.4).

### 11-May-2022: Hotfix version of REMP tools (0.32.2)

We've accidentally made a breaking change in one of our APIs which forced us to release this hotfix version. Since we were able to merge couple of other minor fixes/notices since the last version, this release contains breaking-change fix and also couple of minors.

See the full changelog [here](https://github.com/remp2020/remp/releases/tag/0.32.2).

### 02-May-2022: New version of REMP tools is available (0.32)

It's been a couple of weeks since the latest release and REMP tools bring couple of nice features:

- Beam Tracker now supports Cloud Pub/sub that can be used as a queue for tracked events and possibly replace Kafka cluster.
- The way how Mailer generates batch queues was rewritten to avoid table locking observed on the bigger instances.
- Mailer adds List-Unsubscribe header, so the e-mail clients can display native unsubscribe links.
- Mailer now supports localization for regular one-time emails. We'll be adding localization for jobs in the future.

You can see the full changelog [here](https://github.com/remp2020/remp/releases/tag/0.32.1).

### 31-Mar-2022: Major CRM version release (1.0)

After years of features and months of refactorings, we're happy to annouce that the CRM is stable enough for major version 1.0. Internally we updated the underlying framework and API library, to bring you better features in your modules.

Full changelog is available [here](changelog/crm/1.0.md) and is split to the two sections: Nette 3 update-related section, and feature changes made since the 0.38. This update will be a bit harder due to the amount of breaking changes. Please follow the [migration guide](https://github.com/remp2020/crm-application-module/blob/master/MIGRATION.md) in order to successfully update your internal extensions.

### 14-Mar-2022: New version of REMP tools is available (0.31)

This release brings some useful features to Beam and Mailer:

- Beam can now display non-article URLs instead of one "Landing page" entry. For this feature to work, your site needs to correctly set canonical URLs.
- Mailer's WYSIWYG editor now automatically formats HTML. We also brought full screen mode for email editing.

Full changelog is available [here](https://github.com/remp2020/remp/releases/tag/0.31.0).

### 26-Feb-2022: Hotfix release for REMP Tools (0.30.2)

We've received a report for XSS vulnerability present on the SSO login error callback page. This error was present in the all previous versions of REMP tools and affected Beam, Campaign and SSO. Please update your REMP tools to prevent the vulnerability misuse. ([changelog](https://github.com/remp2020/remp/releases/tag/0.30.2))

### 22-Feb-2022: Hotfix release for REMP Beam (0.30.1)

We've received couple of bugreports in Beam. One related to the conversion event aggregation (which could miss some events prior to conversion) and author/section segment calculation (which could take couple of hours). We recommend to upgrade to this release. ([changelog](https://github.com/remp2020/remp/releases/tag/0.30.1))

### 11-Feb-2022: New version of CRM is available (0.38)

We pushed this release as late as possible. This might also be the last release before major update to v1.0. There are couple of important changes in this version:

- We now officialy support and recommend Redis 6.2. If you're on the older version, you should be fine for now, but we won't be able to test Redis 3 as we were until now.
- Users module now supports "preregistration" flow, which breaks couple of breaking changes. This flow is intended for systems with imported users, which you need to track for internal purposes, but their account shouldn't be activated yet.
- CRM now includes partial Hungarian translation thanks to the great work of [Brainsum](https://brainsum.com). We hope to cover more of this translation in the following weeks and months.
- Stats in the scenario builder have been refreshed and are now much more usable than before.

You can check the full changelog [here](changelog/crm/0.38.md).

### 10-Feb-2022: New version of REMP tools is available (0.30)

Almost three months passed since the latest version, yet this is mainly a maintenance release:

- Google fonts are no longer used in the Campaign banners due to the legal changes and pagespeed affection.
- It's now possible to configure error tracking sample rate for Campaign's showtime request.
- Mailer's subscribe API now accepts variant_code when manipulating the subscription.

And numerous fixes and optimizations. Head to the [changelog](changelog/remp/0.30.md) to see all of the changes in this version and don't forget to also update your Tracker and Segment API binaries (available [here](https://github.com/remp2020/remp/releases/tag/0.30.0)).

### 01-Feb-2022: Hotfix release for Salesfunnel module (0.37.1)

Handling of sales funnel meta values got broken in the latest release and CRM was not able to save new funnel. If you use this flow to create new funnels (opposing to using seeders), please update to the latest version. ([changelog](https://github.com/remp2020/crm-salesfunnel-module/releases/tag/0.37.1))

### 24-Jan-2022: Hotfix release for Scenarios module (0.37.1)

CRM was generating notices on scenarios detail because of the dependency on the currently-internal module. Please update the `crm-scenarios-module` to fix this issue. ([changelog](https://github.com/remp2020/crm-scenarios-module/releases/tag/0.37.1))

### 09-Dec-2021: New version of CRM is available (0.37)

Main features of this release are:

- Changes related to the Payments module allowing publishers to gain more control over payments right before the payment is charged. This brings possibilities for custom wallet implementation and more.
- Deletes for products.
- API to delete the CRM (primarily intended for mobile apps).
- Stability improvements.

Check the [changelog](changelog/crm/0.37.md) to see the full list of changes and upgrade information.

### 07-Dec-2021: Hotfix release for Subscriptions module (0.36.1)

The query generated by SubscriptionTypeLength scenario criteria was incompatible with MySQL 8 and could cause DB execution errors. Please update your `crm-subscriptions-module` to `0.36.1`. ([changelog](https://github.com/remp2020/crm-subscriptions-module/releases/tag/0.33.1))

### 18-Nov-2021: New version of REMP tools is available (0.29)

Another two months passed by and a lot features landed in this release:

- Welcome email when user subscribes to the newsletter.
- Support for Redis Sentinel across all of the applications.
- New Mailer's job/batch option to prepare queue for sending without actual sending to see how many users will receive an email.
- Beam's property filter now correctly filters all of the data screens (not only the main dashboard).

And much more. Head to the [changelog](changelog/remp/0.29.md) to see all of the changes in this version and don't forget to also update your Tracker and Segment API binaries (available [here](https://github.com/remp2020/remp/releases/tag/0.29.0)).

### 18-Nov-2021: New version of CRM is available (0.36)

This time it's more about internal improvements and bugfixes.

There's one note-worthy _experimental_ feature to mention: Google/Apple pay payments in combination with Stripe gateway. We're currently testing the implementation and we'll probably be extending this in the future so it can be used with Tatrabanka. Stay tuned.

Check the [changelog](changelog/crm/0.36.md) to see the full list of changes and upgrade information.

### 26-Oct-2021: Hotfix release for ApplicationModule

Previous version optimized and speed up API. Unfortunately it introduced bug which breaks initial CRM installation _(application is unable to create required tables)_. This hotfix release contains fix for `Core::command()`. Update your `crm-application-module` to `0.35.1` ([changelog](https://github.com/remp2020/crm-application-module/releases/tag/0.35.1)).

### 25-Oct-2021: New version of CRM is available (0.35)

This release focuses mainly on improving stability, but brings some interesting features.

- Bump of minimal version of PHP to 7.4.
- Fix of inefficient API handler initialization, possibly improving speed of all API endpoints.
- Support for Redis Sentinel.
- New Scenario A/B test element.

Check the [changelog](changelog/crm/0.35.md) to see the full list of changes and upgrade information.

### 06-Oct-2021: New version of CRM is available (0.34)

This is mainly maintenance release focusing on improving existing features. The main improvements are:

- Significant speed up of Scenario and Hermes workers. You can now also configure min/max idle times for the worker in case you're not satisfied with the provided defaults.
- Upgrades now support upgrade of subsequent subscriptions. Up until now, only the actual subscription was upgraded and any following subscription would remain untouched. This version brings support for upgrade of subsequent subscriptions if they have same subscription type as upgraded subscription.
  - This feature is not enabled by default and you need to enable it manually. See [README](https://github.com/remp2020/crm-upgrades-module/#subsequent-upgrades) for more information.
- Audit log had a bug which caused the transition from _some value_ to _NULL_ not to be tracked correctly.

There's more, including couple of breaking changes that might affect your own modules. Head to the [changelog](changelog/crm/0.34.md) to see the full list of changes and upgrade information.

### 28-Sep-2021: Hotfix release for SubscriptionsModule

Form for managing subscription types is extendible through data-providers. Unfortunately due to a bug the data-providers were not correctly handled during the form submission process. Update your `crm-subscriptions-module` to `0.33.1` ([changelog](https://github.com/remp2020/crm-subscriptions-module/releases/tag/0.33.1)).

### 09-Sep-2021: New version of REMP tools is available (0.28.0)

This is another bigger release, which took us more than two months to finalize. The main improvements are:

- Public preview support of emails in Mailer.
- Mailer application status widget displaying whether all background services are running correctly.
- Campaign now support pageview attributes in configuration for easier campaign targetting (based on the attributes provided by client web page).
- Campaign also supports definition of global variables, which can be included in banner body, JS/CSS snippets and also external JS/CSS URLs.
- Tracker now automatically tracks canonical URL for each pageview (if it's available).
- Property filter in Beam now filters data in all of the Beam sections, not just the main dashboard.

And much more. Head to the [changelog](changelog/remp/0.28.md) to see all of the changes in this version and don't forget to also update your Tracker and Segment API binaries (available [here](https://github.com/remp2020/remp/releases/tag/0.28.0)).

### 09-Sep-2021: Another hotfix for ApplicationModule

Recently CRM added support for read-only connections in case you have multiple database replicas. In case you haven't configured the connection yet, the Heartbeat handler (trigerred by `application:heartbeat`) command would crash. This release fixes the issue. ([changelog](https://github.com/remp2020/crm-application-module/releases/tag/0.33.2))

### 08-Sep-2021: Hotfix release for ApplicationModule

There have been issues reported with access to CRM admin caused by external translation libraries. Please update your `crm-application-module` to `0.33.1`. ([changelog](https://github.com/remp2020/crm-application-module/releases/tag/0.33.1))

### 23-Aug-2021: New version of CRM is available (0.33)

It's been a while since the last release. The main improvements in this version are:

- More fine-grained ACL control for administration.
- Apple sign-in support.
- Additional scenario criteria, this time mainly for ProductsModule.

There's more, including couple of breaking changes, so head to the [changelog](changelog/crm/0.33.md) to see the full list of changes and upgrade information.
