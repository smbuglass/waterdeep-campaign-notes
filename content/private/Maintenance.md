---
title: Maintenance
---
# Missing Title Frontmatter
```dataview
LIST from ""
WHERE !title
```
# Orphans
```dataview
TABLE file.ctime AS "updated"
FROM "" WHERE length(file.inlinks) = 0
AND length(file.outlinks) = 0
AND length(file.tags) = 0
AND file.name != "Maintenance"
AND !contains(file.path, "templates")
AND !contains(file.path, "private")
SORT file.mtime desc
```
# Dead Links
```dataviewjs  
let r = Object.entries(dv.app.metadataCache.unresolvedLinks) .filter(([k,v])=>Object.keys(v).length) .flatMap(([k,v]) => Object.keys(v).map(x=>dv.fileLink(x)))  
dv.list([...new Set(r)])  
```
# Places Missing from ToC
```dataview
LIST file.inlinks 
FROM "notes/Places"
```

