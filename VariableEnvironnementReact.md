# Comment utiliser les variables d’environnement avec React

A la racine de votre projet créer un fichier `.env`

A l’intérieur toutes les variables doivent obligatoirement commencer par `REACT_APP` suivit du nom de la variable puis de sa valeur.

```env
REACT_APP_NAME=Yan Coquoz
```

puis dans votre composant `process.env.REACT_APP_NAME` :

```javascript
import React from "react";
import "./App.scss";

const App = () => {
  return (
    <div className="App">
      <h1>Name {process.env.REACT_APP_NAME}</h1>
    </div>
  );
};

export default App;
```

Attention, il est important de redémarré le serveur de React pour que la variable d'environnement soit prise en compte.
