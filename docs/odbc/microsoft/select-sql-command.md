---
title: Seleccione - comando SQL | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- select [ODBC]
ms.assetid: 2149c3ca-3a71-446d-8d53-3d056e2f301a
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f300cfb998c0d35aa6c853774fc029445da1015
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="select---sql-command"></a>Seleccione - comando SQL
Recupera datos de una o varias tablas.  
  
 El controlador ODBC de Visual FoxPro admite la sintaxis del lenguaje Visual FoxPro nativo para este comando. Para obtener información específica del controlador, consulte **controlador comentarios**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SELECT [ALL | DISTINCT]  
   [Alias.] Select_Item [AS Column_Name]  
   [, [Alias.] Select_Item [AS Column_Name] ...]   
FROM [DatabaseName!]Table [Local_Alias]  
   [, [DatabaseName!]Table [Local_Alias] ...]   
[WHERE JoinCondition [AND JoinCondition  
…]  
   [AND | OR FilterCondition [AND | OR FilterCondition ...]]]  
[GROUP BY GroupColumn [, GroupColumn ...]]  
[HAVING FilterCondition]  
[UNION [ALL] SELECTCommand]  
[ORDER BY Order_Item [ASC | DESC] [, Order_Item [ASC | DESC] ...]]  
```  
  
## <a name="arguments"></a>Argumentos  
  
> [!NOTE]  
>  A *subconsulta*, mencionadas en los siguientes argumentos, es una instrucción SELECT en una instrucción SELECT y debe ir entre paréntesis. Puede tener hasta dos subconsultas en el mismo nivel (no están anidados) en la cláusula WHERE. (Vea esa sección de los argumentos). Subconsultas pueden contener varias condiciones de combinación.  
  
 [Todos los &#124; DISTINCT]   [*Alias*.] *Select_Item* [AS *Column_Name*] [, [*Alias*.] *Select_Item* [AS *Column_Name*]...]  
 La cláusula SELECT especifica los campos, constantes y expresiones que se muestran en los resultados de la consulta.  
  
 De forma predeterminada, todos muestra todas las filas en los resultados de la consulta.  
  
 DISTINCT excluye duplicados de todas las filas de resultados de la consulta.  
  
> [!NOTE]  
>  Puede usar DISTINCT sólo una vez por cada cláusula SELECT.  
  
 *Alias*. califica los nombres de elemento coincidente. Cada elemento que se especifique con *Select_Item* genera una columna de resultados de la consulta. Si dos o más elementos tienen el mismo nombre, incluya el alias de tabla y un punto antes del nombre de elemento para impedir que las columnas que se duplican.  
  
 *Select_Item* especifica un elemento que se incluirá en los resultados de la consulta. Un elemento puede ser uno de los siguientes:  
  
-   El nombre de un campo de una tabla en la cláusula FROM.  
  
-   Constante que especifica que el mismo valor constante va a aparecer en cada fila de resultados de la consulta.  
  
-   Una expresión que puede ser el nombre de una función definida por el usuario.  
  
 **Funciones definidas por el usuario con SELECT**  
  
 Aunque el uso de funciones definidas por el usuario en la cláusula SELECT tiene ventajas obvias, también debe tener en cuenta las siguientes restricciones:  
  
-   La velocidad de las operaciones realizadas con SELECT puede estar limitada por la velocidad con que se ejecutan dichas funciones definidas por el usuario. Las manipulaciones de gran volumen que impliquen a funciones definidas por el usuario podrían realizarse mejor mediante el uso de API y funciones definidas por el usuario escritas en C o lenguaje de ensamblado.  
  
-   Es la única manera confiable para pasar valores a funciones definidas por el usuario invocadas desde SELECT por la lista de argumentos que se pasan a la función cuando se invoca.  
  
-   Aunque experimentar y detectar una manipulación supuestamente prohibida que funciona correctamente en una versión determinada de FoxPro, no hay ninguna garantía que continuarán funcionando en versiones posteriores.  
  
 Además de estas restricciones, las funciones definidas por el usuario son aceptables en la cláusula SELECT. Sin embargo, recuerde que usar SELECT puede ralentizar el rendimiento.  
  
 Las siguientes funciones de campo están disponibles para su uso con un elemento select que es un campo o una expresión que contenga un campo:  
  
-   AVG (*Select_Item*): calcula el promedio de una columna de datos numéricos.  
  
-   RECUENTO (*Select_Item*): cuenta el número de selección de elementos en una columna. Count cuenta el número de filas de resultado de la consulta.  
  
-   MIN (*Select_Item*): determina el valor más pequeño de *Select_Item* en una columna.  
  
-   MAX (*Select_Item*): determina el valor más grande de *Select_Item* en una columna.  
  
-   SUM (*Select_Item*): suma de una columna de datos numéricos.  
  
 No se pueden anidar funciones de campo.  
  
 AS *Column_Name*  
 Especifica el encabezado de una columna de resultado de la consulta. Esto es útil cuando *Select_Item* es una expresión o contiene un campo de función y desea dar un nombre descriptivo a la columna. *Column_name* puede ser una expresión, pero no puede contener caracteres (por ejemplo, espacios en blanco) que no están permitidos en los nombres de campo de tabla.  
  
 DESDE [*DatabaseName*!] *Tabla* [*Local_Alias*] [, [*DatabaseName*!] *Tabla* [*Local_Alias*]...]  
 Enumera las tablas que contienen los datos que recupera la consulta. Si no hay ninguna tabla está abierta, Visual FoxPro muestra la **abrir** cuadro de diálogo para que pueda especificar la ubicación del archivo. Después de que se ha abierto, la tabla permanece abierta una vez completada la consulta.  
  
 *DatabaseName*! Especifica el nombre de una base de datos distinto del especificado con el origen de datos. Debe incluir el nombre de la base de datos que contiene la tabla si no se especifica la base de datos con el origen de datos. Incluir el delimitador de signo de exclamación (!) después del nombre de la base de datos y antes del nombre de tabla.  
  
 *Local_Alias* especifica un nombre temporal para la tabla mencionada en *tabla*. Si se especifica un alias local, debe utilizar el alias local en lugar del nombre de tabla a lo largo de la instrucción SELECT. El alias local no influye en el entorno de Visual FoxPro.  
  
 DONDE *JoinCondition* [AND *JoinCondition* ...]    [AND &#124; o *FilterCondition* [AND &#124; o *FilterCondition* ...]]  
 Indica a Visual FoxPro para incluir solamente algunos registros en los resultados de la consulta. Si es necesario para recuperar datos de varias tablas.  
  
 *JoinCondition* especifica los campos que se vinculan las tablas en la cláusula FROM. Si incluye más de una tabla en una consulta, debe especificar una condición de combinación para cada tabla después del primero.  
  
> [!IMPORTANT]  
>  Tenga en cuenta la siguiente información al crear condiciones de combinación:  
  
-   Si incluye dos tablas en una consulta y no especifica una condición de combinación, todos los registros de la primera tabla pertenece a todos los registros de la segunda tabla siempre y cuando se cumplen las condiciones de filtro. Este tipo de consulta puede producir resultados extensa.  
  
-   Tenga cuidado al combinar tablas con los campos vacíos porque Visual FoxPro coincide con los campos vacíos. Por ejemplo, si se une en la tabla CUSTOMER. Código postal y factura. Código postal y si el cliente contiene 100 códigos postales vacíos y factura 400 códigos postales vacíos, el resultado de la consulta contiene 40 000 registros adicionales resultantes de los campos vacíos. Use la **() vacío** función para eliminar los registros vacíos de resultado de la consulta.  
  
-   Debe utilizar el operador AND para conectar varias condiciones de combinación. Cada condición de combinación tiene el formato siguiente:  
  
     *Nombredecampo1 comparación Nombredecampo2*  
  
     *Nombredecampo1* es el nombre de un campo de una tabla, *Nombredecampo2* es el nombre de un campo de otra tabla, y *comparación* es uno de los operadores descritos en la tabla siguiente.  
  
|Operador|Comparación|  
|--------------|----------------|  
|=|Igual|  
|==|Exactamente igual|  
|LIKE|SQL COMO|  
|<>, !=, #|No igual|  
|>|Más de|  
|>=|Mayor o igual a|  
|<|Menor que|  
|<=|Menor o igual que|  
  
 Cuando se usa el operador = con cadenas, actúa de forma diferente, según la configuración de SET ANSI. Cuando SET ANSI se establece en OFF, Visual FoxPro trata las comparaciones de cadenas de una manera familiar a los usuarios de Xbase. Cuando SET ANSI se establece en ON, Visual FoxPro sigue las normas de ANSI para comparaciones de cadenas. Vea [SET ANSI](../../odbc/microsoft/set-ansi-command.md) y [SET EXACT](../../odbc/microsoft/set-exact-command.md) para obtener más información acerca de cómo Visual FoxPro realiza comparaciones de cadenas.  
  
 *FilterCondition* especifica los criterios que deben cumplir los registros para que se incluyan en los resultados de la consulta. Se pueden incluir muchas condiciones de filtro en una consulta como desee, conectan con la operación AND o OR (operador). También puede usar el operador NOT para invertir el valor de una expresión lógica, o puede usar **() vacío** para comprobar si un campo vacío. *FilterCondition* puede tener cualquiera de los formularios en los ejemplos siguientes:  
  
 **Ejemplo 1** *Nombredecampo1 comparación Nombredecampo2*  
  
 `customer.cust_id = orders.cust_id`  
  
 **Ejemplo 2** *expresión de comparación de nombre de campo*  
  
 `payments.amount >= 1000`  
  
 **Ejemplo 3** *FieldName comparación* todos (*subconsulta*)  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 Cuando la condición de filtro incluye todas, el campo debe cumplir la condición de comparación para todos los valores generados por la subconsulta antes de su registro se incluye en los resultados de la consulta.  
  
 **Ejemplo 4** *FieldName comparación* ANY &#124; SOME (*subconsulta*)  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 Cuando la condición de filtro incluye alguna, el campo debe cumplir la condición de comparación para al menos uno de los valores generados por la subconsulta.  
  
 En el ejemplo siguiente se comprueba para ver si los valores en el campo que están dentro de un intervalo especificado de valores:  
  
 **Ejemplo 5** *FieldName* [NOT] entre *Start_Range* AND *End_Range*  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 En el ejemplo siguiente se comprueba para ver si al menos una fila cumple los criterios de la subconsulta. Cuando la condición de filtro incluye EXISTS, la condición de filtro se evalúa como True (. T.) a menos que la subconsulta se evalúa como el conjunto vacío.  
  
 **Ejemplo 6** [NOT] existe (*subconsulta*)  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **Ejemplo 7** *FieldName* [NOT] IN *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 Cuando la condición de filtro incluye en, el campo debe contener uno de los valores antes de su registro se incluye en los resultados de la consulta.  
  
 **Ejemplo 8** *FieldName* [NOT] IN (*subconsulta*)  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 Aquí el campo debe contener uno de los valores devueltos por la subconsulta antes de su registro se incluye en los resultados de la consulta.  
  
 **Ejemplo 9** *FieldName* [NOT] como *cExpression*  
  
 `customer.country NOT LIKE "USA"`  
  
 Busca en esta condición de filtro para cada campo que coincida con *cExpression*. Puede usar el signo de porcentaje (%) y caracteres de comodín de subrayado (_) como parte de *cExpression*. El carácter de subrayado representa un único carácter desconocido en la cadena.  
  
 GROUP BY *GroupColumn* [, *GroupColumn* ...]  
 Grupos de filas en la consulta basada en valores de una o varias columnas. *GroupColumn* puede ser uno de los siguientes:  
  
-   El nombre de un campo de tabla normal.  
  
-   Un campo que incluye una función de campo SQL.  
  
-   Una expresión numérica que indica la ubicación de la columna en la tabla de resultados. (El número de columna de la izquierda es 1).  
  
 TENER *FilterCondition*  
 Especifica una condición de filtro que grupos deben cumplir para que se incluyan en los resultados de la consulta. HAVING debe utilizarse con GROUP BY y pueden incluir muchas condiciones de filtro como desee, conectados mediante la operación AND o OR (operador). También puede utilizar no para anular el valor de una expresión lógica.  
  
 *FilterCondition* no puede contener una subconsulta.  
  
 Una cláusula HAVING sin una cláusula GROUP BY se comporta como una cláusula WHERE. Puede utilizar alias locales y las funciones de campo en la cláusula HAVING. Utilice una cláusula WHERE para acelerar el rendimiento si la cláusula HAVING no contiene ninguna función de campo.  
  
 [UNION [ALL] *SELECTCommand*]  
 Combina el resultado final de una selección con los resultados finales de, seleccione otro. De forma predeterminada, unión comprueba los resultados combinados y elimina las filas duplicadas. Utilice paréntesis para combinar varias cláusulas de unión.  
  
 Todos los impide que unión lo que elimina las filas duplicadas de los resultados combinados.  
  
 Cláusulas de unión siguen estas reglas:  
  
-   No se puede utilizar UNION para combinar las subconsultas.  
  
-   Ambos comandos SELECT deben tener el mismo número de columnas en los resultados de la consulta.  
  
-   Cada columna en los resultados de consulta de una selección debe tener el mismo tipo de datos y el ancho que la columna correspondiente en el otro, seleccione.  
  
-   Solo la instrucción SELECT final puede tener una cláusula ORDER BY, que debe hacer referencia a columnas de salida por número. Si se incluye una cláusula ORDER BY, afecta a los resultados completo.  
  
 También puede utilizar la cláusula UNION para simular una combinación externa.  
  
 Cuando se une dos tablas en una consulta, solo los registros con valores coincidentes en los campos de combinación se incluyen en la salida. Si un registro de la tabla primaria no tiene un registro correspondiente en la tabla secundaria, no se incluye el registro de la tabla primaria en la salida. Una combinación externa permite incluir todos los registros en la tabla primaria en la salida, junto con los registros coincidentes en la tabla secundaria. Para crear una combinación externa en Visual FoxPro, debe utilizar un comando SELECT anidado, como en el ejemplo siguiente:  
  
```  
SELECT customer.company, orders.order_id, orders.emp_id ;  
FROM customer, orders ;  
WHERE customer.cust_id = orders.cust_id ;  
UNION ;  
SELECT customer.company, 0, 0 ;  
FROM customer ;  
WHERE customer.cust_id NOT IN ;  
(SELECT orders.cust_id FROM orders)  
```  
  
> [!NOTE]  
>  Asegúrese de que incluye el espacio que precede inmediatamente a cada punto y coma. En caso contrario, recibirá un error.  
  
 La sección del comando antes de la cláusula UNION selecciona los registros de ambas tablas que tengan valores coincidentes. Las compañías de cliente que no tienen las facturas asociadas no se incluyen. La sección del comando después de la cláusula UNION selecciona los registros en la tabla de clientes que no tienen registros coincidentes en la tabla orders.  
  
 Con respecto a la segunda sección del comando, tenga en cuenta lo siguiente:  
  
-   La instrucción SELECT entre paréntesis se procesa en primer lugar. Esta instrucción crea una selección de todos los números de cliente en la tabla orders.  
  
-   La cláusula WHERE busca todos los números de cliente en la tabla de clientes que no están en la tabla orders. Dado que la primera sección del comando proporciona todas las compañías que tenían un número de cliente en la tabla orders, todas las compañías que en la tabla customer ahora se incluyen en los resultados de la consulta.  
  
-   Dado que las estructuras de las tablas incluidas en una unión deben ser idénticas, hay dos marcadores de posición en la segunda instrucción SELECT para representar *orders.order_id* y *orders.emp_id* desde la primera instrucción SELECT instrucción.  
  
    > [!NOTE]  
    >  Los marcadores de posición deben ser del mismo tipo que los campos que representan. Si el campo es un tipo de fecha, el marcador de posición debe ser {/ /}. Si el campo es un campo de caracteres, el marcador de posición debe ser una cadena vacía ("").  
  
 Se ORDENA por *Order_Item* [ASC &#124; DESC] [, *Order_Item* [ASC &#124; DESC]...]  
 Ordena los resultados de la consulta en función de los datos en una o varias columnas. Cada *Order_Item* debe corresponder a una columna de resultados de la consulta y puede tener uno de los siguientes:  
  
-   Un campo en una tabla FROM que también es un elemento seleccionado en la cláusula SELECT principal (no en una subconsulta).  
  
-   Una expresión numérica que indica la ubicación de la columna en la tabla de resultados. (La columna izquierda es el número 1.)  
  
 ASC especifica un orden ascendente de resultados de la consulta, según el elemento o elementos y es el valor predeterminado de ORDER BY.  
  
 DESC especifica un orden descendente de resultados de la consulta.  
  
 Resultados de la consulta aparecen sin ordenar si no especifica un pedido con ORDER BY.  
  
## <a name="remarks"></a>Comentarios  
 SELECT es un comando SQL que está integrado en Visual FoxPro como cualquier otro comando de Visual FoxPro. Cuando usas Seleccione esta opción para suponer una consulta, Visual FoxPro interpreta la consulta y recupera los datos especificados de las tablas. Puede crear una consulta SELECT desde dentro de la ventana de símbolo del sistema o un programa de Visual FoxPro (como ocurre con cualquier otro comando de Visual FoxPro).  
  
> [!NOTE]  
>  Seleccione no respeta la condición de filtro actual especificada con establecer filtro.  
  
## <a name="driver-remarks"></a>Comentarios del controlador  
 Cuando la aplicación envía la instrucción SELECT de SQL de ODBC para el origen de datos, el controlador ODBC de Visual FoxPro convierte el comando en el comando de Visual FoxPro Seleccione sin traducción a menos que el comando contiene una secuencia de escape ODBC. Elementos que se incluyen en una secuencia de escape ODBC se convierten en sintaxis de Visual FoxPro. Para obtener más información sobre el uso de ODBC secuencias de escape, vea [funciones de fecha y hora](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md) y en el *referencia del programador de Microsoft ODBC*, consulte [secuencias de Escape de ODBC](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) .  
  
## <a name="see-also"></a>Vea también  
 [CREAR TABLA - SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL](../../odbc/microsoft/insert-sql-command.md)   
 [CONJUNTO ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [CONJUNTO EXACTO](../../odbc/microsoft/set-exact-command.md)
