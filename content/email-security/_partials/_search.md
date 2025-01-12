---
_build:
  publishResources: false
  render: never
  list: never
---

1. **Detections only** is enabled by default. This means that the system will only search through and display emails that Email Security (formerly Area 1) has marked with a detection {{<glossary-tooltip term_id="disposition" link="/email-security/reference/dispositions-and-attributes/">}}disposition{{</glossary-tooltip>}}. If you prefer to search through and view all emails that have been processed by Email Security, whether they are marked with a detection disposition or not, disable this option.
2. The **All detections** drop-down menu allows you to refine your search by detection disposition. This menu will be disabled if **Detections only** is not selected.
3. By default, the search results are limited to the previous 30 days. Select **Last 30 days** to change this setting.
4. (Optional) You can download the results from your search in CSV format. The CSV file is capped at 1,000 rows.
5. The system returns a list of emails that fit your search criteria, and will inform you if there are emails similar to the ones found. If Email Security finds emails similar to the ones returned by your query, select **Show** to display them. Otherwise, select **View** on the email you are interested in. This will show you more information about that particular email, such as:
	- Disposition (if any)
	- Email status (for example `Quarantined`)
	- Sender details (for example, IP address)