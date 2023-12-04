# Refining and Testing

Continuing to learn rust day by day. One issue I ran into was that the checker
wouldn't let me declare string constants or structs with string constants
before runtime. However, I could declare a function that generates the strings
at runtime.

In short, declare test fixtures as function rather than constants.

```rust
    /// Returns a vector of `ApiStation` structs for testing purposes.
    ///
    /// The vector contains two stations with hardcoded values for their respective fields.
    fn test_api_stations() -> Vec<ApiStation> {
        vec![
            ApiStation {
                name: String::from("station1"),
                stationuuid: String::from("uuid1"),
                url: "url1".to_string(),
                homepage: "homepage1".to_string(),
                favicon: "favicon1".to_string(),
                codec: "codec1".to_string(),
                has_extended_info: None,

                ...
            },
        ]
    }



```
