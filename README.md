# Spécification du produit CANEL
spécifications canel

```mermaid
graph LR
App[Application] -- 1:n --> Inst[Instance]
App -- 0:n --> App
Inst -- n:1 --> Env[Environnement]
TypeConf[Type Conformité] -- 1:n --> Conf[Conformité] -- n:1 --> App
App -- 1:n --> Inst[Instance]
Inst -- n:1 --> Env[Environnement]
App -- 1:n --> Pile[Pile Technique]
Pile -- n:1 --> Tech[Technologie]
Tech -- 0:n --> Tech
```
