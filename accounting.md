I don't think you made a mistake. I think you're recognizing a tradeoff that wasn't obvious when you started.

Here's how I would think about it.

### The case against ERPNext, Akaunting, and Frappe Books

The biggest issue isn't that they're open source.

The issue is that **their ecosystems are relatively small**.

If you build a fantastic feature for ERPNext:

* maybe a few hundred or a few thousand companies use it.
* many users expect free plugins.
* companies often customize ERPNext heavily, making reusable products harder to sell.

You also don't gain experience with systems that large enterprises recognize.

---

### The case for Microsoft Dynamics Finance

This is much stronger from a business perspective.

Large companies use Dynamics 365 Finance because:

* they have real budgets
* they need integrations
* they constantly migrate data
* they automate accounting workflows
* they pay consultants and developers well

Instead of modifying Dynamics itself, you could build:

* Python ETL tools
* invoice converters
* CSV/XML/Excel import generators
* accounting reconciliation tools
* migration utilities
* report generators
* OCR pipelines
* audit helpers

These are valuable because every ERP needs data flowing into it.

---

### An even bigger insight

The real product isn't Dynamics.

The real product is **accounting interoperability**.

Imagine something like:

```
Bank Statement
      ↓

PDF / CSV / XML

      ↓

Python Processing

      ↓

Output:

✓ Dynamics 365
✓ SAP
✓ Oracle
✓ NetSuite
✓ Odoo
✓ QuickBooks
✓ Xero
✓ Sage
```

Now you're no longer tied to one ERP.

You're solving a universal problem.

---

### Open source can still be useful

ERPNext and Frappe are actually great as:

* development playgrounds
* testing environments
* learning accounting workflows

Because they're open source, you can inspect their data models and experiment freely.

But I probably wouldn't spend months adding niche features unless:

* you were getting paid,
* building a portfolio piece with clear value, or
* the feature could later become a standalone product.

---

### What has better long-term leverage?

I'd rank them roughly like this:

1. **Python accounting automation** (highest leverage)
2. **Import/export tools for multiple ERPs**
3. **Dynamics 365 integrations**
4. **General accounting data transformation libraries**
5. **ERPNext feature development**

Notice that ERP development is last—not because it's bad, but because it's tied to a specific ecosystem.

---

### One caution

Don't assume "Microsoft" automatically means a better opportunity.

Developing *inside* Dynamics often requires specialized knowledge of X++, Power Platform, Azure, licensing, and enterprise deployment. That can be lucrative, but it also raises the barrier to entry.

By contrast, **Python tools that integrate with multiple accounting systems** keep you in your strongest area while serving a much larger market. You can build import/export utilities, reconciliation tools, and migration pipelines that work across different ERPs instead of depending on one vendor.

So I wouldn't view your previous work as wasted. It likely taught you:

* accounting concepts,
* ERP data structures,
* import/export formats,
* invoicing workflows,
* and common user pain points.

Those lessons transfer directly into building independent accounting automation tools. The difference is that instead of creating features *for* an ERP, you're creating products that many ERPs—and their users—can benefit from. That tends to be a more durable strategy.
