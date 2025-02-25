# Activitat_1, UF1841

## **La Immutabilitat a ReactJS i la seva Importància** 

### **Què és la immutabilitat?** 

La **immutabilitat** a ReactJS es refereix a la pràctica de **no modificar directament les dades** d'un objecte o estat, sinó que, es **crean noves còpies** amb els canvis necessaris. Aquest és un concepte fonamental en en el context de **ReactJS** on no volem que els elements o objectes es modifiquin o canviin al llarg del temps, en aquest cas treballarem amb **l'estat** i les **propietats** o *props* d'un element o objecte per poder canviar els valors necessaris.

---

### **Per què és important la immutabilitat a React? (principals característiques)**

- #### 1. Optimització del rendiment
  React utilitza el què anomenem **Virtual DOM**, un concepte de programació on una representació de la interfície es guarda a la memòria i es sincronitza amb el **DOM real** per mitjà d'una llibreria com el **ReactDOM**, que optimitza les actualitzacions de la interfície. A aquest procés l'anomenarem reconciliació. Quan un component canvia el seu estat i/o propietats del mateix, React fa una comparació entre la versió actual amb la versió anterior i només actualitza les parts necessàries del DOM real, què és el que veu l'usuari.

  - Si l'estat es modifica **directament**, React no pot detectar correctament els canvis, fent que l'aplicació no sigui eficient.
  - Amb la immutabilitat, cada canvi genera un **nou objecte** que permet a React detectar fàcilment quines parts del render han canviat i cal actualitzar.


  ```jsx
  // ❌ No modificar directament l'estat
  state.items.push("Nou Element"); // Això modifica l'array original!

  // ✅ Crear una nova còpia de l'array amb spread operator
  setState({ items: [...state.items, "Nou Element"] });
  ```
- #### 2. Evitar efectes secundaris no desitjats
  Haurem d'evitar per totes les maneres possibles modificar directament un objecte per tot el mencionat anteriorment perquè poden causar **efectes col·laterals** en la programació i poden ser *errors difícils de rastrejar*.

  ```jsx
  const user = { name: "Joan", age: 25 };

  // ❌ Això modifica l'objecte original
  user.age = 26;

  // ✅ Creem un nou objecte sense modificar l'original
  const updatedUser = { ...user, age: 26 };
  ```

- #### 3. Facilita el Control de versions de l'Estat 
  Moltes eines de desenvolupament, es basen en la immutabilitat per poder fer **seguiment dels canvis d’estat** i permetre accions com:

  - **Desfer i refer (undo/redo)**
  - **Time-travel debugging** (desplaçar-se a un estat anterior)
  - **Comparació d'estats per analitzar bugs**

  Si l'estat fos mutable, aquestes eines no podrien funcionar correctament.

- #### 4. Millor Mantenibilitat i Claredat del Codi 
  Un codi immutable és **més fàcil d’entendre** i **predictible**, ja que sempre es creen **noves versions dels objectes** en lloc de modificar-los.

  - Això fa que els components de React siguin més fàcils de mantenir.
  - Permet treballar amb **React.memo** i **useMemo**, que eviten renders innecessaris.

---
### Com la Immutabilitat s'aplica al cicle de renderització de Components
React re-renderitza un component quan el seu estat o *props* canvien. Si es modifica un objecte directament en lloc de crear-ne una còpia, React pot **no detectar correctament els canvis**, fent que la UI no es comporti com s'espera.

#### **Exemple d'un problema amb estats mutables**  
```jsx
const [user, setUser] = useState({ name: "Joan", age: 25 });

const updateAge = () => {
  user.age = 26; // ❌ Això NO provocarà una re-renderització!
  setUser(user); // React no detecta el canvi perquè l'objecte és el mateix.
};
```

✅ **Solució correcta (immutabilitat):**
```jsx
const updateAge = () => {
  setUser(prevUser => ({ ...prevUser, age: 26 })); // ✔️ Això sí provocarà un re-render!
};
```

---

## Cicle de Render: Trigger/Render/Commit

El cicle de render de React és divideix en tres parts molt importants:

- ### Trigger
  
  La fase de **trigger** és iniciada quan hi ha algún canvi en l'estat o les *props*. Això pot succeïr degut a varies raons:

  - Al render inicial quan els components es carrèguen.
  
  - A un canvi d'estat utilitzant per exemple el useState.
  
  - Un *prop* change desde un component pare.
  
  Quan alguna d'aquestes coses passen, React reacciona i fa un re-render del component.
  
- ### Render
  
  Durant la fase de **render**, React compara el nou *Virtual DOM* amb l'anterior. això determina quins canvis es necessiten fer per el DOM actual. Com hem dit anteriorment és el procés de reconciliació, en aquest procés React només determina quins canvis es necessiten fer per poder canviar el nou DOM.
  
- ### Commit
  
  A la fase de **commit** és on React actualitza el DOM basat en els canvis identificats prèviament en el **Render**. Només aplica els canvis necessaris, assegurant una actualització eficient. És important saber que React pot arribar a la fase de **Render** però no fer **Commit** si el component retorna el mateix resultat com a l'anterior **Render**.

Exemple:

Nosaltres podem clicar un botó que permet "Enviar" un formulari, aquest botó envia una señal al component per canviar l'estat d'aquest a "Enviant..". Llavors React detecta que el botó ja no està a l'estat anterior d'"Enviar" i el canvia a "Enviant..". En canvi la resta de la pàgina remana igual, només a renderitzat el canvi d'estat del botó.

---
### **Conclusió**  
L'ús de la **immutabilitat** a React **millora el rendiment**, **evita errors** i fa que el codi sigui **més fàcil de mantenir**. Per aquest motiu, és fonamental **crear noves instàncies de l'estat** en lloc de modificar directament els objectes o arrays existents.

<br>
<br>

# Activitat_2, UF1842

## **JSX a ReactJS: Què és i per què és tan important?**  

### **Què és JSX?**  
JSX (*JavaScript XML*) és una **extensió de JavaScript** que permet escriure codi HTML dins de JavaScript. És utilitzat a **ReactJS** per definir l’estructura dels components d’una manera més clara i llegible.  

Encara que el navegador no entén JSX directament, aquest és transformat en **codi JavaScript pur** mitjançant **Babel**, un transpilador que converteix el JSX en codi que els navegadors poden interpretar.  

---
### **Principals Característiques de JSX**

1. **S'introdueix dins de JavaScript**
   - Permet escriure HTML dins de JavaScript i combinar-ho amb lògica de programació.
2. **Millora la llegibilitat del codi**
   - Facilita la creació i manipulació de la interfície gràfica.
3. **Seguretat**
   - React escapa automàticament el codi JSX, evitant atacs XSS (Cross-Site Scripting).
4. **Facilita la creació de components reutilitzables**
   - La combinació de JSX amb props i state permet definir components dinàmics de manera eficient.
5. **Converteix el codi en JavaScript pur**
   - Els navegadors no entenen JSX directament, però Babel el transforma en codi JavaScript.

---
### **Avantatges de JSX envers JavaScript**

| **Característica**                 | **JSX** | **JavaScript tradicional** |
|------------------------------------|--------|---------------------------|
| Sintaxi intuïtiva                  | ✅ Sí  | ❌ No                      |
| Llegeix i escriu HTML directament  | ✅ Sí  | ❌ No                      |
| Integració amb React               | ✅ Òptima | ❌ Menys eficient        |
| Prevenció d’errors de sintaxi      | ✅ Sí  | ❌ No                      |
| Optimització automàtica            | ✅ Sí  | ❌ No                      |


---
### **Com JSX es pot aplicar a diferents projectes?**

- **Aplicacions web interactives**: 
JSX permet la creació de components dinàmics que reaccionen a canvis d’estat i interacció de l’usuari.

- **Aplicacions mòbils amb React Native**:
JSX també és utilitzat a React Native per crear aplicacions per iOS i Android amb una sintaxi similar a ReactJS.

- **Aplicacions empresarials i dashboards**:
Empreses utilitzen JSX per construir panells d’administració amb gràfics, taules i dades actualitzades en temps real.

- **Webs estàtiques amb frameworks com Next.js**:
JSX també s’integra amb frameworks com Next.js per generar webs estàtiques i dinàmiques optimitzades per SEO.

---
### Components de React

Una **Component** de React és funció de Javascript a la qual li pots posar etiquetes.És un dels conceptes cores de React. Són els pilars base on es construeixen les interfícies per l'usuari. 

React permet combinar els components de manera que els pots reutilitzar i nidificar entre ells.

---
### **Conclusió**
JSX és un element fonamental de ReactJS perquè facilita la creació d’interfícies, fa que el codi sigui més llegible i eficient, i s’integra perfectament amb el sistema de components de React, que et permet reutilitzar-los i nidificar-los entre ells.

<br>
<br>

# Activitat_3, UF1843

## **useState a ReactJS**  

### **Què és useState?**  
`useState` és un **hook de React** que permet **afegir estat als components funcionals**. Permet actualitzar i gestionar valors dins del component sense necessitat d'utilitzar classes.  

Aquest hook és ideal per gestionar estats **simples i locals** dins d'un component, com ara **comptadors, formularis o valors booleans**.

---

### **Diferències entre useState i useReducer**  

`useReducer` és un **hook avançat** que serveix com una alternativa a `useState` quan la lògica de l'estat és **més complexa** i implica múltiples subvalors o transicions d'estat. En lloc d'actualitzar directament un estat, `useReducer` utilitza una **funció reductora** per modificar l'estat a partir d'accions definides.

| **Característica**           | **useState**                      | **useReducer**                     |
|-----------------------------|----------------------------------|------------------------------------|
| Simplicitat                 | ✅ Fàcil d'usar                 | ❌ Més complex                     |
| Estat complex               | ❌ Poc eficient per estat complex | ✅ Ideal per estats amb lògica     |
| Rendiment                   | ✅ Ràpid per estats senzills     | ✅ Millor per estats amb múltiples accions |
| Forma de modificar l'estat  |  Funció `setState`             |  `dispatch` i accions           |
| Ús recomanat                |  Estat simple i directe       |  Estat complex amb múltiples accions |

---

## **Principals avantatges de useState i useReducer**  

### **Avantatges de useState**  
-  Fàcil d'implementar en components senzills.  
-  Menys codi i més intuïu.  
-  Ideal per estat local dins d'un component.  

### **Avantatges de useReducer**  
-  Millor gestió de lògica d'estat complexa.  
-  Evita problemes amb estats derivats.  
-  Recomanat per aplicacions grans amb molts components connectats.  

---

## **Aplicació de useState i useReducer en projectes**  

-  **useState** es pot utilitzar en:  
    - Formularis senzills amb camps d’entrada.  
    - Comptadors i interaccions bàsiques.  
    - Canvis d’estat locals en components petits.  

-  **useReducer** es pot utilitzar en:  
   - Gestió d’estat global en aplicacions grans.  
   - Aplicacions amb múltiples tipus d’accions en estat.  
   - Panells d’administració amb moltes opcions.  

---
### Més exemples

#### Exemples amb `useState`

1. **Comptador bàsic**: Un comptador que es pot incrementar i disminuir.
2. **Control de formulari**: Gestionar el valor de camps de text en un formulari (per exemple, el nom d'un usuari).
3. **Visibilitat d'un element**: Canviar l'estat de visibilitat d'un component o element (per exemple, mostrar o amagar un quadre de diàleg).
4. **Temporitzador**: Gestionar l'estat de temps passat en un temporitzador (per exemple, iniciar, aturar o reiniciar un rellotge).
5. **Activar/desactivar un botó**: Controlar si un botó ha d'estar activat o desactivat en funció d'altres accions.

#### Exemples amb `useReducer`

1. **Gestió de l'estat d'un formulari**: Mantenir l'estat de diversos camps d'entrada (per exemple, nom, correu electrònic) i manejar les actualitzacions per cada camp.
2. **Comptador amb múltiples accions**: Un comptador que pot incrementar, disminuir o reiniciar en funció d'accions específiques.
3. **Carro de la compra**: Afegir, eliminar o actualitzar articles en un carro de la compra, mantenint un estat més complex.
4. **Gestió de l'estat de l'autenticació**: Controlar l'estat de connexió de l'usuari (per exemple, iniciar sessió, tancar sessió, etc.).
5. **Cicle de vida d'una petició API**: Gestionar l'estat d'una petició a una API (per exemple, carrega, èxit, error).



---
## **Conclusió**  
-  **useState** és ideal per **estat senzill i local**.  
-  **useReducer** és millor per **estat complex** i amb múltiples accions.  

L'elecció entre `useState` i `useReducer` depèn de la **complexitat del projecte** i de com es gestiona l’estat a ReactJS.