# Firmas ciegas para pagos no rastreables

David Chaum

Departamento de Ciencias de la Computación
Universidad de California
Santa Bárbara, CA

## INTRODUCCIÓN

La automatización de la forma en que pagamos por bienes y servicios ya está en marcha, como se puede observar por la variedad y el crecimiento de los servicios de banca electrónica disponibles para los consumidores.

La estructura final del nuevo sistema de pagos electrónicos puede tener un impacto sustancial en la privacidad personal, así como en la naturaleza y el alcance del uso delictivo de los pagos. 

Idealmente, un nuevo sistema de pagos debería abordar estos dos conjuntos de preocupaciones aparentemente conflictivos.

Por un lado, el conocimiento por parte de un tercero del beneficiario, el monto y la hora del pago de cada transacción realizada por un individuo puede revelar mucho sobre el paradero, las asociaciones y el estilo de vida del individuo. Por ejemplo, considere los pagos de cosas como transporte, hoteles, restaurantes, películas, teatro, conferencias, comida, productos farmacéuticos, alcohol, libros, publicaciones periódicas, cuotas, contribuciones religiosas y políticas.

Por otro lado, un sistema de pagos anónimo como los billetes de banco y las monedas adolece de falta de controles y seguridad. Por ejemplo, considere problemas como la falta de prueba de pago, el robo de medios de pago y los pagos en negro por sobornos, evasión de impuestos y mercados negros. 

Aquí se propone un tipo de criptografía fundamentalmente nuevo, que permite un sistema de pagos automatizado con las siguientes propiedades:

1. Imposibilidad de que terceros determinen el beneficiario, la hora o el monto de los pagos realizados por un individuo.

2. Capacidad de los individuos para proporcionar prueba de pago o para determinar la identidad del beneficiario en circunstancias excepcionales.

3. Capacidad para detener el uso de medios de pago denunciados como robados.

## Criptosistemas de firma ciega

El nuevo tipo de criptografía se introducirá primero en términos de una analogía y luego mediante la descripción de sus partes, su uso y las propiedades de seguridad resultantes. No se presenta ningún ejemplo de criptosistema real.

### Idea básica

El concepto de firma ciega puede ilustrarse con un ejemplo tomado del mundo familiar de los documentos en papel. El análogo en papel de una firma ciega se puede implementar con sobres forrados con papel carbón. 

Escribir una firma en el exterior de dicho sobre deja una copia carbón de la firma en un trozo de papel dentro del sobre. Considere el problema que enfrenta un administrador que desea celebrar una elección por votación secreta, pero los electores no pueden reunirse para depositar sus votos en un solo sombrero. 

Cada elector está muy preocupado por mantener su voto en secreto para el administrador, y cada elector también exige la capacidad de verificar que su voto sea contado. 

Se puede obtener una solución mediante el uso de los sobres especiales. Cada elector coloca una papeleta con su voto escrito en ella en un sobre forrado con carbón; coloca el sobre forrado con carbón en un sobre exterior dirigido al administrador, con su propia dirección de devolución; y envía los sobres anidados al administrador. 

Cuando el administrador recibe un sobre exterior con la dirección de devolución de un elector, el administrador retira el sobre interior forrado con carbón del sobre exterior; firma el exterior del sobre forrado con carbón; y envía el sobre forrado con carbón de vuelta, en un nuevo sobre exterior, a la dirección de devolución en el antiguo sobre exterior. 

Por lo tanto, solo los electores autorizados reciben papeletas firmadas. ¡Por supuesto, el administrador usa una firma especial que solo es válida para la elección! 

Cuando un elector recibe un sobre firmado, el elector retira el sobre exterior; verifica la firma en el sobre forrado con carbón; retira la papeleta firmada del sobre forrado con carbón; y envía la papeleta al administrador el día de la elección en un nuevo sobre exterior, sin una dirección de devolución. 

Cuando el administrador recibe las papeletas, se pueden exhibir públicamente. Cualquiera puede contar las papeletas exhibidas y verificar las firmas en ellas. 

Si los electores recuerdan algún aspecto identificativo de su papeleta, como el patrón de la fibra del papel, pueden verificar que su papeleta esté en exhibición. 

Pero dado que el administrador nunca vio realmente las papeletas al firmarlas (y asumiendo que cada firma es idéntica), el administrador no puede conocer ningún aspecto identificativo de la papeleta. 

Por lo tanto, el administrador no puede saber nada sobre la correspondencia entre los sobres que contienen las papeletas firmadas y las papeletas hechas públicas. 

Por lo tanto, el administrador no puede determinar cómo votó nadie.

### Funciones

Los sistemas de firma ciega podrían considerarse como la inclusión de las características de los verdaderos sistemas de firma digital de dos claves combinados de una manera especial con los sistemas de clave pública de estilo conmutativo. Las siguientes tres funciones componen el criptosistema de firma ciega:

1. Una función de firma s' conocida solo por el firmante, y la inversa públicamente conocida correspondiente s, tal que $s(s^{\prime}(x))=x$ y s no da ninguna pista sobre s'.

2. Una función de conmutación c y su inversa c', ambas conocidas solo por el proveedor, tal que $c^{\prime}(s^{\prime}(c(x)))=s^{\prime}(x)$ y c(x) y s' no dan ninguna pista sobre x.

3. Un predicado de verificación de redundancia r, que verifica si hay suficiente redundancia para hacer impráctica la búsqueda de firmas válidas.

### Protocolo

La forma en que se utilizan estas funciones recuerda a la forma en que se utilizaron los sobres forrados con papel carbón en el ejemplo descrito anteriormente:

1. El proveedor elige x al azar tal que $r(x)$, forma $c(x)$ y proporciona $c(x)$ al firmante.

2. El firmante firma $c(x)$ aplicando s' y devuelve el material firmado $s^{\prime}(c(x))$ al proveedor.

3. El proveedor elimina el material firmado mediante la aplicación de c', lo que da como resultado $c^{\prime}(s^{\prime}(c(x)))=s^{\prime}(x)$.

4. Cualquiera puede verificar que el material eliminado $s^{\prime}(x)$ fue formado por el firmante, aplicando la clave pública s del firmante y verificando que $r(s(s^{\prime}(x)))$.

### Propiedades

Las siguientes propiedades de seguridad se desean del sistema de firma ciega que comprende las funciones y protocolos anteriores:

1. Firma digital: cualquiera puede verificar que una firma eliminada $s^{\prime}(x)$ fue formada usando la clave privada s' del firmante.

2. Firma ciega: el firmante no sabe nada sobre la correspondencia entre los elementos del conjunto de material firmado eliminado $s^{\prime}(x_{i})$ y los elementos del conjunto de material firmado no eliminado $s^{\prime}(c(x_{i}))$.

3. Conservación de firmas: el proveedor puede crear como máximo una firma eliminada por cada cosa firmada por el firmante (es decir, incluso con $s^{*}(c(x_{1}))$...$s^{*}(c(x_{n}))$ y la elección de c, c' y $x_{i}$, es impráctico producir $s^{\prime}(y)$, tal que $r(y)$ e $y\ne x_{i}$).

Como es común en el trabajo criptográfico, se ignora la posibilidad de que el mismo número aleatorio pueda generarse de forma independiente.

## Sistema de pagos no rastreables

Un ejemplo de transacción de pago ilustrará cómo los sistemas de firma ciega introducidos anteriormente se pueden utilizar para crear un sistema de pagos no rastreable. El concepto crítico es que el banco firmará cualquier cosa con su clave privada, pero cualquier cosa así firmada vale una cantidad fija, digamos \$1. 

Los actores en el ejemplo a continuación son un banco, un pagador y un beneficiario. El pagador formará un solo billete, el banco lo firmará, el pagador lo eliminará, lo proporcionará al beneficiario y el banco lo liquidará. Lo siguiente rastrea los pasos detallados de una sola transacción de pago:

1. El pagador elige x al azar tal que $r(x)$, y forma el billete $c(x)$.

2. El pagador envía el billete $c(x)$ al banco.

3. El banco firma el billete, es decir, forma $s^{\prime}(c(x))$, y debita la cuenta del pagador.

4. El banco devuelve el billete firmado, $s^{\prime}(c(x))$, al pagador.

5. El pagador elimina el billete formando $c^{\prime}(s^{\prime}(c(x)))=s^{\prime}(x)$.

6. El pagador verifica el billete comprobando que $s(s^{\prime}(x))=x$ y se detiene si es falso.

7. El pagador realiza el pago algún tiempo después proporcionando el billete $s^{\prime}(x)$ al beneficiario.

8. El beneficiario verifica el billete formando $r(s(s^{\prime}(x)))$ y se detiene si es falso.

9. El beneficiario envía el billete $s^{\prime}(x)$ al banco.

10. El banco verifica el billete formando $r(s(s^{\prime}(x)))$ y se detiene si es falso.

11. El banco agrega el billete a una lista completa de billetes liquidados y se detiene si el billete ya está en la lista.

12. El banco acredita la cuenta del beneficiario.

13. El banco informa al beneficiario de la aceptación.

Observe que, según la propiedad de firma ciega anterior, cuando el banco recibe un billete para ser liquidado del beneficiario en el paso (9), el banco no sabe a qué pagador se emitió originalmente el billete en el paso (4). La firma digital y las propiedades relacionadas de conservación de firmas anteriores aseguran que la falsificación no sea posible.

### Auditabilidad

La extensión de la práctica actual sugiere que los pagadores reciben recibos digitales de los beneficiarios. Estos recibos incluirían la descripción habitual de los bienes o servicios comprados, y la fecha. Además, el recibo también podría incluir una copia del billete. En circunstancias excepcionales, como una auditoría, el billete permitiría al pagador, con la cooperación del banco (y las cámaras de compensación como se describe a continuación), verificar a qué cuenta se depositó realmente el billete. Un recibo que indique que un billete se depositó en una cuenta que no sea la cuenta realmente depositada sería evidencia de fraude. Un cliente insatisfecho de un mercado negro podría revelar un billete proporcionado al mercado negro, que luego podría rastrearse hasta la cuenta en la que finalmente terminó. Los billetes no liquidados denunciados como robados podrían incluirse en las listas de la cámara de compensación y, por lo tanto, evitarse que se liquiden; los billetes robados liquidados podrían rastrearse.

Los recibos emitidos por el beneficiario al pagador proporcionan control sobre todas las salidas y, por lo tanto, sobre todos los flujos de fondos. Un contribuyente podría proporcionar recibos verificables para cualquier gasto necesario para una auditoría fiscal. Se podría exigir a las personas que conserven los recibos de las entradas sustanciales, pero los recibos de las entradas mantenidas por las organizaciones pueden ser indeseables, si pudieran revelar a los clientes de la organización.

### Elaboraciones

El sistema simple del ejemplo anterior podría extenderse de varias maneras para proporcionar economía de mecanismo, desagregación de servicios y descentralización. Por ejemplo, se obtendrían eficiencias obvias del uso de billetes de múltiples denominaciones. Las funciones bancarias y de cámara de compensación podrían separarse. Podría haber múltiples bancos; múltiples cámaras de compensación podrían servir a diferentes bancos o superponerse. Los cambios periódicos de la(s) clave(s) utilizada(s) para firmar billetes podrían aumentar la seguridad, aumentar la auditabilidad y reducir la incertidumbre sobre el tamaño de la oferta monetaria.

## Resumen e Implicaciones

Se ha introducido un nuevo tipo de criptografía, las firmas ciegas. Permite la realización de sistemas de pagos no rastreables que ofrecen una mejor auditabilidad y control en comparación con los sistemas actuales, al tiempo que ofrecen una mayor privacidad personal.