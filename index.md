## REMP Technical news

**Technical announcements:** 

**29-Apr-2025**: REMP 4.0 dropped support for PHP 8.1 and requires PHP 8.2 or newer. We recommend using PHP 8.3 in production environment.

**03-Apr-2025**: CRM 4.0 dropped support for PHP 8.1. CRM now requires PHP 8.2 and newer. We recommend using PHP 8.3 in production environment. Minimum MySQL version (due to features we might require in some of our modules) is 8.0.31.

**04-Sep-2024**: Since REMP tools v3.9, the primary Elasticsearch version we support is v8. We made sure that there's backwards compatibility with the v7, so you still have time to upgrade your database. The compatibility will only be enforced by the end of this year. After January 2025 the compatibility will most likely still be in place, but will not be guaranteed by us.

### 27-Jun-2025: REMP release (4.1)

This is a pretty important release, two big features come in this version:

- Campaign now finally has its own skeleton application. We strongly recommend to migrate from monorepo to the skeleton (https://github.com/remp2020/campaign-skeleton).
- Beam now supports impression tracking - it can store elements that your users saw on the website to Elasticsearch. The feature is disabled by default and experimental, but it can be enabled with JS config (see https://github.com/remp2020/remp/blob/master/Beam/README.md). More documentation will come in the following releases.
  - For now it only stores the data and it's up to you to evaluate them if you ever need to.
- Other fixes and improvements.

In order for this version to function correctly, you need to upgrade your Telegraf installation to the v1.31.1.

The full list of changes is available [here](https://github.com/remp2020/remp/releases/tag/4.1.0).

### 27-Jun-2025: CRM release (4.2)

In this version we bring nicer object history for CRM admin users. You no longer need to go to the audit log page, but CRM provides a history log widget and also a way how to attach to the existing implementations of widgets (for payments, subscriptions, and shop orders and products. Visit their detail pages to see the new feature.

- CRM now allows to store cardholder name for payment cards if your gateway provides such information.
- Products module (eshop) now allows to specify global postal fee conditions if you ever need to make some postal fee available only conditionally.
- Scenarios now validate if you filled the condition elements correctly.
- And other fixes and improvements.

You can see the full changelog [here](changelog/crm/4.2.md).

### 25-May-2025: CRM release (4.1)

This release contains mainly quality of life improvements and fixes, that benefits mainly the installations extending the CRM.

You can see the full changelog [here](changelog/crm/4.1.md).

### 29-Apr-2025: REMP release (4.0)

Finally, we are releasing the 4.0 of our REMP tools. This release brings lots of internal breaking changes, so if you extended any of the modules, please read the Changelog thoroughly. 

- The minimum supported version now is PHP 8.2 and recommended version is 8.3.
- We've upgraded underlying libraries and the Laravel framework to their latest version. We had significant technical debt here which is now gone.
- Laravel made some changes, including slimming the skeleton application. We are doing this as well, but you don't have to do it immediately:
  - The minimum upgrade path for you is displayed in [this commit](https://github.com/remp2020/beam-skeleton/commit/85a24b77fe2898600421f4e1d31f739ad1982054).
  - To get to the latest skeleton version, please apply changes from [this commit](https://github.com/remp2020/beam-skeleton/commit/fc215048d307eb041908f516857ce32bb0609287).
  - When removing middlewares, please make sure you apply any of your internal changes to the `bootstrap/app.php` file (the `->withMiddleware()`) call.
- We've updated Elasticsearch and Telegraf docker images to use the newer versions - Elasticsearch 8.6.1 and Telegraf 1.31.

Apart from that, there are minor improvements and bugfixes across all modules, feel free to go through the Changelog and review them [here](https://github.com/remp2020/remp/releases/tag/4.0.0).

### 03-Apr-2025: CRM release (4.0)

It took us couple of more months to finish, but CRM 4.0 is here.

- We updated majority of our dependencies.
- Minimum supported PHP version is now 8.2, recommended for production is 8.3.
- There are lot of breaking changes (due to dependencies update) that you need to review before upgrading. All of them are summarized in the Changelog. We tried to add new Rector rules to ease the upgrade, review the latest version of [CRM rector module](https://github.com/remp2020/crm-rector).
- We deprecated iframe-based use of sales funnels. We highly recommend to use direct funnels. See [README](https://github.com/remp2020/crm-salesfunnel-module#iframe-deprecation-in-sales-funnels).
- We started implementation on full refunds. System now allows you to implement `RefundableInterface` in your payment gateways which allows direct refunds from the system. At the moment, none of the open-sourced gateways implement this, internally we use it for our Trustpay integration.

There's more, mainly bugfixes that we found during the upgrade. As always, but this time even more, please review the full list of changes available [here](changelog/crm/4.0.md). We've also made some [changes in the Skeleton app](https://github.com/remp2020/crm-skeleton/commit/a69eaccb20cb255738de6025b2d42dc6ebbda4a7), you might want to port them to your projects as well.

### 04-Feb-2025: REMP release (3.11)

Similar to CRM, we are making one last v3 REMP release before we move on to v4 with some breaking changes. This version includes:

- Accessibility improvements of Campaign banners (contrasts, screen reader labels).
- Ability to extend Campaign's color schemes to include your own.

Release contains some additional fixes and improvements, the full list of changes is available [here](https://github.com/remp2020/remp/releases/tag/3.11.0).

### 04-Feb-2025: CRM release (3.7)

Eventhough we declared that the 3.6 would be the last 3.*, we needed to make one more release as the work on v4 got delayed. Here's what's new:

- We completely changed underlying JS library for scenarios, allowing us to make easier improvements for UI in the future.
- You can now create gift subscriptions in CRM Admin (if you use gifts-module).
- Fixed things related to changing payment country and VAT in CRM Admin.

As usual, there are smaller changes and fixes, and some possibly breaking changes for those who extend the CRM. You can see the full changelog [here](changelog/crm/3.7.md).

### 28-Nov-2024: CRM release (3.6)

This version is primarly finance-featured.

- One Stop Shop (OSS) mode is now generally available. Please read about [VAT in EU](https://github.com/remp2020/crm-payments-module/blob/master/README.md#one-stop-shop) and about [how to get VAT rates into the system](https://github.com/remp2020/crm-payments-module/blob/master/README.md#european-union-vat). The mode is disabled by default. Enable it only after consulting with your accounting department and agreeing on the launch date, and making sure your sales funnels can provide payment country to backend. Once enabled, each payment **must** have the country assigned.
- System now also supports multiple VAT modes (B2B, B2C, B2B reverse charge) and Invoices module implements the default behavior. If we recognize that your CRM is in the EU and you enabled VAT rates update from the previous step, CRM will deduct VAT for B2B purchase within EU where applicable. This is enabled by default, but if you need more control, you can implement your own `VatModeDataProviderInterface` ([docs](https://github.com/remp2020/crm-payments-module?tab=readme-ov-file#vat-modes)).
- On backend we made some notable improvements with the transactions. CRM repositories now provide application-level transactions, which we heavilly recommend to use. They make sure, that you never start the transaction twice within your request, and also postpone Hermes event emitting until the transaction is commited. If the transaction is rollbacked, Hermes events are thrown away.
- Due to security reason, we needed to upgrade `twig` templating system used in the sales funnels to v3. Please see the changelog and review the deprecations from the v2.

Please be aware that this is the last 3.* version. Next version will (as announced earlier) drop support for PHP 8.1, raise minimum version for MySQL to 8.0.31, and bring some possibly breaking changes.

You can see the full changelog [here](changelog/crm/3.6.md).

### 25-Oct-2024: REMP release (3.10)

Today we're also releasing new version of REMP. In Beam, we focused on some compatibility issues with Elasticsearch 8. Campaign got first batch of accessibility improvements, more will came in the following release. And Mailer received couple of bugfixes and improvements as well, see the changelog.

The full list of changes is available [here](https://github.com/remp2020/remp/releases/tag/3.10.0).

### 25-Oct-2024: CRM release (3.5)

We have new CRM release ready. The One Stop Shop mode is fairly tested and stable at this moment, but we're still missing one important feature - B2B reverse charge mode which would allow 0% VAT purchase for the businesses within EU. We decided to hold the documentation for now and we'll release everything together. If you would like to use OSS anyway, let us know and we'll guide you forward.

This version brings more or less stability changes:

- Internal changes allowing us management of payment methods in the future - we're moving CIDs from the recurrent payments to their own table. Because of this migration, we'll need you to run `payments:migrate_payment_methods` command after the release to make sure everything was migrated correctly.
- Bugfixes and improvements for specific system events, we recommend you to review the changelog.

You can see the full changelog [here](changelog/crm/3.5.md).

### 20-Sep-2024: CRM release (3.4)

It took more than two months to release the new version of CRM, but we hope it was worth it. We're working on the support for One Stop Shop mode in EU, which allows you to charge your users VAT rate dependning on their country. At the moment it's not completely finished yet, since we still need to work on foreign B2B sales. The full support with the documentation will be available next month.

These changes forced us to do some major refactorings and they caused some breaking changes. Please go through the changelog (mainly the `PaymentsModule`) and verify that these changes don't break something for you.

The noticable features of this release are:

- You can now transfer subscriptions (together with their payments and recurring payments) between two accounts.
- Localizable countries lists. You can now configure the CRM to display lists of countries in user's language. It's a opt-in feature, it might change in the future. You can change the setting in the CRM admin.
- Family (company) module now correctly handles recurring charges of master payments.
- VAT rates are now decimal.
- There is new trigger in scenarios which generates events before a recurrent payment's card expiration.
- Fixed the slower performance of Login API introduced in 3.0.

You can see the full changelog [here](changelog/crm/3.4.md).

### 04-Sep-2024: REMP tools release (3.9)

We managed to successfully upgrade to Elasticsearch 8 during the summer months. The upgrade was farely easy and we only needed to follow official [upgrade guide](https://www.elastic.co/guide/en/elastic-stack/8.14/upgrading-elasticsearch.html). To use the latest version of Elasticsearch, please upgrade Tracker API, Segments API, and [Telegraf](https://github.com/remp2020/telegraf/releases/tag/v1.31.0).

Thanks to our friends from Fatchilli, we also made changes necessary to split Campaign to the separate skeleton app in the near future. The Campaign is already extracted into its own [module](https://packagist.org/packages/remp/campaign-module) and we now wait for the skeleton app to be ready. Becasue of that, there are some important changes to follow/check before upgrading in the [Campaign's changelog](https://github.com/remp2020/campaign-module/releases/tag/3.9.0), please make sure you read them.

The full list of changes is available [here](https://github.com/remp2020/remp/releases/tag/3.9.0).

### 12-Jul-2024: REMP tools release (3.8)

In this version we bring improvements to the Mailer UI, Beam dashboard and add support for Elasticsearch 8 into the Segments and Tracker APIs. Eventhough the update is not mandatory for this release, we highly recommend to do it so you are future-proof. We remind that the Elasticsearch 8 update is imminent and should happen by the end of the summer / beginning of the fall. 

- Mailer now supports full screen preview for text emails and the UI has been polished.
- Manipulation with Mailer's newsletters have also improved.
- Chart library in Mailer was updated and the charts have now slightly improved look.
- Beam dashboard now displays percentage of mobile traffic next to the active concurrents.

Full changelog is available [here](https://github.com/remp2020/remp/releases/tag/3.8.0).

### 12-Jul-2024: CRM release (3.3)

This version brins changes, that will allow us to support One Stop Shop scheme in the EU. In fact, we already support this internally and test it on our installations. If nothing special emerges, we expect to open-source the full support in the following releases. You might see stuff related to One Stop Shop in the changelog, none of it is actually live yet and we recommend not to enable it.

Apart from the One Stop Shop changes, this version includes:

- Automatic reload of configs for long-running jobs/daemons.
- Major refactor of recurrent payments charging, which allows us to add extra payment items to the recurrent payments.
  - For example, you can now add additional postal fee items to your subscriptions based on the user's country, and this fee will be included also in the recurrent charges. This was not possible so far.
- Sales funnels now support system translations via `|trans` filter.
- You can now use Twig in `header_block` and `sales_funnel_header_block` config options, and for `head_script` in each of the sales funnels.
- We also added extra trait `SalesFunnelTwigSnippetLoaderTrait` that helps you loading and providing snippets into your funnels.

The rest is mainly improvements and minor fixes. You can check the full changelog [here](changelog/crm/3.3.md).

### 27-May-2024: REMP tools release (3.7)

No new features in this release, but couple of notable technical improvements:

- If you use non-zero Redis database, please read the README as one of the fixes in the `RedisClientTrait` are important for you.
- Mailer received `application:cleanup` command that removes obsolete data from the database. Please add it to your scheduled tasks to be run at least once a day.
- Mailer is now able to reload configuration on-the-fly. Up until now, workers needed to be restarted if the config changed. That's not necessary anymore.
- There's a new segment in Mailer called "everyone", that should replace necessity of calling CRM to get the list of all users if you needed it.
- Tracker's and Segment's underlying library (Goa) was updated to the latest version. There are no visible changes.

Full changelog is available [here](https://github.com/remp2020/remp/releases/tag/3.7.1).

### 24-May-2024: CRM release (3.2)

After 2 months, CRM brings some notable changes that took us some time to deliver.

- Scenarios are now capable of validate the connections. From now on, you won't be able to save the scenario if you system detects that trigger doesn't provide parameters required by some of the conditions down the road.
- Because of this, we added new `TriggerManager` to scenarios. If you implement your own triggers, please see the [changelog](https://github.com/remp2020/crm-scenarios-module/releases/tag/3.2.0).
- We also managed to upgrade processing of Apple's server to server notifications. If you use AppleAppstoreModule, please see the new configuration options that are required for the module to work correctly. It's also recommended to change notification versions from v1 to v2 in the Apple developer account settings for the app and point it to the `/api/v2/apple-appstore/webhook` endpoint.
- This version also brings some security and performance improvements.

We advise to review the full changelog available [here](changelog/crm/3.2.md).

### 24-Apr-2024: REMP tools release (3.6)

This release brings interesting feature in Campaign and some minor updates in other tools.

- Campaigns can now targeted based on the session referal. That means that if your visit comes from the Facebook, you now have an option to target the whole visit instead of just the first pageview.
- Mailer and Beam now refresh their configs on-the-fly, it's not necessary to restart workers after the config change anymore.
- Mailer now supports One-Click unsubscribe according to RFC8058, see README for more information.
- Beam could be slow when displaying data tables for systems with many authors and tags. (Thanks **SME.sk** for debugging this)

Full changelog is available [here](https://github.com/remp2020/remp/releases/tag/3.6.0).

### 13-Mar-2024: CRM release (3.1)

After 6 weeks, we have new CRM release with some notable new features:

- You can now nest segments in other segments (both in queries and UI editor). The query editor also received syntax highlighting.
- CRM now adds more complex refund process, which will be extended in the future. Refunds now direct you to the separate form and stop subscription and recurrent payment immediately.
- Any updated `ActiveRow` object can now provided its state before the update thanks to integrating `OriginalAwareInterface`.
- Global admin search can search by invoice number.
- Subscription extension can now use address as a parameter to determine when the new subscription should start.

We advise to review the full changelog available [here](changelog/crm/3.1.md).

### 23-Jan-2024: REMP tools release (3.5)

This time it's a very minor update, since most of our efforts were directed to the CRM.

- Mailer updates some major dependencies, please check the changelog if you extend it.
- Mailer fixes memory issue on the job detail.
- Campaign fixes a bug that caused segments to be removed from the original campaign if it was copied.
- Fixed issus with HTTP 404 errors during login process in some scenarios.

We've also updated our skeleton apps (Mailer, Beam) to use PHP 8.2 by default. That's the version of PHP we recommend to use from now on.

Full changelog is available [here](https://github.com/remp2020/remp/releases/tag/3.5.0).

### 22-Jan-2024: CRM release (3.0)

After two months of updates and refactorings, we're finally able to release version 3.0 of REMP CRM. 

This version brings lots of internal updates and breaking changes - if you are a developer extending CRM with your own modules, please pay attention to everything marked as **BREAKING** and **IMPORTANT** within the changelog. Minimum supported version of PHP is now 8.1 and we plan to raise minimum version of MySQL in the next major release (4.0). The most cumbersome changeset of this release - PSR4 refactoring - is covered by Rector rules and the fix can be automated on your side.

Feature-wise this is a standard update release, with couple of notable ones:

- Google Play Billing payment gateway is now marked as recurrent. In order to generate past records, please run `google:create-missing-recurrent`.
- Google Play Billing now correctly handles "void purchase" scenario.
- Thanks to VAT change in Czechia, we were able to catch couple of edge cases related to the change.
- You can now suppress _subscription end_ trigger in scenarios per each subscription separately. And we fixed some bugs in scenario conditions too.

Updates in the Skeleton app (https://github.com/remp2020/crm-skeleton/):

- In the base CRM skeleton app, we updated the PHP Docker image to PHP 8.2 - that is the version we currently use in production and recommend to use.
- In `app/bootstrap.php` change application initialization to `$application = new Crm\ApplicationModule\Application\Core(dirname(__DIR__));`. _(namespace change)_
- In `bin/command.php` change application initialization to `$application = new Crm\ApplicationModule\Application\Core();`. _(namespace change)_
  - This can be covered by Rector, but you might possibly want to change it manually sooner.
- In `app/config.neon` change definition of `ConfigExtension` to `local_configs: Crm\ApplicationModule\Config\ConfigExtension`.
  - This can be covered by Rector, but you might possibly want to change it manually sooner.
- In `app/config.local.neon`, if you kept the original set of populators, replace `Populator` with `Populators` within their namespaces.

You can see all of those changes commited here: https://github.com/remp2020/crm-skeleton/commit/4d115a560c0b3d6160aff8158bc38ab3a5a0d372

The full changelog is available [here](changelog/crm/3.0.md).

### 23-Nov-2023: REMP tools release (3.4)

- Thanks to contribution from [@pulzarraider](https://github.com/pulzarraider), Campaigns got a significant performance boost. We've also merged an experimental PhpRedis support, which can be enabled via `.env` file. We haven't tested it in production and it doesn't support Redis Sentinel, so use it at your own risk.
- Mailer and Campaign received some minor improvements and bugfixes.
- And we've also fixed a bug in SSO which caused occasional 404 after login redirects.

Full changelog is available [here](https://github.com/remp2020/remp/releases/tag/3.4.0).

### 21-Nov-2023: CRM release (2.11)

This release focuses on bringing some smaller features developed to one of our clients and made available open-source.

- Users module fixes session-based bug that could appear when user switched accounts elsewhere (by having different `n_token`) and the first account was kept signed in in CRM.
- Google Play Billing module now correctly handles grace periods (if they're enabled for subscription in Google Play Console).
- Admin filter can now search against Google Play order ID / Apple original transaction ID.
- Some improvements within the PrintModule, mainly possibility to differentiate which countries should only be included within the export.

The full changelog is available [here](changelog/crm/2.11.md).

### 03-Oct-2023: REMP tools release (3.3)

- Campaigns can now be targeted by user's language, not just his current geo-ip-based country.
- Beam can now track custom URLs and referers if necessary (they're extracted automatically by default).
  - Please update Tracker API before you use this feature.

Full changelog is available [here](https://github.com/remp2020/remp/releases/tag/3.3.0).

Due to the changes in underlying framework, we were force to quickly release a hotfix for Mailer with some possibly breaking changes. See the changelog [here](https://github.com/remp2020/mailer-module/releases/tag/3.3.1).

### 03-Oct-2023: CRM release (2.10)

This release brings performance and visual improvements. The notable are:

- CRM admin now has dedicated detail (read-only) pages for subscription and payment.
- New `LazyEventEmitter` allows us to defer initialization of event handlers and speed up all requests to CRM. You can either replace the registration manually, or use our Rector rule to do that automatically for you.
  - In your main module classes, replace use of:
    ```
    public function registerEventHandlers(Emitter $emitter)
    ```
    with the replacement method:
    ```
    public function registerLazyEventHandlers(LazyEventEmitter $emitter)
    ```
  - Or use our newly added Rector rule: [https://github.com/remp2020/crm-rector](https://github.com/remp2020/crm-rector#transform-to-lazy-event-listeners)
- API logger can now log responses if necessary (custom implementation needed).

The full changelog is available [here](changelog/crm/2.10.md).

### 24-Aug-2023: REMP tools release (3.2)

New minor version brings mostly fixes to Beam _(related to Beam skeleton)_ and project changes (docker & docker compose changes and fix for yarn link not being able to link JS packages).

Full changelog is available [here](https://github.com/remp2020/remp/releases/tag/3.2.0).

### 24-Aug-2023: CRM release (2.9)

Important changes:

- Added _locale_ parameter to snippets to support different translations within one snippet.
- Removed restriction for administrators to generate invoice only if invoice address has company ID
- Added support for calculating recurrent payment charge time for payments without subscription. (`charge_at` is calculated from `payment->paid_at` and `subscription_type->length`).
- Added audit log for changes to ACL repositories.

All changes are listed in [changelog for v2.9](changelog/crm/2.9.md).

### 16-Aug-2023: REMP tools hotfix release (3.1.3)

Our friends from Petit Press reported some issues when using Yarn 3. This release fixes two issues that could occur if you used Yarn 3 to install dependencies instead of (tested) Yarn 2. If you encounter any issues, update to this version.

Full changelog is available [here](https://github.com/remp2020/remp/releases/tag/3.1.3).

### 11-Aug-2023: REMP tools hotfix release (3.1.2)

During testing of Beam Skeleton (now with the complete Docker Compose!) we've found out that there are background schedules missing and couple of other minor issues. If you started to work with Beam Skeleton, please update `remp/beam-module` to the latest version.

We also recommend to check the updated version of Beam Skeleton, since it now provides all dependencies within Docker Compose (there's no need to install them manually) and also testing article with example how to include JS snippet into the page and which APIs are mandatory to call when you want to use Beam.

Full changelog is available [here](https://github.com/remp2020/remp/releases/tag/3.1.2).

### 25-Jul-2023: REMP tools release (3.1)

This version brings mainly stability improvements including couple of bugfixes.

The most notable feature of the release is that Mailer now has the option to notify REMP CRM that user's mail subscription changed. This one is important for people using CRM's user data cache (in Redis), as people's mail subscription might be updated directly in Mailer and CRM wouldn't know about this change. To enable this feature, register the handler to these Hermes events:

```neon
services:
	hermesWorker:
		setup:
			- add('user-subscribed', Remp\MailerModule\Hermes\NotifyCrmSubscribeUnsubscribeHandler())
			- add('user-unsubscribed', Remp\MailerModule\Hermes\NotifyCrmSubscribeUnsubscribeHandler())
			- add('user-subscribed-variant', Remp\MailerModule\Hermes\NotifyCrmSubscribeUnsubscribeHandler())
			- add('user-unsubscribed-variant', Remp\MailerModule\Hermes\NotifyCrmSubscribeUnsubscribeHandler())
```

The full changelog is available [here](https://github.com/remp2020/remp/releases/tag/3.1.0).

### 24-Jul-2023: CRM release (2.8)

This month brings mainly usability and performance improvements within CRM:

- Getting IDs of users in bigger segments should now be less memory-heavy.
- It's now possible for admins to reactivate recurrent payments stopped by system.
- Subsequent upgrades are now capable of upgrading any kind of subscription, even the ones with the different length.
- And more smaller improvements.

See the [changelog](changelog/crm/2.8.md). to see full list of changes for this version. 

### 28-Jun-2023: REMP tools release (3.0)

After couple of months of development we're proud to release v3.0. There's a lot going on under the hood and Beam, Campaign, and Sso are no ready to be extensible apps instead of static apps provided at the moment. We now deprecate use of `remp2020/remp` repository for deploys in favor of the newly created skeleton applications. We're finalizing Beam Skeleton and the other apps will continue soon.

Please be aware that this version is a major release due to some breaking changes. Please update your Mailer skeleton application based on [these changes](https://github.com/remp2020/mailer-skeleton/commit/088cf5b660b8b4509295e01815451bfe9f751d03) and Yarn to v2.

Apart from the under-the-hood changes, this release also brings performance improvements and some minor feature updates to Mailer.

The full changelog is available [here](https://github.com/remp2020/remp/releases/tag/3.0.0).

### 28-Jun-2023: CRM release (2.7)

This release brings new extensions points for widgets and event handlers accross the application, and fixes some UI and usability issues of CRM admin.

If you want to get more technical, the full changelog is available [here](changelog/crm/2.7.md).

### 02-Jun-2023: REMP tools patch release (2.2.1)

Patch release 2.2.1 contains fixes for link tracking (new feature of Mailer introduced in 2.2).

The full changelog is available [here](https://github.com/remp2020/remp/releases/tag/2.2.1).

### 25-May-2023: REMP tools release (2.2)

Release 2.2 contains only Mailer changes. Notable change are clicked links tracking and breaking change to how multi variant mail types are subscribed when default variant is not set and no variant is provided.

The full changelog is available [here](https://github.com/remp2020/remp/releases/tag/2.2.0).

### 25-May-2023: CRM release (2.6)

Release 2.6 brings few fixes (eg. `next_subscription_type_id` not being saved when creating subscription type in admin); audit log for `payment_items`; option to not prolong child company subscriptions when new parent subscription is purchased and pairing of one device token to multiple access tokens of same user. `RempMailerModule` contains few breaking changes.

The full changelog is available [here](changelog/crm/2.6.md).

### 25-Apr-2023: REMP tools release (2.1)

This release brings lots of optimizations to Beam, which started to feel a bit slower for bigger instances. Mailer brings better possibilities to manage newsletter variants (both in APIs and UI).

The full changelog is available [here](https://github.com/remp2020/remp/releases/tag/2.1.0).

### 21-Apr-2023: CRM release (2.5)

The latest version of CRM is out. This month it's mainly backend improvements and edge case fixes. There were some important internal changes in the `InvoiceModule` and the `SubscriptionModule` - see the Changelog.

The full changelog is available [here](changelog/crm/2.5.md).

### 24-Mar-2023: REMP tools release (2.0)

The main reason for major version is bump of the minimal version of the core dependencies. REMP tools now require PHP 8.1 and Node.js 18+ to release. The release otherwise contains performance improvements in Mailer and Beam, which will also continue in the following releases.

Please note that in order to use this version, it is expected that both `mail:migrate-mail-logs-and-conversions` and `mail:migrate-user-subscriptions-and-variants` commands introduced in the previous versions were already executed. Update to this version only if you meet the criteria.

The full changelog is available [here](https://github.com/remp2020/remp/releases/tag/2.0.0).

### 24-Mar-2023: CRM release (2.4)

This release brings new extension method for subscriptions asked by our users for some time - `ExtendLastExtension`. It adds new subscription after the last available subscription. It should replace the `ExtendActualExtension` as the default in the future. Also we found a logical issue with audit log which could keep track of anonymized records. To delete those records, please add `application:audit_logs_cleanup` to your scheduled tasks.

The full changelog is available [here](changelog/crm/2.4.md).

### 23-Feb-2023: REMP tools release (1.2)

Today we also bring the new version of REMP tools. In Mailer we continue with internal updates (see info about `mail:migrate-user-subscriptions-and-variants`) and improve tracking of subscribe sources. In Campaign the most important feature is new set of settings for the campaign allowing you to configure what happens when users clicks/closes the banner (without using the Beam segments).

Please note that this version requires you to schedule a manual migration in order to update database internals without the distruption of the system. Read the CHANGELOG's section with `mail:migrate-user-subscriptions-and-variants` command execution.

The full changelog is available [here](https://github.com/remp2020/remp/releases/tag/1.2.0).

### 23-Feb-2023: CRM release (2.3)

After some irregular updates in the recent months we will be trying to get back to more regular (monthly) release cycles. This CRM release might not look big, but for API-primary users of CRM it will be a huge performance improvement.

The full changelog is available [here](changelog/crm/2.3.md).

### 27-Jan-2023: REMP tools release (1.1)

This took a while, but there are features to look for. This release brings support for PHP 8.1 and couple of notable features:

- Campaign is now more focused on JS-banner use which is showing bigger potencial than we originally anticipated. We extracted JS editing from the inline input in the banner form to the separate modal window and added variable extraction for non-developers.
- Mailer now allows you to add your own variables that can be injected into the every email. See `ServiceParamsProviderInterface` in the Mailer's readme file.
- Mailer also need to make a bigger data migration in this release. The process is described in changelog. It's not blocking, but a bit time-intensive.

Please note that this version requires you to schedule a manual migration in order to update database internals without the distruption of the system. Read the CHANGELOG's section with `mail:migrate-mail-logs-and-conversions` command execution.

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
