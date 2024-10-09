# 💳 Subscriptions and Changes

## Usage-based Billing

The Subscriptions tab shows you exactly what each site uses broken down into high-level types of infrastructure usage and then down to specific Siteglide features to help show more value to clients.

For example, you can see the total number of Units but the real value is seeing that this is made up of CRM Contacts, Form Cases, WebApp items, Module Items, Products and much more.

**Note:** External API calls are unlikely to be used for many sites if you're not working on platformOS directly via CLI.

When comparing the cost of the various different tools required to achieve the same result and then trying to somehow connect them all together you can show huge savings to clients both in terms of cost and time.

### Plans and Extras

You can see the individual Site Plan pricing on the Plans page:

<figure><img src="../../.gitbook/assets/Siteglide-Billing-Plans.png" alt=""><figcaption></figcaption></figure>

Extras are charged pro-rata based on the plan price. Simply divide the Plan Price by the Units included you get the Unit Rate that you will be charged if you exceed the limit.

We replaced the old, more costly Overages with Extras. If your site subscription tab shows a 'Legacy' plan please refer to old old Overages pricing or speak to the team about switching to one of our new plans!&#x20;

### How our usage-based billing works:

1. Storage, Records, Domains and Client Admin Users do not reduce unless deleted.
2. Emails, API Calls and Bandwidth renew each month.
3. You are billed based on the peak usage each calendar month.
4. Deleted items count towards peak usage for that month but do not count in subsequent months.
5. Once you hit 70% usage of any metric it will be marked as orange as a warning.
6. Once you hit 100% usage of any metric you will start incurring Extras.
7. If you have [Automatic Upgrades](automatic-site-upgrades.md) turned on and the cost of Extras exceeds the difference in cost to upgrade to the appropriate plan the site will automatically be upgraded on the 1st of the following month.
8. You can manually upgrade or downgrade to any plan once per month but if the new plan doesn't cover the usage you will be charged overages.
9. We do not downgrade automatically as we do not know what usage will be required in a given month and assume most sites increase in usage as the business grows and the site becomes more successful/popular.

## Subscription Changes

To give you full use of the Siteglide platform we simply charge you based on your usage which can change over time and likely increase as you help your clients grow.

Please ensure you're aware of how subscription changes work before going live:

1. We monitor usage and provide the Subscriptions tab for each site to show if you are close to exceeding or exceeding the usage available on the current plan. Find out more about the Subscriptions Area in Portal.
2. We calculate usage at midnight on the 1st of each month for the whole of the previous month. If you have [Automatic Upgrades](automatic-site-upgrades.md) turned on and exceed any usage limits we will apply the **cheapest option** at the time which will either be to charge Extras or Upgrade the plan. If you have Automatic Upgrades turned off we will only charge the Extras.
3. Extras are charged in blocks as a one-off charge for excess usage in that billing period. Typically you could use double the allowance of one usage metric before it’s cheaper to upgrade to the next plan.
4. For Monthly Upgrades the new plan will be applied immediately both for the new month and retrospectively for the previous month (to avoid paying more costly overages). We will charge for the new month and the increase between the new and previous plan. **This will only be done to save higher overage costs, we will always apply the cheapest option.**
5. Annual Upgrades will start a new 12 month subscription crediting the balance of the previous subscription prior to payment (e.g. $250 - $63 (6 months remaining of Starter plan).
6. For Sites on Connect Billing (deprecated) we will continue to pick the cheapest option based on our fees not what you charge your customer as this can vary (you could manually upgrade them to a higher plan if preferred).
7. If your site usage decreases and you believe it will not increase again then you might wish to Downgrade to a lower plan. Simply press Downgrade on the Subscriptions page, pick your chosen plan and request the Downgrade. The Downgrade will not take effect until the end of the current billing period. **Note**: You may prefer not to do this on Connect Billing to avoid lots of changes.
8. If you wish to cancel a site we recommend first discussing any issues with our Success team but alternatively you can delete the site via the portal. Please note deleting a site takes effect immediately and all data will be irretrievably lost. All payments are non-refundable so we recommend making full use of the current billing cycle before deleting the site (any remaining time will be forfeited).
9. Please see our full Payment Terms and Payment Failure Process in our [End User Licence Agreement](https://www.siteglide.com/end-user-license-agreement) (sections 7 and 8).
