---
pcx_content_type: how-to
title: Zone level
weight: 3
meta:
  title: Zone custom nameservers
  description: With zone-level custom nameservers, each custom nameserver name must be a subdomain of the zone where the custom nameservers are configured. These custom nameservers can only be used within the respective zone.
---

# Zone custom nameservers

With zone custom nameservers (ZCNS), each custom nameserver name must be a subdomain of the zone where the custom nameservers are configured.

For example, for a zone `domain.test`, the ZCNS can be `ns1.domain.test` and `ns2.domain.test` but they cannot use a different TLD (`ns1.domain.org`) nor a different domain (`ns1.example.com`).

## Use zone custom nameservers

### Primary (full setup) zones

To create zone custom nameservers:

{{<tabs labels="Dashboard | API">}}
{{<tab label="dashboard" no-code="true">}}

1. Log in to the [Cloudflare dashboard](https://dash.cloudflare.com) and select your account and zone.
2. Go to **DNS** > **Records**.
3. On **Custom nameservers**, select **Configure**.
4. Select **Create custom nameservers just for `your-domain.com`** and enter the subdomains used for the ZCNS names (for example, `ns1`, `ns2`, `ns3`).

{{</tab>}}
{{<tab label="api" no-code="true">}}

Use the [Edit zone endpoint](/api/operations/zones-0-patch) and specify the custom nameservers in the payload:

```txt
"vanity_name_servers": ["ns1.example.com","ns2.example.com"]
```
{{</tab>}}
{{</tabs>}}

Cloudflare will assign an IPv4 and an IPv6 address to each ZCNS name and automatically create the associated `A` or `AAAA` records (visible after you refresh the page).

The next step depends on whether you are using [Cloudflare Registrar](/registrar/) for your domain:

- If you are using Cloudflare Registrar for your domain, no further action is required. Glue records will be added automatically on your behalf.
- If you are not using Cloudflare Registrar for your domain, add the zone custom nameservers at your registrar as your authoritative nameservers and as [glue (A and AAAA) records]([RFC 1912](https://www.rfc-editor.org/rfc/rfc1912.html)). If you do not add these records, DNS lookups for your domain will fail.

### Secondary zones

If you are using [Cloudflare as a secondary DNS provider](/dns/zone-setups/zone-transfers/cloudflare-as-secondary/), you can still set up zone custom nameservers. After following the [steps above](/dns/additional-options/custom-nameservers/zone-custom-nameservers/#primary-full-setup-zones) to create zone custom nameservers, do the following:

1. Get the ZCNS IPs. You can see them on the dashboard (**DNS** > **Records**) or you can use the [Zone details endpoint](/api/operations/zones-0-get) to get the `vanity_name_servers_ips`.
2. At your primary DNS provider, add [`NS` records](/dns/manage-dns-records/reference/dns-record-types/#ns) and, on the subdomains that you used as ZCNS names, add `A/AAAA` records.
3. At your registrar, add the zone custom nameservers as your authoritative nameservers and as [glue (A and AAAA) records](https://www.ietf.org/rfc/rfc1912.txt).

## Remove zone custom nameservers

To remove zone custom nameservers (and their associated, read-only DNS records):

{{<tabs labels="Dashboard | API">}}
{{<tab label="dashboard" no-code="true">}}

1. Log in to the [Cloudflare dashboard](https://dash.cloudflare.com) and select your account and zone.
2. Go to **DNS** > **Records**.
3. (TBD) On **Custom nameservers**, select **Remove custom nameservers**.

{{</tab>}}
{{<tab label="api" no-code="true">}}

Use the [Edit zone endpoint](/api/operations/zones-0-patch) and include an empty array in the payload:

```txt
"vanity_name_servers": []
```
{{</tab>}}
{{</tabs>}}

Cloudflare will remove your ZCNS and their associated read-only `A` or `AAAA` records.

If you are not using Cloudflare Registrar for your domain, make sure to adjust your nameservers at the registrar, parent zone, or Primary DNS provider accordingly.