# Redacció del useContext

## Què és el useContext i per què es important per gestionar dades globals? I característiques principals

El `useContext` és un **hook** de React que et permet *llegir* i *subscriure't* al **contingut** del teu component. Amb **subscriure** tenim clar que passem quelcom per una sèrie d'estats successius que van canviant gradualment.<br>
 **Proveeix** un camí per *accedir*, *gestionar* i *consumir* **estats** què es necessiten *compartir* a través de múltiples components.


És molt important per gestionar dades globals perquè **simplifica** la *compartició* sense la necessitat de fer *prop drilling*, què és passar l'estat a través dels components més alts fins els més baixos a l'arbre de components, i això ja es considera *mala praxis*. És molt útil alhora de compartir coses com els *theme settings*, *user authentification status*, o simplement un *estat global* a tota la teva aplicació.

---
### Com es combina amb un custom hook i l'encapsulació de la lògica del context

Per començar haurem de crear el context utilitzant la funció de `HookPersonalitzat.createContext(defaultValue)`. Llavors emboliquem (wrap) una part del nostre arbre de components, el que ens interessi que hagi d'accedir al contingut del Context, amb el `<HookPersonalitzat.Provider value={value}>`. <br> En aquest moment tot el que estigui dins del provider ( {children} ) tindrà accés a la informació del Context utilitzant dins del component `useContext(HookPersonalitzat)`. Tots els components que estiguin utlitzant el `useContext` automàticament es tornarant a renderitzar quan el value del Context canviï.

#### Exemple d'implementació

**Context.jsx**
```
export const ApiContext = createContext();

const API_BASE_URL = 'http://localhost:8080/api';

export const ApiProvider = ({ children }) => {
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  const apiClient = axios.create({
    baseURL: API_BASE_URL,
    headers: {
      'Content-Type': 'application/json',
    },
  });

  const get ...
  const post ...
  const put ...
  const remove ...

return (
    <ApiContext.Provider
      value={{
        loading,
        error,
        get,
        post,
        put,
        remove,
        setError
      }}
    >
      {children}
    </ApiContext.Provider>
  );
};
```

**App.jsx**
```
import { ApiProvider } from './context/ApiContext';

function App() {
  return (
    <ApiProvider>
        {children}
    </ApiProvider>
  );
}

export default App