Color-row-in-SharePoint-list
============================

Using JsLink

// Create a namespace for our custom functions

var svokSpace = svokSpace || {};

// Create function for rendering the field value

svokSpace.myFiledRender = function ()
{
    var myFieldOverride = {};
    //myFieldOverride.Templates = {};
    myFieldOverride.OnPostRender = [ svokSpace.PostRender ];
  
    // We need to register the rendering template
    SPClientTemplates.TemplateManager.RegisterTemplateOverrides(myFieldOverride);
};

svokSpace.PostRender = function (ctx) {
    for (var i = 0; ctx.ListData.Row.length > i; i++) {
        var item = ctx.ListData.Row[i];
        var row = document.getElementById(GenerateIIDForListItem(ctx,item));

        if (row != null) {
            if (item.Color == "A") { row.style.backgroundColor = "rgba(255,0,0,0.5)"; }
            if (item.Color == "B") { row.style.backgroundColor = "rgba(0,255,0,0.5)"; }
            if (item.Color == "C") { row.style.backgroundColor = "rgba(0,0,255,0.5)"; }
            
            // If we want to change font instead of backgroundColor...
            
            if (item.Color == "D") { row.style["font-family"] = "fantasy"; }
        }
    }
    ctx.skipNextAnimation = true;
};
  
// Call the function.
svokSpace.myFiledRender();
