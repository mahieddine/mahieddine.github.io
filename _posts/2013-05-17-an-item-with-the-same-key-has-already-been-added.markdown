---
layout: post
title:  "An item with the same key has already been added…"
date:   2013-05-17 20:00:23 +0700
categories: [dotnet]
---

If you use the Microsoft Framework “Microsoft ASP.NET Dynamic Data”  to build data driven web applications  you may encounter this error “An item with the same key has already been added…” in the OnPreRenderComplete Event handler method this is because you used the reserved keyword “Action” or “Table” to name a column or a table in your database, the Router use these keywords for its internal purposes and using one of this keywords causes troubles

To overcome this issue you must simply catch this error like this : 

```C#
protected override void OnPreRenderComplete(EventArgs e)
        {
            try
            {
                RouteValueDictionary routeValues = new RouteValueDictionary(GridView1.GetDefaultValues());
                InsertHyperLink.NavigateUrl = table.GetActionPath(PageAction.Insert, routeValues);
            }
            catch (Exception)
            {
            }
            base.OnPreRenderComplete(e);
        }
```
In my case i was using entity framework and even with renaming the Entity Type and stuff like that it doesn’t work, you have to don’t use one of those keywords

I Agree this is not the perfect solution but in my case i was not able to change the name of my table.

The ASP Team is working on this issue according to this [http://forums.asp.net/t/1848221.aspx/1](http://forums.asp.net/t/1848221.aspx/1) but for the moment there are no solution except the one i’ve done.
