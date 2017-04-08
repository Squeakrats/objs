# objs.js

## Description
Simple obj file loader written in Javascript. Useful for loading files via ajax or parsing pre-loaded text. Should be compatible with every model [here]( http://people.sc.fsu.edu/~jburkardt/data/obj/obj.html) (except the pyramid). Please note that this library only supports a subset of the obj format. 

## Previewing
To see if the library supports your model head over [here](https://squeakrats.github.io/TFWGF/) and upload it. It will show you a preview and probably save you some debugging time. 

## Usage 

### Ajax
```javascript
Objs.loadObj("../test/skyscraper.obj").then((skyscraper)=> {
  // Do things with skyscraper
  console.log(skyscraper);
})
```

### Text

#### Raw String
```javascript
let model = Objs.parseObj(RawOBJString);
// Do things with skyscraper
console.log(model);
```

#### [TFWGF Loader]( http://people.sc.fsu.edu/~jburkardt/data/obj/obj.html)
```javascript
let model = PreLoadedAssets["skyscraper.obj"]
// Do things with skyscraper
console.log(model);
```

## Data Structures

### Vertex Format
```javascript
{
       v  : // <vertex position index in model vertices list>
       vt : // <vertex texture coordinate index in model UVs list>
       vn : // <vertex normal index in model normals list>
}
```

### Face Format
```javascript
{
       a  : // <first Vertex> * See above data structure. These are NOT the vertex positions
       b  : // <second Vertex>
       c  : // <third Vertex>
       m : // <material Index>
}
```

### Model Format
```javascript
{
        vertices :  [v1, v2, v3, ... ], // where each element is an array [x, y, z]
        normals :  [n1, n2, n3, ... ], // where each element is an array [x, y, z]
        UVs :  [uv1, uv2, uv3, ... ], // where each element is an array [u, v, w]
        faces :  [f1, f2, f3, ...], // where each element is a Face
        groups :  { groupname : [f1, f2, f3, ... ] }, // where each f element is a Face
        materials :  [materialname1, materialname2, ... ],
        mtllibs :  [filename1, filename2, ... ]
}
```
### Examples
See examples folder for more specific examples

### Example (Average vertex)
```javascript
let model = Objs.parseObj(RawOBJString);
let sum = [0, 0, 0]
for(let vertex of model.vertices)
  for(let i = 0; i < 3;i++)
    sum[i] += vertex[i]

let c = model.vertices.length;
sum[0] /= c;
sum[1] /= c;
sum[2] /= c;
console.log(sum)
```

### Example (Iterate Over Faces And Print Vertex Positions)
```javascript
let model = Objs.parseObj(RawOBJString);
let vertices = model.vertices;

for(let face of model.faces) {
  let v1 = vertices[face.a.v]
  let v2 = vertices[face.b.v]
  let v3 = vertices[face.c.v]
  console.log(v1 + "," + v2 + "," + v3);
}

```
