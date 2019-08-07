# Card

**KCard** is meant to highlight content in grids or group relative information together.

&nbsp;
<KCard title="Card Title" body="Body Content"/>

```vue
<KCard title="Card Title" body="Body Content"/>
```

## Props
### title
String to be used in the title slot.

- `title`

<KCard title="Title">
  <template slot="body">
    I am the body.
  </template>
</KCard>

```vue
<KCard title="Title">
  <template slot="body">
    I am the body.
  </template>
</KCard>
```

If the title is ommitted, then KCard acts as a generic Box element.

<KCard>
  <template slot="body">
    I am a box. I have padding and a border. Useful for composing other components
  </template>
</KCard>

```vue
<KCard>
  <template slot="body">
    I am a box. I have padding and a border. Useful for composing other components
  </template>
</KCard>
```

Example composing `KCard` with other Kongponents to make another component:

<KCard :hasHover="true">
  <template slot="body">
    <KAlert alert-message="Welcome to Kong!" />
    <div class="mx-4">
      <div style="display: flex; justify-content: space-between; align-items: center;">
        <h2>Kong Enterprise Edition</h2>
        <KButton to="https://docs.konghq.com/enterprise" target="_blank">
          Docs
        </KButton>
      </div>
      <div class="mt-2">
        <p>Kong Enterprise adds features, functionality, and performance to Kong. This documentation doesn’t cover the general practices that are common to both Kong and Kong Enterprise—learn the basics in Kong documentation.</p>
      </div>
    </div>
  </template>
</KCard>


```vue
<KCard :hasHover="true">
  <template slot="body">
    <KAlert alert-message="Welcome to Kong!" />
    <div class="mx-4">
      <div>
        <h2>Kong Enterprise Edition</h2>
        <KButton to="https://docs.konghq.com/enterprise" target="_blank">
          Docs
        </KButton>
      </div>
      <div class="mt-2">
        <p>Kong Enterprise adds features, functionality, and performance to Kong. This documentation doesn’t cover the general practices that are common to both Kong and Kong Enterprise—learn the basics in Kong documentation.</p>
      </div>
    </div>
  </template>
</KCard>
```

### Body
String to be used in the body slot.

- `body`

<KCard body="I am the body."/>

```vue
<KCard body="I am the body."/>
```

### Border Variants
Sets top border or no border. If neither set default will have border

- `borderTop`
- `noBorder`

<div class="borderless-cards">
  <KCard
    title="Card without border"
    body="Body Content"
    borderVariant="noBorder"/>

  <KCard
    title="Card with top border"
    body="Body Content"
    borderVariant="borderTop"/>
</div>

```vue
<KCard
  title="Card without border"
  body="Body Content"
  borderVariant="noBorder"/>

<KCard
  title="Card with top border"
  body="Body Content"
  borderVariant="borderTop"/>
```

### Hover
Sets if card has hover state (shadow)

- `hasHover` 

<KCard
  title="Card Title"
  body="Body Content"
  hasHover/>

```vue
<KCard
  title="Card Title"
  body="Body Content"
  hasHover/>
```

## Slots
- `title`
- `body`
- `actions` - Right side of title. Used for links, buttons, etc

&nbsp;
<KCard>
  <template slot="title">Look Mah!</template>
  <template slot="actions"><a href="#">View All</a></template>
  <span slot="body">Body slot content here</span>
</KCard>

```vue
<KCard>
  <template slot="title">Look Mah!</template>
  <template slot="actions">
    <a href="#">View All</a>
  </template>
  <span slot="body">Body slot content here</span>
</KCard>
```

<style lang="scss">
.borderless-cards {
  padding: 1rem;
  background: rgba(27,31,35,0.05);
  border-radius: 3px;
  .kong-card {
    background: #fff;
  }
}
</style>