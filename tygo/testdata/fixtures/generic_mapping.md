A type mapping can refer to a generic type's arguments with `{0}`, `{1}`, ...
```yaml
type_mappings:
  nullable.Field: "{0} | null"
  richtext.Document: "RichTextDocument"
```

```go
type UpdateEventRequest struct {
    Name            nullable.Field[string]            `json:"name,omitzero"`
    Capacity        nullable.Field[int]               `json:"capacity,omitzero"`
    DescriptionJSON nullable.Field[richtext.Document] `json:"descriptionJson,omitzero"`
    Tags            []nullable.Field[string]          `json:"tags"`
    Links           map[string]nullable.Field[string] `json:"links"`
}
```

```ts
export interface UpdateEventRequest {
  name?: string | null;
  capacity?: number /* int */ | null;
  descriptionJson?: RichTextDocument | null;
  tags: (string | null)[];
  links: { [key: string]: string | null};
}
```

Several type arguments, and a pointer argument
```yaml
type_mappings:
  util.Pair: "[{0}, {1}]"
  nullable.Field: "{0} | null"
```

```go
type Lookup struct {
    Entry  util.Pair[string, int]  `json:"entry"`
    Parent nullable.Field[*string] `json:"parent"`
}
```

```ts
export interface Lookup {
  entry: [string, number /* int */];
  parent: (string | undefined) | null;
}
```

A mapping without placeholders keeps the TypeScript generic
```yaml
type_mappings:
  nullable.Field: "Nullable"
```

```go
type Patch struct {
    Name nullable.Field[string] `json:"name,omitempty"`
}
```

```ts
export interface Patch {
  name?: Nullable<string>;
}
```
