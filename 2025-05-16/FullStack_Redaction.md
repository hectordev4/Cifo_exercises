# Redacció Full-Stack

## Què és un framework full stack com Vaadin i per què és avantatjós per al desenvolupament web?

Un framework full-stack és un entorn de desenvolupament que *proporciona totes les eines necessàries* per crear tant el **frontend** com el **backend** d'una aplicació de manera **integrada** i **coherent**. En el cas de *Vaadin*, és un framework Java que permet construir aplicacions web modernes completament amb Java, sense necessitat d'escriure HTML, CSS o JavaScript manualment.<br>

Els avantatges d'utilitzar el sistema full-stack són que ofereix **versatilitat** i **flexibilitat** permetent als developers poder manegar diversos aspectes del projecte. Permèt *l'utilització eficient dels recursos* reduïnt la necessitat de separar especialistes. Això desemboca a uns *cicles de desenvolupament més ràpid i millor col·laboració entre equips*.

## Quines són les característiques clau de Flow i Hilla? Com simplifiquen el desenvolupament?

- **Full Stack**: Permeten construir tant el frontend com el backend de l'aplicació de manera integrada.

- **Two-Way Data Binding**: Sincronització automàtica entre dades del backend i la interfície d'usuari.

- **Integració amb Spring Boot**: Ambdós es poden integrar fàcilment amb Spring Boot per gestionar serveis i repositoris.

- **Components UI rics**: Ofereixen una llibreria completa de components web per construir interfícies modernes.

- **Seguretat integrada**: Proveeixen mecanismes per gestionar autenticació i permisos d'accés.

- **Routing integrat**: Gestió de rutes de navegació directament des del framework.

Per Flow i Hilla tenim un parell de característiques personals per a cadascún:

- **Vaadin Flow**: Permet crear frontend i backend només amb Java, sense HTML ni JavaScript.

- **Vaadin Hilla**: Genera automàticament clients TypeScript per al frontend en React o Lit, eliminant la configuració manual d'APIs.


#### Exemple d'una aplicació desenvolupada amb Flow o Hilla:

**Backend**
```
package com.example.application;

import dev.hilla.Endpoint;
import dev.hilla.Nonnull;

@Endpoint
public class GreetingEndpoint {

    public String sayHello(@Nonnull String name) {
        return "Hola, " + name + "!";
    }
}
```
**Frontend**
```
import { useState } from "react";
import { GreetingEndpoint } from "./generated/endpoints";

export function App() {
  const [name, setName] = useState("");
  const [greeting, setGreeting] = useState("");

  const handleClick = async () => {
    const response = await GreetingEndpoint.sayHello(name);
    setGreeting(response);
  };

  return (
    <div>
      <input
        type="text"
        placeholder="Escriu el teu nom"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <button onClick={handleClick}>Saluda</button>
      <p>{greeting}</p>
    </div>
  );
}
```

## Què significa integració tipus-segura?

Integració tipus-segura significa que *la comunicació entre el frontend i el backend* està **garantida** perquè les dades enviades i rebudes *respecten els tipus definits en el codi* (per exemple, Strings, números, objectes), evitant errors de tipus durant l’execució. Això es fa generant automàticament el codi client amb els tipus correctes a partir del backend, assegurant **coherència** i **robustesa** en l’intercanvi d’informació.