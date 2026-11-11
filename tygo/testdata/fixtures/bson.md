BSON tags name fields, and their `omitempty` / `omitzero` make them optional
```go
type Event struct {
    ID        string `bson:"_id"`
    OrgID     string `bson:"org_id"`
    Subtitle  string `bson:"subtitle,omitempty"`
    PublishAt string `bson:"publish_at,omitzero"`
}
```

```ts
export interface Event {
  _id: string;
  org_id: string;
  subtitle?: string;
  publish_at?: string;
}
```

`bson:"-"` skips the field
```go
type Session struct {
    Token  string `bson:"token"`
    Secret string `bson:"-"`
}
```

```ts
export interface Session {
  token: string;
}
```

A `bson` tag wins over a `json` tag, for both the name and optionality
```go
type Ticket struct {
    TicketDateID string `json:"ticketDateId,omitempty" bson:"ticket_date_id"`
    Name         string `json:"name" bson:"name,omitempty"`
}
```

```ts
export interface Ticket {
  ticket_date_id: string;
  name?: string;
}
```

`json:"-"` still skips the field even when it has a `bson` tag
```go
type Upload struct {
    Key  string `bson:"key"`
    Data string `json:"-" bson:"data"`
}
```

```ts
export interface Upload {
  key: string;
}
```
