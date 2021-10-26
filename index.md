## REMP Technical news

### 26-Oct-2021: Hotfix release for ApplicationModule

Previous version optimized and speed up API. Unfortunately it introduced bug which breaks initial CRM installation _(application is unable to create required tables)_. This hotfix release contains fix for `Core::command()`. Update your `crm-application-module` to `0.35.1` ([changelog](https://github.com/remp2020/crm-application-module/releases/tag/0.35.1)).

### 25-Oct-2021: New version of CRM is available (0.35.0)

**Technical announcement:** We've been successfully using CRM with MySQL 8 in production and we believe it's stable for everyone to use. In order to use the latest features of MySQL 8, we will need to drop MySQL 5.7 support in the next months. 

The preliminary end of support for MySQL 5.7 is scheduled for **April 2022**. Please schedule the upgrade of your database by this date in order to safely receive next versions of CRM. It's possible the CRM will work for you after this date, but you might encounter compatibility issues though.

Now for the actual release. This release focuses mainly on improving stability, but brings some interesting features.

- Bump of minimal version of PHP to 7.4.
- Fix of inefficient API handler initialization, possibly improving speed of all API endpoints.
- Support for Redis Sentinel.
- New Scenario A/B test element.

Check the [changelog](changelog/crm/0.35.md) to see the full list of changes and upgrade information.

### 06-Oct-2021: New version of CRM is available (0.34.0)

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

### 23-Aug-2021: New version of CRM is available (0.33.0)

It's been a while since the last release. The main improvements in this version are:

- More fine-grained ACL control for administration.
- Apple sign-in support.
- Additional scenario criteria, this time mainly for ProductsModule.

There's more, including couple of breaking changes, so head to the [changelog](changelog/crm/0.33.md) to see the full list of changes and upgrade information.
