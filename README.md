# Lighting Internals Package
Provides access to internal lighting APIs.

# `LightingData`
Provides access to the information contained in the `LightingDataAsset` class. To use it, create a new instance and call `Initialize`:
```cs
var data = ScriptableObject.CreateInstance<LightingData>();
data.Initialize(Lightmapping.lightingDataAsset);
```
In order to save your changes back to the `LightingDataAsset`, use the `Save` method:
```cs
data.Save(Lightmapping.lightingDataAsset);
```

# `LightmappingInternal`
Provides access to the `bakeAnalytics` callback, which receives detailed information about lightmap bakes. This comes in the form of a JSON string, which can be deserialized through the `LightmappingAnalyticsData` type.

```cs
LightmappingInternal.bakeAnalytics += OnBakeAnalytics;

// ...

static void OnBakeAnalytics(string json)
{
    switch (JsonUtility.FromJson<LightmappingAnalyticsData>(json).outcome)
    {
    case "success":
        // Bake completed successfully
        break;
    case "cancelled":
    case "forcestop":
    case "interrupted":
        // Bake completed unsuccessfully
        break;
    }
}
```
