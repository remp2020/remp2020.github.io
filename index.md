## REMP Technical news

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
