# Acceptance fixture security patches

Official Magento Open Source 2.4.9 source with the July, August, September and
October 2026 CE isolated patches, followed by the separate CVE-2026-75650 hotfix.
Only CE changes are applied; EE/B2B patch files are not used.

Sources:

- https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-37421
- https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-40380
- https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-44020
- https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-49323
- https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/announcements/commerce-apsb26-146

The official patch headers use Composer vendor paths. Only paths were mapped to
the equivalent GitHub CE app/code and lib/internal paths; patch contents were
not changed. A separate clean source copy passed all five dry-runs and applies
with fuzz=0 and no ignored hunks. The committed runtime files match that result.
PHP syntax checks pass with PHP 8.5.11. Composer runtime installation, Magento
functional tests and cloud acceptance are pending.

The upstream CVT script was inspected locally. Its status check is NOT_RUN for
this GitHub-source layout: composer.lock does not contain a
magento/product-community-edition package. Vendor tools are not committed;
no CVT vulnerability-status claim is made. No Cloud Patches engine or catalog
is copied into MageLift.

Official download archive SHA-256 values:

```text
0f300d043b5f7f9558d2d1ffe13b91ec84b5766549adbaec1fc73278ff72b0e1  2-4-9-aug-2026.zip
650e8e34e925653a1b3980ce053b9cb993dc2b22e72ee80b5557e03f36848984  2-4-9-jul-2026.zip
1d995f5998a65dc46c76c31bb4cff799ebaf26121ca933ec18a708393b2f1d30  2-4-9-oct-2026.zip
9fe17a9681d94deaaeb2ca9245e1e1bcd9fad9b3478fbcaaa8ab1a94ee4cd686  2-4-9-sep-2026.zip
5f98d409e627c0ac77fb9cbff4bf139c17ad69550dc06411a4b4d0aeadd669e1  VULN-39341-composer-patches.zip
```
