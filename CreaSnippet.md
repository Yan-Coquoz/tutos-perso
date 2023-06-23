## Creation d'un snippet

 Dans `VScode`
 appel d'un snippet pour que lors de sont appel il est toujours la même structure.

 Aller dans `fichier` , `préférences` puis  `Configurer les extraits utilisateur`.

 - une fenêtre apparait, selectionner `javascript.json` (babel) (pour React)
 - pour vue, selectionner `Nouveau fichier d'extraits globaux...`, puis nommé le fichier comme vous le souhaitez.
 On arrive sur une page qui presente se texte :

 ```json
 {
   // Place your snippets for javascript here. Each snippet is defined under a snippet name and has a prefix, body and
  // description. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
  // $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. Placeholders with the
  // same ids are connected.
  // Example:
  // "Print to console": {
  //  "prefix": "log",
  //  "body": [
  //   "console.log('$1');",
  //   "$2"
  //  ],
  //  "description": "Log output to console"
  }
  }
  ```

  copier le code de `Print to console` à la fin de la phrase de description, mettre la copie avant le `}` .

```json
}
 "Print to console": {
    "prefix": "log",
    "body": [
      "function ${machin}(){",
      "console.log('$1');",
       "$2"
       "}",
       "export default ${machin}",
    ],
   "description": "Log output to console"
 }
```

1. "description du nouveau snippet ":{
2. "prefix": "rte",                                 <= raccourci emmet que l'on veut
3. "body" : [ ,                                    <= apparence du code voulu, chaque ligne doit être `entre quotes` et toutes les lignes doivent avoir une `,` à la fin.
4. "const route = require(./modules/router)",    <= action voulu à l'appel de `rte`
5. "\t un truc indenté",                          <= une indentation au cas ou il aurait de la mise en forme avec `\t`
6. ],                                               <= bien fermer les crochets
7. "description" : "et voila une dernier desciption de ce que l'on veut",
8.
9. prochain snippet
10. Tous ce qui sera présent dans `${bidule}` sera changeable dès l'import
]

mes exemples React :

```json
}
 "Créer un composant stateless": {
  "prefix": "imprsl",
  "body": [
   "import React from \"react\";",
   "\n",
   "import \"./style.scss\"",
   "\n",
   "\t const ${composant} = (props)=> {",
   "\t//ecrire le code ici",
   "\t\t return(\n",
   "\t)",
   " };",
   "\n",
   "export default ${composant};",
  ],
  "description": "Import React & creer un composant stateless"
 },
 "Créer un composant statefull": {
  "prefix": "imprsful",
  "body": [
   "import React,{ Component } from \"react\";",
   "\n",
   "class ${App} extends Component {",
   "\t render() {",
   "\t\treturn(",
   "\n",
   "\t\t )",
   "\t };",
   "\n",
   "\t};",
   "export default ${App};",
  ],
  "description": "Import React & creer un composant statefull"
 },
 "Container React": {
  "scope": "javascript",
  "prefix": "container",
  "body": [
   "import { connect } from 'react-redux';",
   "import $1 from 'src/components/$1';",
   "",
   "const mapStateToProps = (state) => ({});",
   "",
   "const mapDispatchToProps = (dispatch) => ({});",
   "",
   "export default connect(mapStateToProps, mapDispatchToProps)($1);",
  ],
  "description": "création d'un container react"
 },
 "Middleware": {
  "prefix": "middleware",
  "body": [
   "const $1 = (store) => (next) => (action) => {",
   "  switch (action.type) {",
   "    default:",
   "      next(action);",
   "  }",
   "};",
   "",
   "export default $1;",
   "",
  ],
  "description": "Création d'une middleware sur Redux"
 },
 "Action": {
  "scope": "javascript",
  "prefix": "craction",
  "body": [
   "export const $1 = '$1';",
   "",
   "export const $2 = ($3)=>({;",
   "  type: $1,",
   "  $3,",
   "});",
   ""
  ]
 }
```

mes exemples Vue2 :
```json
{
  "vue2Template": {
    "prefix": "vue2Template",
    "description": "Création des différentes balises de Vue.js",
    "body": [
      "<template>",
      "\n\t<div></div>",
      "</template>",
      "\n<style scoped>",
      "</style>",
      "\n<script>",
      "import { defineComponent } from \"@vue/composition-api\";",
      "\nexport default defineComponent({",
      "name: \"\",",
      "components: {},",
      "\nprops:{},",
      "\nsetup(){},",
      "\ndata(){},",
      "\ncomputed:{},",
      "\nwatch:{},",
      "\nmethods:{}",
      "});",
      "</script>"
    ],
    "scope": "vue"
  }
}
```

