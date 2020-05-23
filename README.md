# Teoria de los Juegos Evolutivos. Machos fieles y atorrantes, hembras faciles y esquivas.

## Simulacion online

https://grandes-chicos-comparten-pelea.herokuapp.com/


## Resumen

Como dice Daniel Dennett, en La Evolución de la Libertad, la teoría evolutiva de los juegos nos brinda conceptos que son imprescindibles para entender como pudo haber evolucionado la moral en los animales. Tal vez pueda ayudar a poner en cuestión la ideología de género, pensar si en realidad existe algo como el patriarcado y porque las políticas de genero muestran ser tan ineficaces.  La teoría evolutiva de los juegos fue creada por John Maynard Smith y se hizo muy conocida con el libro El Gen Egoísta de Richard Dawkins.

En este trabajo implemento varios de los juegos  de la teoría evolutiva de los juegos. Siguiendo el libro Evolución y Teoría de los Juegos de John Maynard Smith, empiezo simulando una población donde todos los individuos son iguales y existen  solo 2 estrategias para resolver conflictos, compartir y pelear. Luego agregaremos una diferencia arbitraria entre los individuos, por ejemplo, individuos que son residente e individuos que son intrusos. Luego usaremos esa diferencia arbitraria entre los individuos para definir estrategias condicionales. Una estrategia condicional es una estrategia del tipo ‘si tu oponente es intruso pelea en caso contrario comparte’. Después veremos que sucede cuando convertimos la diferencia arbitraria en diferencias que influyen en el resultado de una pelea, por ejemplo, hay individuos que se diferencian en tamaño y fuerza, y estrategias condicionales del tipo peleo solo si mi oponente es más grande y fuerte. Por últimos consideremos una población formada por individuos distintos, por ejemplo machos y hembras, pero donde cada tipo de individuo tiene diferente conjunto de estrategias, por ejemplo, los machos no pueden usar las estrategias fieles y atorrantes, mientras que las hembras solo pueden usar las estrategias fáciles y esquivas. 

En la implementación nos encontramos con una serie de dificultades, por ejemplo si los individuos más aptos tienen  2 o más descendientes el crecimiento es exponencial  y en pocas generaciones nos quedamos sin recursos.  Analizamos cuales son las capacidades cognitivas mínimas que tienen que tener los organismos simulados,  cómo influye la distancia mínima que tienen que estar dos individuos para que surja un conflicto, juego de halcones y palomas, el dilema del prisionero repetido,  algunas condiciones para que pueda surgir la cooperación en individuos que no están relacionados genéticamente, guerra de desgaste, carrera armamentística, juegos asimétricos y simétricos.  

Si la mitad de la población comparte y la otra mitad pelea ¿qué sucederá si se deja evolucionar la población? Si la población está formada inicialmente por n individuos chicos que pelean solo si su oponente es más grande y por k individuos grandes que pelean solo si su oponente es más chico ¿porque individuos estará formada la población luego de varias generaciones de evolución? Nos preguntamos qué sucede con distintas poblaciones a las que se las deja evolucionar. Realizo varias simulaciones y analizo los resultados obtenidos.  


## Introducción
 
Al igual que nosotros,  los animales también necesitan determinados recursos para vivir y reproducirse. Por ejemplo, un animal no puede vivir sin agua ni comida. Para nosotros todas las cosas tienen un precio. El precio depende de la oferta y la demanda. El kilogramo de naranja vale más caro en verano que en invierno porque es menor la oferta que la demanda.  

Una pregunta interesante es como poder asignar valor a los recursos que los animales necesitan. Podríamos asignar a un recurso un valor equivalente al aumento en aptitud darwiniana. Maynard Smith dice, supongamos que en promedio  un animal que vive en un ambiente favorable tiene 5 crías mientras que si el mismo animal viviera en un ambiente desfavorable tendría en promedio 3 crías, entonces podríamos asignar  al ambiente favorable un valor de 2 pagos, la diferencia entre 5 crías del ambiente favorable y las 3 crías del ambiente desfavorable. 

Esta forma de definir el valor que un recurso tiene para un animal no es perfecta. En nuestra especie las personas pobres y sin estudios tienen muchos más hijos que las personas ricas. Esto no significa que los pobres tengan una mayor aptitud darwiniana que los ricos, ni que una villa miseria es un ambiente favorable y un barrio privado es un ambiente desfavorable. Se puede decir que nuestra especie es un caso particular, atípico, ninguna otra especie pudo construir un estado benefactor. 

Otro argumento por el cual definir el valor del recurso como la diferencia entre cantidades de crías no es perfecto. Un animal puede tener muchas más crías que otro y no necesariamente ser más apto. Por ejemplo un animal puede tener 20 crías y otro solo 3 crías.  Puede ser que todas las crías del que tuvo 20 se mueran al mes porque los padres no puedan alimentar a todas las crías o no puedan decidir a qué cría dejar morir, mientras que el animal que tuvo solo 3 crías se convirtió en abuelo de varios nietos. Para que sea correcto hay que completar la frase de la siguiente manera, un animal en un ambiente favorable tiene más crías que llegan a la edad adulta, y a su vez estas crías tienen crías. 

En los modelos que presentamos vamos a suponer que los recursos son divisibles y que a los animales les conviene tener la mitad del recurso antes que quedarse sin nada, o que buscar un recurso de menor valor. En la vida real no solamente hay recursos que no se pueden dividir, sino que también hay situaciones en las cuales a ningún animal le conviene compartir un recurso. Por ejemplo, supongamos que el recurso es un ambiente favorable y al animal le da 10 pagos, mientras que el animal que se queda con el ambiente desfavorable obtiene 8 pagos. En esta situación a nadie le convenida compartir y tener 5 puntos, ya que si se fuera al ambiente desfavorable obtendría 8 puntos que es mayor que los 5 puntos obtenidos al compartir el ambiente favorable.

Las plantas y otros animales son recursos que sirven como alimentos. Las plantas producen sabores desagradables, las gacelas corren más rápido que los leones, la vista de los pájaros mejora para ver a insectos que se camuflan cada vez mejor. En este modelo no vamos a considerar la  carrera armamentística entre presa y depredador. Vamos a suponer que en cada posición del tablero, el ambiente donde se desarrolla la simulación, hay recursos que los animales necesitan.

Cuando dos o más individuos quieren el mismo recurso no sube el precio, como sucede en una subasta. En el modelo el valor del recurso esta fijo, como vimos al principio, está en relación con la diferencia entre la cantidad de crías del individuo que obtuvo el recurso y el que se quedó sin el recurso. Cuando dos individuos quieren el mismo recurso se produce un conflicto que se puede resolver de diferentes formas. El recurso se puede compartir o los animales pueden pelear por el recurso. Solo si los dos animales esta dispuestos a compartir el recurso se comparte. Si solo uno está dispuesto a compartir y el otro quiere pelear, entonces el que estaba dispuesto a pelear se queda con el recurso. Si los dos animales esta dispuestos a pelear, entonces el ganador se queda con el recurso mientras que el perdedor sufre una penalidad. Se puede pensar como el tiempo de reposo para recuperarse, porque perder un combate no afecta el desempeño del individuo en futuros combates. ¿Por qué los animales no son siempre agresivos? ¿Habrá situaciones en las que a los animales no le convenga pelear? ¿En qué situaciones conviene compartir? Estas son preguntas que se intentara responder con un modelo simple.

En la vida real, cuando dos animales deciden pelear, ambos pagan un costo, no solo el perdedor.  Por ejemplo, si el costo está dado por el tiempo que duro la pelea, tanto el ganador como el perdedor perdieron el mismo tiempo en la pelea.  En los juegos de guerra de desgaste el ganador obtiene el recurso, pero ambos pagan el mismo costo, el costo que estaba dispuesto a pagar el que perdió. Siguiendo el libro de Maynard Smith, Evolución y Teoría de los Juegos, yo implemente modelos donde solo el perdedor paga el costo y comparo la simulación con los resultados analíticos deducidos en el libro.

No es fácil saber qué valor tiene un recurso para un animal, ni asignar el costo que tiene una pelea perdida. Además, como dijimos al principio, el valor del recurso está dado por diferencia entre cantidades de crías, mientras que el costo esta dado en tiempo perdido o lesiones recibidas. Hay un problema con los tipos, faltan factores de conversión, que conviertan diferencia de crías, tiempo perdido y lesiones recibidas en puntos. Tampoco es fácil encontrar una función que convierta puntos en cantidad de descendientes. Las predicciones en biología ni tienen la misma precisión que en física o astronomía. Por ejemplo. Tenemos 2 especies muy emparentadas genéticamente, una vive en un ambiente hostil mientras que la otra vive en un ambiente donde sobre el alimento, el alimento va a tener un mayor valor para la especie que vive en un ambiente hostil y por lo tanto se va a esperar que sea más agresiva, que las peleas entre los miembros sean más duras, mientras que la otra especie no sería raro que compartieran el alimento. En una especie donde los machos viven en arenes, con muchas hembras, el valor del recurso, muchas hembras, tiene un valor muy alto y se esperaría peleas muy agresivas entre machos. 

¿Cuáles son las capacidades cognitivas que el modelo supone que los organismos tienen? ¿Para poder usar el modelo será necesario que los organismos puedan reconocerse individualmente, que tengan memoria, que puedan recordar cómo les fue en peleas que hayan tendido? Por ejemplo. Modelos para el altruismo suponen que los organismos se puedan reconocer individualmente, que puedan reconocer a individuos altruistas y ayudar a los que son altruistas, como dice Dawkins, si un individuo con el gen para el altruismo se tira al rio para salvar a 10 individuos con genes de altruismo, no importa si el individuo que se tiro al rio muera, si se salvaron 10 individuos el gen para el altruismo tendrá una ventaja evolutiva. De igual manera modelos para la cooperación suponen que los organismos están jugando el dilema del prisionero repetido, que son mayoría los que están cooperando y entonces la mejor estrategia es empezar cooperando y después hacer lo que hizo el otro jugador en el pasado. 
 
En el modelo que implemento no hay reconocimiento individual, los organismos no saben si se encontraron anteriormente con el mismo individuo, no tienen memoria y el resultado de las luchas pasadas influye sobre futuras peleas. Aunque el modelo supone que no hay reconocimiento individual, ni memoria del pasado, en ciertas circunstancias se puede aplicar a organismos superiores. Por ejemplo, en una pelea de tránsito, con alguien desconocido, hay muy baja probabilidad de volver a encontrarse a la misma persona en el futuro. El costo de una pelea puede ser tiempo en cárcel o desaprobación social mientras que el valor del recurso un lugar donde estacionar el vehículo. 

¿A qué distancia tienen que estar dos animales para que tengan un conflicto? No es necesario que estén en la misma celda del tablero, pueden estar en casilleros adyacentes o pueden estar más lejos, puede estar uno en una punta del tablero y el otro en la otra punta. La vecindad es un parámetro de la simulación. Si ponemos que todos los agentes sean vecinos de todos encontramos que los resultados  obtenidos en la simulación son muy similares a los deducidos analíticamente.  Hay modelos donde la vecindad afecta muchísimo más los resultados que se obtienen. Anteriormente hablamos de modelos para el  altruismo y  la cooperación. Dijimos que solo cuando la mayoría de la población está cooperando, cooperar es la mejor estrategia. Si la mayoría de la población no esta cooperando entonces desertar, la estrategia no cooperativa, es la mejor estrategia. Ahora bien, cooperar tiene la propiedad de que cuando se encuentra con copias de sí mismo les va muy bien,  les va mucho mejor que cuando copias que desertan  se encuentran entre si. Por lo tanto si para considerarse vecinos tienen que estar muy cerca y los descendiente nacen cerca de sus padres, la población de los que cooperan crecen mucho más rápido que los que desertan y en pocos pasos cooperar se hacen mayoría, condición para que cooperar sea la mejor estrategia en toda la población. 

La explosión demográfica es un problema en nuestra especie y el la simulación. Si la mitad de la población con mayor puntaje, los más aptos,  tiene 2, o más descendientes, el crecimiento es exponencial. Si tan solo el 10% de la población con mayor puntaje tiene 2 o más descendientes y el resto de la población solo un descendiente el crecimiento sigue siendo exponencial. En cambio, si los individuos más aptos tienen un solo descendiente y el resto no tiene ningún descendiente, en cada generación la población se va reduciendo. En la naturaleza, son raros los casos de poblaciones de animales que crecieron hasta agotar todos los recursos. Biólogos como Lorenz pensaron en selección de grupo, por el bien de la especie los animales reducen la tasa de natalidad cuando se van quedando sin recursos. La explicación de Dawkins es otra: Tener un hijo tiene un costo y solo se obtiene una ganancia cuando el hijo llega sano y salvo a la edad adulta y da nietos. Podemos suponer que en la población hay individuos que, independientemente de su aptitud,  están genéticamente programados para tener una camada de 20 crías y hay individuos que están programados para tener 3 crías. Si el individuo que tuvo 20 crías  no pudo alimentarlos, murieron todos sus hijos y, entonces, dejo menos descendiente que alguien que solo tuvo 3 crías, que pudo alimentar a las 3 crías y que todos llegaron sanos y salvos a la edad adulta dejando nietos.  Esto da como resultado una regulación dinámica de la cantidad óptima de hijos.  La solución al problema de la sobrepoblación implementada en la simulación fue la siguiente: Si la cantidad de individuos que hay población es menor que N,  el 20% de los individuos más aptos tienen 2 descendiente y el resto un solo descendiente. Si la cantidad de individuos es mayor, elimino aleatoriamente individuos de la población, cual deriva genética,  quedándome con una población de la mitad del tamaño original.

Los modelos simples pueden volverse gradualmente más complejos. Esperamos que medida que se vuelven más complejos se asemejen más al mundo real. 

Primero supondremos una población donde todos los individuos son exactamente iguales, son todos clones. Luego, un gen mutado da como resultado una diferencia en la forma de resolución de conflictos, unos van a resolver los conflictos peleando mientras que otros van a resolver los conflictos compartiendo. La única diferencia que va a producir la mutación es la forma de resolver conflictos, en el resto siguen siendo exactamente iguales, no hay ninguna diferencia física entre los individuos.

Después, otra mutación, o las condiciones de existencia, produce una diferencia arbitraria. Por ejemplo, unos son residentes y los otros intrusos, unos tienen barba verde y los otros son lampiños. Esta diferencia no influye en la fuerza física, ni en la capacidad de lucha. En una pelea tienen la misma probabilidad de ganar. Usando esta diferencia arbitraria entre los individuos podemos introducir estrategias condicionales, por ejemplo, pelear solo si mi oponente es un intruso o, pelear solo si mi oponente tiene barba verde y compartir en caso contrario. 
Luego, otra mutación produce diferencia entre los individuos pero ahora la diferencia no es arbitraria, la diferencia influyen en la fuerza o en la capacidad de lucha. Veremos qué pasa cuando los individuos se diferencian en atributo que influye en la fuerza o en  la capacidad de lucha. Nos preguntaremos si puede haber situaciones en las que sea una buena idea usar estrategia condicional paradójica, esto es, pelear con oponentes que son de mayor tamaño y cuando el oponente es de menor tamaño huir.

Por ultimo realizaremos simulaciones en una población formada por individuos de distinto tipo, por ejemplo, machos y hembras. Cada tipo de individuo tiene distintas estrategias, por ejemplo, los machos tienen las estrategas fiel y atorrante y las hembras fáciles y esquivas.

Nota: Maynard Smith dice que cuando dos palomas se enfrentan el recurso se comparte de manera equitativa entre los dos participantes. Mientras que Dawkins dice  cuando una paloma se enfrenta a otra paloma nadie saldrá lesionado; se limitarán a asumir una postura, una frente a la otra, durante un largo tiempo hasta que una de ellas se canse o decida no molestarse más y, por lo tanto, ceda. Las palomas comparten o se limitan a asumir una postura hasta que una de ellas se cansa? Cuando yo intente explicar el juego note que la gente  suponía que los halcones eran más grandes físicamente que las palomas. Si bien el juego que implemento se conoce como el juego de  Halcones y Palomas yo voy a usar las palabras individuos que usan la estrategia pelear e individuos que comparten. Más allá de las palabras, el juego tiene la misma tabla de pagos que es lo único que importa.

## BIBLIOGRAFIA

* **Richard Dawkins, El Gen Egoista.**
* **Richard Dawkins, El Relojero Ciego.**
* **Richard Dawkins, Escalando el Monte Improbable.**
* **Richard Dawkins, El Rio del Eden.**
* **Daniel Dennett, La Peligrosa Idea de Darwin.**
* **Daniel Dennett, La Evolucion de La Libertad.**
* **Steven Pinker, La Tabla Rasa.**
* **Steven Pinker, El Instinto del Lenguaje.**
* **John Maynard Smith, Evolucion y Teoria de los Juegos.**
* **John Maynard Smith, Animal Signals.**






 
