---
description: Backup your sites and data
---

# Site Backups and Disaster Recovery

{% hint style="info" %}
We recommend using the Sitegurus Protect Backup Tool: [https://www.sitegurus.io/protect](https://www.sitegurus.io/protect)
{% endhint %}

There are 3 main components that make up your clients sites that we need to consider in terms of backups and disaster recovery: Code, Assets and Data. We will outline how each are handled below:

#### Code

* Every code change whether through CLI or Admin is stored in a Github repo controlled by Siteglide
* This also stores the UserID of the user that took the action for traceability
* This is mainly stored for disaster recovery purposes
* You can export using `siteglide-cli pull <env>`

#### Assets

* Stored on S3 by platformOS
* AWS/Google Cloud mirror assets across multiple data centres
* You can export using `siteglide-cli export <env> -w`

#### Data

* Stored in databases by platformOS
* platformOS have backups and store changelogs/versions of what happened
* Upon deletion, the data is recoverable for 30 days. After 30 days of being soft deleted the data is permanently deleted at 5am UTC.
* You can export data using `siteglide-cli export <env>`

We will be offering additional backup tools and automations in the future.

PlatformOS also have documentation on [Backups and Disaster Recovery](https://documentation.platformos.com/developer-guide/about-platformos/security-drp).

The following are key points taken from the platformOS documentation:

platformOS automatically backs up your applications and databases using real-time READ REPLICAs which exist across multiple Zones for further physical disaster recovery within a data-center.

Additionally, incremental transaction logs, daily and weekly backups are taken.

The retention period for monthly backups is 60 days.

These processes are internal to the platformOS DevOps team.

Learn more:

* [Data Backup and Removal](https://documentation.platformos.com/developer-guide/records/data-backup-removal#undeleting-data): Learn about how deleted data is backed up and when it is removed permanently. Includes explanation of automatic and manual permanent removal.
* [GDPR Compliance in platformOS](https://documentation.platformos.com/best-practices/gdpr/gdpr-compliance): Learn how platformOS approaches GDPR as just one of many compliance requirements and ensures that your project can easily comply with any number of government legislated privacy rules.
* [AWS Backup](https://aws.amazon.com/backup/): AWS Backup is a fully managed backup service that makes it easy to centralize and automate the backup of data across AWS services.
* [Google Cloud Backups](https://cloud.google.com/sql/docs/mysql/backup-recovery/backups): How backups of your Cloud SQL instance work, and how they can be used to restore your data to the same or another instance.
