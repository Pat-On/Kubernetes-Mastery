# Security Implications of Apply

## Security implications of `kubetl apply`

- when we do `kubectl apply -f <url>` we create arbitrary resources
- resources can be eveil, imagine a `deployment` that ..
  - start bitcoin minders on the whole cluster
  - hides in a non-default namespace
  - bind-mounts our node filesystems
  - insert SSH keys in the root account on the node
  - encrypts our data and ransoms it
  - !!!!!! :<

## kubectl apply is the ne curl | sh
- curl | sh is convenient
- it is safe is you use https urls from trusted sources
- kubectl apply -if is convenient
- it is safe is you use https urls from trusted sources
- example the official setup instructions for most pod networks