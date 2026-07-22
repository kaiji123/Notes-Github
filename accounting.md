Given your goal—**understanding accounting deeply, building external Python tools, and making money in Slovakia**—I would separate the problem into **accounting knowledge** and **software market knowledge**.

They overlap, but they're not the same.

## 1. To learn accounting

You do **not** need Microsoft Dynamics specifically.

Accounting principles are largely the same regardless of software:

* double-entry bookkeeping
* VAT
* invoices
* credit notes
* inventory
* depreciation
* bank reconciliation
* accruals
* financial statements

You can learn these with:

* Excel
* a textbook or accounting course
* sample transactions
* any accounting software

The software is just the interface.

---

## 2. To make money in Slovakia

This is where software choice matters.

If your customers are Slovak companies, they're much more likely to use local accounting packages than Microsoft Dynamics.

Examples include:

* Omega
* Pohoda
* Money S3
* KROS products
* occasionally Dynamics in larger enterprises

Small and medium businesses dominate Slovakia, and many of them use local software because it's tailored to Slovak tax rules and reporting.

If you want to sell automation to accountants and SMEs, understanding at least one major local package is a significant advantage.

---

## 3. Microsoft Dynamics

Dynamics is valuable because it teaches enterprise ERP concepts:

* dimensions
* chart of accounts
* workflows
* approvals
* fixed assets
* purchasing
* sales
* inventory
* project accounting

These concepts transfer well to SAP, Oracle, and other enterprise systems.

However, it is less representative of what a typical Slovak bookkeeping office uses day to day.

---

## 4. Excel

Excel is indispensable.

Professional accountants still rely on it heavily for:

* reconciliation
* imports and exports
* VAT analysis
* pivot tables
* audit work
* data cleaning
* ad hoc reporting

If your Python applications can read and write Excel well, they'll integrate naturally into many accounting workflows.

---

## 5. If I were building your foundation

I'd prioritize it like this:

1. **Accounting theory** (most important)
2. **Excel** (advanced formulas, Power Query, pivots)
3. **One Slovak accounting package** (such as Omega or Pohoda)
4. **Python automation**
5. **Microsoft Dynamics Finance**

Why this order?

Because once you understand accounting and a real local workflow, you'll start seeing repetitive tasks that Python can automate. Those are often the kinds of tools businesses are willing to pay for.

---

## 6. Your long-term advantage

I actually think your edge won't be "knowing Dynamics."

It will be being able to say:

> "I understand accounting well enough to automate it."

That leads to tools like:

* invoice importers
* bank statement converters
* VAT validation
* reconciliation assistants
* journal entry generators
* bulk transaction processors
* document parsers (PDF → accounting entries)
* data migration utilities between accounting systems

Those solve problems regardless of the ERP.

## My suggestion

If your goal is to earn income in Slovakia within the next few years, I would choose:

* **70%** learning accounting (including Slovak accounting rules and one widely used local package like Omega or Pohoda),
* **20%** becoming excellent with Excel,
* **10%** learning Microsoft Dynamics Finance to understand enterprise ERP concepts.

That combination gives you a strong understanding of real accounting practice in your local market while also preparing you to build external Python applications that can later support both local software and enterprise systems.


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
