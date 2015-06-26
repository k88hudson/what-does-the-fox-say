# React Application Flow

Testing out different kinds of data flow

`npm install && npm start` to run

## Only use state at the topmost level where a distinct model is created. Otherwise, use props directly.

### Parent to child

In this example, `name` is used by the `<Parent>` component, but `happy` and `awesome` are only used by the `<Child />` component.

```
<Parent>
  props: [empty]
  state: {
    name: 'Jo'
  }

  <Child name={this.state.name} />
    props: {
      name: 'Jo'
    }
    state: {
      happy: true,
      awesome: true
    }
  </Child>

<Parent>
```

### Sibling to sibling

Use a parent as an intermediary for a shared data model.

```
<Parent>
  props: [empty]
  state: {
    loading: true
  }

  <Child loading={this.state.loading} />
    props: {
      loading: true
    }
    state: [empty]
  </Child>

  <Loading loading={this.state.loading} />
    props: {
      loading: true
    }
    state: [empty]
  </Loading>

<Parent>
```

## For two-way bindings in parent-child and sibling relationships, use a callback API.

### Child <=> Parent

```
<Parent>
  props: [empty]
  state: {
    name: 'Jo'
  }
  setName: (newName) => {
    this.setState({name: newName});
  }

  <Child name={this.state.name} setName={this.setName} >
    props: {
      name: 'Jo'
    }
    state: [empty]
  </Child>

<Parent>
```

### Sibling <=> Sibling

Use a parent as an intermediary for a shared data model.

```
<Parent>
  props: [empty]
  state: {
    loading: true
  }
  setLoading: (newLoading) => {
    this.setState({loading: newLoading});
  }

  <Child loading={this.state.loading} setLoading={this.setLoading} />
    props: {
      loading: true,
      setLoading: [function]
    }
    state: [empty]
  </Child>

  <Loading loading={this.state.loading} />
    props: {
      loading: true
    }
    state: [empty]
  </Loading>

<Parent>
```

## Use an event emitter for grandparent/deep-child relationships.

### One way bindings

[todo]

### Two way bindings

[todo]
