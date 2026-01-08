# Add an External Domain

{% hint style="warning" %}
We strongly recommend Fully Delegating your domain for best results or ensuring you use a domain control panel that allows CNAME records on the root/@ or ANAME records such as [Cloudflare](https://www.cloudflare.com/).
{% endhint %}

If you have a domain that is managed in GoDaddy or another registrar and would like to point it to a Siteglide website you can use our External Domain feature. This means that you can continue to manage your DNS through GoDaddy/other registrar.

{% hint style="info" %}
This guide is for our Oracle/Cloudflare OCI servers. If your site is on our old AWS stacks please use the link below:
{% endhint %}

{% content-ref url="legacy-aws-external-domains.md" %}
[legacy-aws-external-domains.md](legacy-aws-external-domains.md)
{% endcontent-ref %}

### Standard Setup: Enable WWW Redirect (e.g. https://www.example.com)

Most websites use www and redirect non-www traffic to www.

#### Step 1: Add the domain

Simply select External, type in the root domain (without www) and then select _'Use as default domain'_ and _'Enable WWW redirect'_:

<figure><img src="../../../.gitbook/assets/Siteglide-Portal-Sites-Domain-External-Add.png" alt=""><figcaption></figcaption></figure>

#### Step 2: Add the www records

Simply add the following records in your DNS control panel to setup the www version:

{% hint style="info" %}
Replace \[example.com] and \[www.example.com] with and without www as documented.
{% endhint %}

**UK OCI server:**

<table><thead><tr><th width="210.3828125">Name</th><th width="90.59765625">Type</th><th>Value</th></tr></thead><tbody><tr><td>_acme-challenge.www</td><td>CNAME</td><td>[www.example.com].fb56597de0699182.dcv.cloudflare.com</td></tr><tr><td>www</td><td>CNAME</td><td>_fallback.uk-siteglide.com</td></tr></tbody></table>

**US OCI server:**

<table><thead><tr><th width="209.98828125">Name</th><th width="90.59765625">Type</th><th>Value</th></tr></thead><tbody><tr><td>_acme-challenge.www</td><td>CNAME</td><td>[www.example.com].946274feaef29fbf.dcv.cloudflare.com</td></tr><tr><td>www</td><td>CNAME</td><td>_fallback.us-siteglide.com</td></tr></tbody></table>

**AU OCI server:**

<table><thead><tr><th width="210.421875">Name</th><th width="90.59765625">Type</th><th>Value</th></tr></thead><tbody><tr><td>_acme-challenge.www</td><td>CNAME</td><td>[www.example.com].e94b5430d374b59e.dcv.cloudflare.com</td></tr><tr><td>www</td><td>CNAME</td><td>_fallback.au-siteglide.com</td></tr></tbody></table>

#### Step 3: Redirect the root to www

{% hint style="warning" %}
If your DNS provider doesn't support CNAME flattening we recommend switching either to our fully delegated option or using Cloudflare to manage your DNS (they offer CNAME flattening).
{% endhint %}

Does your DNS provider support a "flattened" CNAME (sometimes called ANAME or CNAME flattening) on the root/apex?

1. If **YES** you can add the following records (replace values in square brackets: \[]):

<table><thead><tr><th width="239.56640625">Name</th><th width="90.59765625">Type</th><th>Value</th></tr></thead><tbody><tr><td>_acme-challenge</td><td>CNAME</td><td>As above but without www, e.g for UK:[example.com].fb56597de0699182.dcv.cloudflare.com</td></tr><tr><td>blank/@</td><td>CNAME</td><td>As above, e.g. for UK: _fallback.uk-siteglide.com</td></tr></tbody></table>

2. If **NO** you must redirect traffic to www and you will need to use an external service such as redirect.pizza to handle the root redirection to www:

<table><thead><tr><th width="240.1953125">Name</th><th width="90.59765625">Type</th><th>Value</th></tr></thead><tbody><tr><td>[example.com] (blank/@)</td><td>A</td><td><a data-mention href="add-an-external-domain.md#forward-the-root-to-the-www-with-ssl">#forward-the-root-to-the-www-with-ssl</a></td></tr></tbody></table>

### Alternative Setup: Redirect all traffic to the root (e.g. https://example.com)

{% hint style="danger" %}
This is not possible via External DNS if your DNS provider doesn't support CNAME flattening. We recommend switching either to our fully delegated option or using Cloudflare to manage your DNS (they offer CNAME flattening).
{% endhint %}

#### Step 1: Add the domain

Simply select External, type in the root domain (without www) and then select _'Use as default domain'_ and NOT select _'Enable WWW redirect'_:

<figure><img src="../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

#### Step 2: Add the records

Simply add the following records in your DNS control panel:

**UK OCI server:**

<table><thead><tr><th width="190.34375">Name</th><th width="90.59765625">Type</th><th>Value</th></tr></thead><tbody><tr><td>_acme-challenge</td><td>CNAME</td><td>[example.com].fb56597de0699182.dcv.cloudflare.com</td></tr><tr><td>blank/@</td><td>CNAME</td><td>_fallback.uk-siteglide.com</td></tr></tbody></table>

**US OCI server:**

<table><thead><tr><th width="190.3984375">Name</th><th width="90.59765625">Type</th><th>Value</th></tr></thead><tbody><tr><td>_acme-challenge</td><td>CNAME</td><td>[example.com].946274feaef29fbf.dcv.cloudflare.com</td></tr><tr><td>blank/@</td><td>CNAME</td><td>_fallback.us-siteglide.com</td></tr></tbody></table>

**AU OCI server:**

<table><thead><tr><th width="189.5703125">Name</th><th width="90.59765625">Type</th><th>Value</th></tr></thead><tbody><tr><td>_acme-challenge</td><td>CNAME</td><td>[example.com].e94b5430d374b59e.dcv.cloudflare.com</td></tr><tr><td>blank/@</td><td>CNAME</td><td>_fallback.au-siteglide.com</td></tr></tbody></table>

### Subdomain Setup

#### Step 1: Add the subdomain

Simply type in the subdomain and ensure you do NOT select Enable WWW redirect:

<figure><img src="../../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

**Step 2: Add the records**

{% hint style="info" %}
Replace \[subdomain] with the value you want the subdomain to be, e.g: 'blog' (this would create: blog.example.com). In this example replace \[subdomain.example.com] with: 'blog.example.com'.
{% endhint %}

**UK OCI server:**

<table><thead><tr><th width="190.34375">Name</th><th width="90.59765625">Type</th><th>Value</th></tr></thead><tbody><tr><td>_acme-challenge.[subdomain]</td><td>CNAME</td><td>[subdomain.example.com].fb56597de0699182.dcv.cloudflare.com</td></tr><tr><td>[subdomain]</td><td>CNAME</td><td>_fallback.uk-siteglide.com</td></tr></tbody></table>

**US OCI server:**

<table><thead><tr><th width="190.3984375">Name</th><th width="90.59765625">Type</th><th>Value</th></tr></thead><tbody><tr><td>_acme-challenge.[subdomain]</td><td>CNAME</td><td>[subdomain].946274feaef29fbf.dcv.cloudflare.com</td></tr><tr><td>[subdomain]</td><td>CNAME</td><td>_fallback.us-siteglide.com</td></tr></tbody></table>

**AU OCI server:**

<table><thead><tr><th width="189.5703125">Name</th><th width="90.59765625">Type</th><th>Value</th></tr></thead><tbody><tr><td>_acme-challenge.[subdomain]</td><td>CNAME</td><td>[subdomain].e94b5430d374b59e.dcv.cloudflare.com</td></tr><tr><td>[subdomain]</td><td>CNAME</td><td>_fallback.au-siteglide.com</td></tr></tbody></table>

***

### Forward the Root/@ to the www (with SSL) <a href="#forward-the-root-to-the-www-with-ssl" id="forward-the-root-to-the-www-with-ssl"></a>

Most DNS Control Panels cannot correctly redirect the root traffic to the WWW over SSL so we recommend using an external service called Redirect.Pizza.

Just follow these steps to redirect your **non-www** to the **www** variant. The non-www is also sometimes called naked record or "apex" (screenshots below):

1. Create a [redirect.pizza](https://redirect.pizza/register) account.
2. Add your source. This should be the domain without www. For instance, enter **example.com** as your source.
3. Set the destination to the variant with www. Example: **www.example.com**
4. In most cases, you will want the setting for "Path forwarding" and "Query string forwarding" set to "Yes". If set to "No", all non-www pages will redirect to your www homepage.
5. Press "Create redirect"
6. The required DNS change pops up. Go to your domain registrar to make this DNS change for the **A** record. This record may already exists '@'. Press 'edit' to edit it to the required DNS setting for redirect.pizza. For more info, see [What are these DNS changes?](https://redirect.pizza/support/what-are-these-dns-changes)
7. The DNS change is made! It may take up to 24 hours before the DNS is fully propagated.

![](https://docs.siteglide.com/en/~gitbook/image?url=https%3A%2F%2F584571746-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Ft7n2OYNNUr9PgpkBD2eX%252Fuploads%252Fgit-blob-64e986b309a0f7b4e659fb592a5b4651a560b06d%252FSiteglide-Portal-Sites-Domains-External-Redirect-Pizza-Verified.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=c978c0b9\&sv=2)![](https://docs.siteglide.com/en/~gitbook/image?url=https%3A%2F%2F584571746-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Ft7n2OYNNUr9PgpkBD2eX%252Fuploads%252Fgit-blob-bf5d72f92646003a4078b95d1b2b930d196edd0a%252FSiteglide-Portal-Sites-Domains-External-Redirect-Pizza-Checking.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=bb4a5c21\&sv=2)![](https://docs.siteglide.com/en/~gitbook/image?url=https%3A%2F%2F584571746-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Ft7n2OYNNUr9PgpkBD2eX%252Fuploads%252Fgit-blob-24dcd675ff27d1d788dfbf84669f65711da4d5ef%252FSiteglide-Portal-Sites-Domains-External-Redirect-Pizza-Create.png%3Falt%3Dmedia\&width=768\&dpr=4\&quality=100\&sign=bb62dfaa\&sv=2)

These Steps can also be found here: [https://redirect.pizza/support/redirecting-non-www-to-www](https://redirect.pizza/support/redirecting-non-www-to-www)
