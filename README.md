# Ilojo Bar

Ilojo Bar of Casa do Fernandez was een beeldbepalend nationaal monument in Lagos, Nigeria, dat in 2016 illegaal werd gesloopt. Ilojo Bar werd ontworpen en gebouwd door Afrikanen die in de negentiende eeuw terugkeerden uit slavernij in Brazilië. Legacy wil graag een Engelstalige website die een soort virtueel monument wordt van dit bijzondere gebouw en de vele verhalen er omheen.

## Inhoudsopgave
  * [Het probleem](#het-probleem)
  * [Debriefing](#debriefing)
  * [Design challenge](#design-challenge)
  * [Gekozen user story](#gekozen-user-story)
  * [Oplossing](#oplossing)
  * [Uitleg van de code](#uitleg-van-de-code)
  * [Volgende stappen](#volgende-stappen)


## Het probleem
De Ilojo Bar is in 2016 gesloopt, terwijl dit niet legaal was. Hierdoor heeft Lagos een monumentaal pand minder. Het pand is nu misschien verloren gegaan, maar de verhalen die eromheen hangen niet. Aan ons de taak om deze verhalen op een digitale manier te vertellen.

## Debriefing

#### Contactgegevens
Femke van Zeijl is een journaliste die sinds 2012 haar werk doet vanuit Lagos Nigeria. Op dit moment is Femke bezig met een project over de Ilojo bar. Hier heeft ze ook een scriptie over geschreven voor haar master African Studies. Samen met het bedrijf Legacy (Zij zetten zich in om de erfgoed en geschiedenis van Nigeria te behouden en promoten) zet ze haar onderzoek door na de tragische vernieling van de bar in 2016.

Mail: femke@fvz-journaliste.nl

#### Achtergrondinformatie
De bar is gemaakt door Afro-Brazilianen die terugkeerde van de slavernij. Deze personen kwamen goed geschoold terug, vaak ook in de achtergrond als timmerlui. Zo hebben ze het pand op kunnen bouwen in de Braziliaanse stijl. Het pand en de grond was eerst van een Spanjaard. Dit was de eerste eigenaar, deze Spanjaard (José Amoedo Fernandez) kwam uit Galicië wat in die tijd één van de armere delen was van Spanje. Later is het pand van familie naar familie gegaan en opgekocht door andere. Het pand werd als laatst gebruikt als woning en niet meer als restaurant of bar.

#### Gebruikerscontext
In Nigeria worden in de steden vrij moderne apparaten gebruikt. Denk aan Iphone modellen van drie jaar geleden. Buiten de stad gebruiken mensen wat ze kunnen krijgen. Dit zijn vaak 'afdankertjes' van de mensen in de stad. De internetverbinding is het grootste pijnpunt in Nigeria. Dit wil nog wel eens wegvallen en is erg traag. Desktops worden aanzienlijk minder gebruikt dan mobiele apparaten.

#### Opdrachtomschrijving
De opdracht is het maken van een digitaal monument van de Ilojo bar. Voornamelijk gericht op het vertellen van de geschiedenis van de bar.

#### Aanleiding
De Ilojo bar is in 2016 gesloopt, onterecht. Het was een monumentaal pand. Dus nu moet het herbouwd worden.

#### Doelstelling
Laten zien wat je nog kan doen met erfgoed dat er niet meer is.

#### Oplevering
Iedereen maakt zijn eigen project en zal dit opleveren.

#### Randvoorwaarden
-	Voor mobiel moet het goed werken
-	Verhalen vertellen
-	Verhalen insturen en modereren

#### Gebruikers van het eindresultaat
1.	Mensen die in Lagos wonen.
2.	Nigerianen, ook voor Nigerianen in andere landen.
3.	Wereldburgers

#### Relatie met andere projecten
Legacy waar Femke nu mee samenwerkt heeft al eerdere projecten gedaan met betrekking tot het behouden van cultureel erfgoed in Nigeria.

## Design challenge
Ontwerp en ontwikkel een interactief, virtueel monument voor Ilojo Bar.
Aantrekkelijk én functioneel voor inwoners van een land met lage bandbreedte, waar velen alleen via hun mobiel het internet gebruiken, terwijl het ook voor desktop mooi is.

## Gekozen user story
### Verhalen over Ilojo Bar lezen, luisteren en bekijken
Als inwoner van Lagos, Nigeriaan, lid van de Nigeriaanse diaspora of geïnteresseerde wereldburger, wil ik online verhalen over Ilojo Bar kunnen lezen, luisteren en zien, zodat ik meer te weten kan komen over de betekenis van het gebouw voor de miljoenenstad Lagos en van de kosmopolitsche geschiedenis ervan, die van Spanje tot Brazilië tot Nigeria leidt.


## Oplossing
Om het huidige probleem op te lossen hebben wij gekozen om ieder verhaal een eigen karakter mee te geven. De rode draad van ons project is wel het journalistieke werk wat gedaan is door Femke van Zeijl. Doormiddel van een storytelling approach en een visuele aanpak brengen wij deze verhalen tot leven. Zo heeft de gebruiker het idee dat hij of zij daadwerkelijk in dat verhaal zit.

Onze digitale oplossing: https://ilojo-bar.vercel.app/ (alleen op mobiel beschikbaar)

## Uitleg van de code
### Next.js
Voor dit project hebben we Next.js gebruikt. Next.js is een framework bovenop React wat ervoor zorgt dat we serverside code kunnen schrijven. Dit kan niet in React. Naast, het kunnen schrijven van serverside code, heeft Next.js nog een aantal belangrijke voordelen. 

Next heeft een aantal fijne optimalisatie's:
1. Het <Image /> component zorgt voor geoptimaliseerde responsive afbeeldingen
2. Font optimalisaties
3. Stel loading priority van <Scripts /> in. 
4. Caching headers
5. Minified files
6. Pre-rendering pages (met getStaticProps()).

Deze optimalisatie's zijn voor ons de reden geweest om Next.js te gebruiken. De apparaten en verbindingen in Nigeria zijn minder krachtig en stabiel als hier. En dus wilde wij er zeker van zijn dat het met de performance van onze website goed zit. 
<img src="https://github.com/DaanKetelaars/ilojo-bar/blob/main/assets/performance.png" alt="data model" width="550px" /> 



### Data model
<img src="https://github.com/DaanKetelaars/ilojo-bar/blob/main/assets/data-model.png" alt="data model" width="350px" /> 
In het data model is te zien hoe de data, in dit geval de content voor website, zich door de website verspreid. 

We versturen de data uit het CMS (Content Management Systeem) via GraphQL. Deze halen we binnen in API.js (zie code hieronder). In API.js pakken we de data uit en versturen we het naar Index.js. In Index.js laden we uiteindelijk data in als de pagina door de browser wordt aangevraagd. Middels een Context provider verdelen we uiteindelijk de data over de Components. 

### Context Provider
Omdat wij Next gebruiken werken wij server-side. Het ophalen van onze data vanuit ons CMS doen wij ook server-side. Toch was het voor ons wat lastig om dit door te brengen naar client-side components. Uiteindelijk kwamen wij uit op Context Provider. Context geeft je de optie om data te kunnen versturen naar je component level. Dit was nodig om zo onze content uit het CMS te kunnen tonen in de website. 

Ik zal even laten zien hoe wij nu data ophalen.

```jsx
//../lib/api.js

import {
  GraphQLClient,
  gql
} from 'graphql-request';
const graphcms = new GraphQLClient(process.env.GRAPHCMS_ENDPOINT);
let mains;
let blocks;
let header;
let footer;

export async function getAllStories(section) {
  const query = gql `
    {
      mains {
        blocks {
          ... on Story {
            id
            bodytext01 {
              text
            }
            bodytext02 {
              text
            }
            images {
              id
              url
            }
            title
            subtitle
          }
        }
      }
      headersConnection {
        edges {
          node {
            heading
            id
            image {
              url
              id
            }
          }
        }
      }
      footersConnection {
        edges {
          node {
            title
            image {
              url
              id
            }
          }
        }
      }
    }
  `;

  const results = await graphcms.request(query);
  mains = results.mains;
  mains.forEach((item) => {
    blocks = item.blocks;
  });
  results.headersConnection.edges.forEach((result) => {
    header = result.node;
  });
  results.footersConnection.edges.forEach((result) => {
    footer = result.node;
  });

  const sections = {
    blocks,
    header,
    footer,
  };
  return sections;
}

```

Omdat wij gebruik maken van GraphCMS, wat gemaakt is door GraphQL, kunnen wij gemakkelijk op die manier data inladen. Zo kiezen wij wat er nodig is. Uiteindelijk doen wij nog een forEach om in de juiste array of object te komen. Dit word gereturnd, zodat wij dit via onze context provider kunnen gebruiken in pages en components. Dus api.js moet je zien als ons fetchData bestand.

Hierna maak je een context bestand aan, op google komen er verschillende versies voorbij. De één heel ingewikkeld en de ander heel simpel. Uiteindelijk hebben wij vrij weinig code nodig gehad om tot het gewenste resultaat te komen.

```jsx
//../context/state.js

import { createContext } from "react";
export const Context = createContext();

```

De volgende stap is de variabel "Context" toevoegen aan je index.js. Doe je dit niet wordt het vrij lastig om je data door te sturen.
Dit ziet er als volgt uit.

```jsx
import Main from '../components/main/Main';
import Header from '../components/header/Header';
import Footer from '../components/footer/Footer';
import { Context } from '../context/state';
import React, { useState } from 'react';
import { getAllStories } from '../lib/api';
import Script from 'next/script';
import Head from 'next/head';

export default function Home({ stories }) {
  const [context, setContext] = useState(stories);

  return (
    <Context.Provider value={[context, setContext]}>
      <Head>
        <title>The stories of Ilojo bar.</title>
        <meta name="viewport" content="initial-scale=1.0, width=device-width" />
        <link rel="icon" href="/images/home/favicon.svg" type="image/svg+xml"></link>
      </Head> 
      <div>
        <div className='grain'></div>
        <Header />
        <Main />
        <Footer />
        <Script strategy='lazyOnload' src='/js/generateHeading.js' />
        <Script strategy='lazyOnload' src='/js/scrollJacking.js' />
        <Script strategy='lazyOnload' src='/js/InView.js' />
      </div>
    </Context.Provider>
  );
}

export async function getStaticProps() {
  const stories = (await getAllStories()) || [];

  return {
    props: { stories },
  };
}

```
De belangrijkste stukjes hierin voor het versturen van de data zijn deze.


```jsx
import { Context } from '../context/state';
import React, { useState } from 'react';
import { getAllStories } from '../lib/api';

```
Hier importeren wij ons api.js en de functie. In de functie getAllStories zit onze data vanuit het CMS. Ook importeren wij de context provider. En als laatst de useState. Met useState gaan wij onze context provider koppelen aan ons index.js bestand.

```jsx
export default function Home({ stories }) {
  const [context, setContext] = useState(stories);
  
```
Aan Home voegen wij een prop toe. Deze prop komt weer vanuit de getAllStories en getStaticProps, die onderin staat.
Daaronder staat de useState. useState is een Hook waarmee je state variables in functional components kunt hebben. Daar voegen wij nogmaals de prop stories toe.

```jsx
<Context.Provider value={[context, setContext]}></Context.Provider>

```

In de context provider die om alle andere code staat in ons index.js wordt er een value meegegeven. Dit is dan weer de useState. Zoals je ziet geef je stap voor stap de data door. Het is even zoeken, maar als je het doorhebt is het wel te doen. 

```jsx
export async function getStaticProps() {
  const stories = (await getAllStories()) || [];

  return {
    props: { stories },
  };
}
```
Als laatst voegen wij een getStaticProps functie toe. Dit is een functie vanuit Next.JS om data binnen te halen. Voor ons was dit de meest ideale optie met ons CMS. Er zijn ook nog andere functies in Next.JS, maar die waren niet in ons voordeel. getStaticProps werkt eigenlijk ook wel het best. In deze functie doen wij een async await van getAllStories en maken we de prop aan die bovenin weer toegevoegd wordt.


Dan hebben we nog de allerlaatste stap. Het gebruiken van je data. Ik pak even onze main waar wij ons story component maken. Hier zitten weer wat functies en code die hierboven ook al gebruikt is. Het enige verschil is dat je nu eindelijk kan filteren binnen in de data.

```jsx
// Styles
import styles from '../../styles/main/Main.module.scss';
import Image from 'next/image';

import React, { useContext } from 'react';
import { Context } from '../../context/state';

export default function Main() {
  const [context] = useContext(Context);
  const stories = context.blocks;
  return (
    <main className={styles.main}>
      {stories.map((ctx, i) => (
        <article key={i}>
          {ctx.subtitle !== null ? <h4>{ctx.subtitle}</h4> : ''}
          <h2>{ctx.title}</h2>
          {ctx.bodytext01.text !== '' ? <p>{ctx.bodytext01.text}</p> : ''}
          {ctx.bodytext02.text !== '' ? <p>{ctx.bodytext02.text}</p> : ''}
          {ctx.images.map((image) => {
            return (
              <div key={image.id} className='article-img'>
                <Image
                  src={image.url}
                  alt='foto'
                  layout='responsive'
                  width='100%'
                  height='100%'
                  objectFit='contain'
                />
              </div>
            );
          })}
        </article>
      ))}
    </main>
  );
}

export async function getStaticProps() {
  const stories = (await getAllStories()) || [];
  return {
    props: { stories },
  };
}

```

```jsx
  const stories = context.blocks;
  
   {stories.map((ctx, i) => (
        <article key={i}>
          {ctx.subtitle !== null ? <h4>{ctx.subtitle}</h4> : ''}
          <h2>{ctx.title}</h2>
          {ctx.bodytext01.text !== '' ? <p>{ctx.bodytext01.text}</p> : ''}
          {ctx.bodytext02.text !== '' ? <p>{ctx.bodytext02.text}</p> : ''}
          {ctx.images.map((image) => {
            return (
              <div key={image.id} className='article-img'>
                <Image
                  src={image.url}
                  alt='foto'
                  layout='responsive'
                  width='100%'
                  height='100%'
                  objectFit='contain'
                />
              </div>
            );
          })}
        </article>
      ))}
      
```
Dit is het enige wat anders is dan de index.js. Hier pakken we de prop "stories" die op dit moment alle data meeneemt en gaan we wat dieper op de code in. Voor deze pagina pakken we content.blocks. Blocks is een object die in onze query staat. Binenn in blocks staat alle data die nodig is om onze verhalen te tonen.

Het is even wat werk en was ook aardig zoeken naar de juiste opzet. Toch als je eenmaal begrijpt is het wel duidelijk. Met hooks kun je ook veel kanten op en ze bieden je veel meer opties. Dat is wel één van de dingen met React, je moet vaak alles omzetten en omdenken naar de logica van Hooks.


## Volgende stappen
-- (het hele verhaal op eigen pagina) (responsive) (3d model in de footer geanimeerd) 


## Licentie

![GNU GPL V3](https://www.gnu.org/graphics/gplv3-127x51.png)

This work is licensed under [GNU GPLv3](./LICENSE).
