---
versionFrom: 8.0.0
---

# Radiobutton List

`Alias: Umbraco.RadioButtonList`

`Returns: string`

Pretty much like the name indicates this Data type enables editors to choose from list of radio buttons and returns the value of the selected item as string.

## Data Type Definition Example

![Radiobutton List Data Type Definition](images/RadioButton-List-DataType-v8.png)

## Content Example

![Radiobutton List Content](images/RadioButton-List-Content-v8.png)

## MVC View Example

### Typed

#### Without Modelsbuilder

```csharp
@if (Model.HasValue("colorTheme"))
{
    var value = Model.Value("colorTheme");
    <p>@value</p>
}
```

#### With Modelsbuilder

```csharp
@if (Model.ColorTheme.HasValue())
{
    var value = Model.ColorTheme;
    <p>@value</p>
}
```

## Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the [Content Service](../../../../../Reference/Management/Services/ContentService/index.md).

```csharp
@{
    // Get access to ContentService
    var contentService = Services.ContentService;

    // Create a variable for the GUID of the page you want to update
    var guid = new Guid("796a8d5c-b7bb-46d9-bc57-ab834d0d1248");
    
	// Get the page using the GUID you've defined
    var content = contentService.GetById(guid); // ID of your page
	
	// Set the value of the property with alias 'colorTheme'
    content.SetValue("colorTheme", "water");
            
    // Save the change
    contentService.Save(content);
}
```

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

```csharp
@{
    // Get the page using it's id
    var content = contentService.GetById(1234); 
}
```

If Modelsbuilder is enabled you can get the alias of the desired property without using a magic string:

```csharp
@{
    // Set the value of the property with alias 'colorTheme'
    content.SetValue(Home.GetModelPropertyType(x => x.ColorTheme).Alias, "water");
}
```