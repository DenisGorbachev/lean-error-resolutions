# Cannot find synthesization order

## Situation 1

### Code

```lean
class Parent (α β : Type) where
  some : α
  other : β

class Child (γ : Type) (α β : outParam Type) extends Parent α β where
  field : γ
```

### Message

```lean
cannot find synthesization order for instance Child.toParent with type
  (γ : Type) → {α β : outParam Type} → [self : Child γ α β] → Parent α β
all remaining arguments have metavariables:
  Child ?γ α β
```

### Solutions

#### Change the type of each offending argument from `A` to `semiOutParam A`

```diff
-class Child (γ : Type) (α β : Type) extends Parent α β where
+class Child (γ : semiOutParam Type) (α β : Type) extends Parent α β where
```

#### Change the type of each offending argument from `A` to `outParam A`

```diff
-class Child (γ : Type) (α β : Type) extends Parent α β where
+class Child (γ : outParam Type) (α β : Type) extends Parent α β where
```
