# prova_DS_SaloOcupacio2024

README
1. Introducció
Aquest projecte analitza un conjunt de dades obtingut d'una enquesta sobre la bretxa digital a la ciutat de Barcelona (https://opendata-ajuntament.barcelona.cat/data/ca/dataset/enquesta-escletxa-digital). 
EL DF que he importat conté 2.542 enquestes de població de Barcelona de 16 anys i més que es va dur a terme entre el 15 d’octubre al 2 de novembre de 2020 per l'Institut Opinòmetre, aixo dona un DF de 135 columnes amb una majoria de dades numèriques (Float103), seguit de Int64(31) i object(1).

2. Depuració de dades
La depuració de dades es va dur a terme mitjançant diverses tècniques de preprocessament per assegurar la qualitat i la utilitat del conjunt de dades per a l'anàlisi. 

De les 135 columnes inicial, he decidit crear un nou DF_final amb 34 variables relatives a les informacions de perfil, usatge technologic a la llar. En aquest nou DF amb nom DF_final, les variables han estat mapades amb les etiquetes descriptives de l'informacio_de_variables.csv per facilitar la comprensió. He decidit de no incloure les següents variables, ja que no aporten informació rellevant o bé són redundants en relació amb altres variables del conjunt de dades:'resideix_a_bcn','empradonament','data_enquesta','nom_districte','llengua_enquesta','longitud','latitud','edat'.

Aquest conjunt de dades té la particularitat de ser una enquesta, cada ID és la resposta d'una persona. L'enquesta està dissenyada amb una barreja de preguntes condicionals, el que significa que algunes preguntes només són rellevants en funció de les respostes anteriors. Com a resultat, això provoca respostes no aplicables als enquestats, representades com a <Nan> al conjunt de dades. En aquest cas, no sembla pertinent eliminar les columnes que contenent poca informació, ni fer calculs de mitjana per emplenar el conjunt de dades.

S'han imputat els valors nuls utilitzant el mètode SimpleImputer de sklearn, que substitueix els valors nuls amb els més freqüents de cada columna.

Mapeig de Codis a Etiquetes: Es van substituir els codis numèrics per etiquetes significatives per facilitar la interpretació de les dades. Això inclou l'assignació d'etiquetes descriptives a les variables que contenien codis de resposta.

Divisió de Dades: El conjunt de dades es va dividir en conjunts d'entrenament i prova utilitzant train_test_split, amb un 80% de les dades destinades a l'entrenament i un 20% a la validació del model.

3. Resultats
Les variables seleccionades per entrenar els models venent del DF_final:
-Renda: Classificació del nivell econòmic dels participants.
-Nivell d'educació: Últim nivell d'educació assolit.
-Grup d'edat: Ranges d'edat dels enquestats.
-Codi de districte: Identificador del districte de residència.
-Situació laboral: Estat laboral dels participants.
-Internet a la llar: Accés a Internet a la llar (Sí/No). Aquesta variable es la Target. 

Els models de predicció utilitzats inclouen Random Forest i Regressió Logística. 

Els resultats obtinguts es poden resumir com:
Random Forest:
Precisió: 84.68%
Recall per a la classe amb accés a Internet: 88%
F1-score per a la classe sense accés a Internet: 29%

Regressió Logística:
Precisió: 65.42%
Recall per a la classe amb accés a Internet: 66%
F1-score per a la classe sense accés a Internet: 18%

Els resultats indiquen que, tot i l'eficàcia dels models, existeix una dificultat per predir correctament els usuaris sense accés a Internet.

4. Conclusions
Els models de Random Forest han demostrat un rendiment superior en la predicció de l'accés a Internet en comparació amb la regressió logística. Amb una precisió superior al 84%, el model de Random Forest és més eficaç per identificar usuaris amb connexió a Internet, indicant la seva robustesa en entorns amb dades complexes.

Tots els models van mostrar dificultats significatives per identificar usuaris sense accés a Internet. La baixa precisió i recall per a la classe d'usuari sense connexió (class 2) suggereix que els factors que contribueixen a la falta de connexió poden ser més complexos o estar menys representats en les dades, reflectint la necessitat de tècniques de mostreig més sofisticades o la incorporació de variables addicionals per millorar les prediccions.

Les variables relacionades amb la renda i la situació laboral han demostrat influir significativament en l'accés a Internet. Això indica que l'accés a la tecnologia i la connectivitat estan fortament relacionats amb factors econòmics, ressaltant la importància d'adreçar les desigualtats econòmiques per millorar l'accés a serveis digitals.

Una part considerable dels enquestats depenien del wifi de casa per accedir a Internet, com es reflecteix en les respostes sobre la manca de dades mòbils. Aquesta dependència pot indicar una falta de comprensió o accés a altres opcions de connectivitat, la qual cosa podria ser una àrea clau per a futures intervencions.

Els resultats subratllen la necessitat de realitzar investigacions més aprofundides per entendre millor les dinàmiques que envolten l'accés a Internet. Incorporar més variables sociodemogràfiques i de comportament dels usuaris podria proporcionar una visió més clara sobre les barreres que impedeixen l'accés a la tecnologia.

Finalment, aquests resultats poden servir de base per a la formulació de polítiques que busquin millorar la connectivitat en els districtes amb menys accés. Viure 'connectat' segueix sent un privilegi. 
