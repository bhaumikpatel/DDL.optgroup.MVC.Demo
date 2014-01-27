HTML5 &lt;optgroup&gt; tag in MVC
=====================
There is no built-in support in the framework for this kind of drop down lists.

----------
Nuget Package [<i class="icon-share"></i> DDL.optgroup.MVC](#publish-a-document)
---------

To install *DDL.optgroup.MVC*, run the following command in the Package Manager Console

> **PM> Install-Package Microsoft.AspNet.Mvc**

#### **Document** - Using Database Context
```
    MvcApplication1.Models.Database1Context db = new MvcApplication1.Models.Database1Context();
    var data = db.locations.ToList().Select(t => new GroupedSelectListItem
    {
        GroupKey = t.location_group_id.ToString(),
        GroupName = t.location_group.name,
        Text = t.name,
        Value = t.id.ToString()
    });
```
**Razor View**
```
    @Html.DropDownGroupListFor(m => m.location_id, data, "-- Select --", new { 
            @data_val = "true",  // for Required Validation
            @data_val_required = "The Name field is required." // for Required Validation
        })
```
#### **Document** - Using Static Data
```
    IEnumerable<GroupedSelectListItem> item;
    item = new List<GroupedSelectListItem> { 
        new GroupedSelectListItem() { Value="volvo", Text="Volvo", GroupName="Swedish Cars", GroupKey="1", Disabled=true },
        new GroupedSelectListItem() { Value="saab", Text="Saab",GroupName="Swedish Cars", GroupKey="1" }, 
        new GroupedSelectListItem() { Value="mercedes", Text="Mercedes", GroupName="German Cars", GroupKey="2" },
        new GroupedSelectListItem() { Value="audi", Text="Audi", GroupName="German Cars", GroupKey="2",Selected=true }};
```
**Razor View**
```
    @using (Ajax.BeginForm("Index", null, new AjaxOptions { HttpMethod = "post" }, new { id = "frm" }))
    {
        @Html.DropDownGroupList("Cars", item, "-- Select Car --", 
            new Dictionary<string, object>() { 
                { "data-val", "true" }, 
                { "data-val-required", "The Car field is required." } 
            })
        <input type="submit" name="name" value="Send" />
    }
```
**HTML**
```
    <select data-val="true" data-val-required="The Car field is required." id="Cars" name="Cars" class="valid">
        <option value="">-- Select Car --</option>
        <optgroup label="Swedish Cars" value="1" disabled="">
            <option value="volvo">Volvo</option>
            <option value="saab">Saab</option>
        </optgroup>
        <optgroup label="German Cars" value="2">
            <option value="mercedes">Mercedes</option>
            <option selected="selected" value="audi">Audi</option>
        </optgroup>
    </select>
```
**Output**
<select data-val="true" data-val-required="The Car field is required." id="Cars" name="Cars" class="valid"><option value="">-- Select Car --</option>
<optgroup label="Swedish Cars" value="1" disabled="">
<option value="volvo">Volvo</option>
<option value="saab">Saab</option>
</optgroup>
<optgroup label="German Cars" value="2">
<option value="mercedes">Mercedes</option>
<option selected="selected" value="audi">Audi</option>
</optgroup>
</select>