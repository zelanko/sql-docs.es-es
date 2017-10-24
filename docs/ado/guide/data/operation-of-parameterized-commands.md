---
title: "Funcionamiento de los comandos con parámetros | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
ms.assetid: 4fae0d54-83b6-4ead-99cc-bcf532daa121
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 65f8a1caba2f709e4583613ced4d6aa03b2d6bf1
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="operation-of-parameterized-commands"></a>Funcionamiento de los comandos con parámetros
Si está trabajando con un elemento secundario grande **Recordset**, especialmente si se compara con el tamaño del elemento primario **conjunto de registros**, pero la necesidad de tener acceso a solo unos pocos capítulos secundarios, le resultará más eficaz usar un comando con parámetros.  
  
 A *comando sin parámetros* recupera tanto el principal y secundario completos **conjuntos de registros**, anexa una columna de capítulo al elemento primario y, a continuación, asigna una referencia al capítulo secundario relacionado para cada fila primaria .  
  
 A *comando con parámetros* recupera el elemento primario todo **Recordset**, pero recupera únicamente el capítulo **Recordset** cuando se accede a la columna de capítulo. Esta diferencia en la estrategia de recuperación puede producir ventajas significativas de rendimiento.  
  
 Por ejemplo, puede especificar lo siguiente:  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 Las tablas primarias y secundarias tienen un nombre de columna en común, cust_id*.* El *comando secundario* tiene un "?" marcador de posición, al que hace referencia la cláusula RELATE (es decir, "... PARÁMETRO 0").  
  
> [!NOTE]
>  La cláusula del parámetro pertenece únicamente a la sintaxis del comando shape. No está asociado a cualquier ADO [parámetro](../../../ado/reference/ado-api/parameter-object.md) objeto o la [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección.  
  
 Cuando se ejecuta el comando parametrizado shape, ocurre lo siguiente:  
  
1.  El *comando primario* se ejecuta y devuelve un elemento primario **Recordset** de la tabla Customers.  
  
2.  Una columna de capítulo se anexa al elemento primario **conjunto de registros**.  
  
3.  Cuando se tiene acceso a la columna de capítulo de una fila principal, el *comando secundario* se ejecuta con el valor del cliente como el valor del parámetro.  
  
4.  Todas las filas en el conjunto de filas del proveedor de datos creado en el paso 3 se usan para rellenar el elemento secundario **conjunto de registros**. En este ejemplo, que es todas las filas de la tabla Orders en el que cust_id es igual al valor de cliente. De forma predeterminada, el elemento secundario **Recordset**s se almacenarán en caché en el cliente de hasta que todas las referencias al elemento primario **Recordset** se liberan. Para cambiar este comportamiento, establezca la **Recordset** [propiedad dinámica](../../../ado/reference/ado-api/ado-dynamic-property-index.md) **Cache Child Rows** a **False**.  
  
5.  Una referencia a las filas secundarias recuperadas (es decir, el capítulo del elemento secundario **Recordset**) se coloca en la columna de capítulo de la fila actual del elemento primario **conjunto de registros**.  
  
6.  Pasos del 3 al 5 se repiten cuando se tiene acceso a la columna de capítulo de otra fila.  
  
 El **Cache Child Rows** propiedades dinámicas se establece en **True** de forma predeterminada. El comportamiento de almacenamiento en caché varía en función de los valores de parámetro de la consulta. En una consulta con un solo parámetro, el elemento secundario **Recordset** para un parámetro dado valor se almacenará en caché entre las solicitudes de un elemento secundario con ese valor. El código siguiente se muestra cómo hacerlo:  
  
```  
SCmd = "SHAPE {select * from customer} " & _  
         "APPEND({select * from orders where cust_id = ?} " & _  
         "RELATE cust_id TO PARAMETER 0) AS chpCustOrder"  
Rst1.Open sCmd, Cnn1  
Set RstChild = Rst1("chpCustOrder").Value  
Rst1.MoveNext      ' Next cust_id passed to Param 0, & new rs fetched   
                   ' into RstChild.  
Rst1.MovePrevious  ' RstChild now holds cached rs, saving round trip.  
```  
  
 En una consulta con dos o más parámetros, se utiliza un elemento secundario en caché solo si todos los valores de parámetro coincide con los valores almacenados en caché.  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>Comandos con parámetros y las relaciones secundarias de complejas entre principal  
 Además de utilizar comandos parametrizados para mejorar el rendimiento de una jerarquía de tipos de combinación, los comandos con parámetros se pueden utilizar para admitir las relaciones de elementos primarios y secundarios más complejas. Por ejemplo, considere la posibilidad de una base de datos Little League con dos tablas: una que consta de los equipos (team_id, nombre_equipo) y otra de encuentros (date, home_team, visiting_team).  
  
 Utilizando una jerarquía sin parámetros, no hay ninguna manera para relacionar las tablas de equipos y encuentros de tal manera que el elemento secundario **Recordset** para cada equipo contenga su programación completa. Puede crear capítulos que contienen la programación principal o la programación de viaje, pero no ambos. Esto es porque la cláusula RELATE limita a relaciones primarias y secundarias de la forma (pc1 = cc1) AND (pc2 = pc2). Por lo tanto, si el comando incluye "RELATE team_id TO home_team, team_id TO visiting_team", se obtendría sólo juegos donde estaba reproduciendo un equipo propio. Lo que desea es "(team_id=home_team) o (team_id = visiting_team)", pero el proveedor de formas no admite la cláusula OR.  
  
 Para obtener el resultado deseado, puede usar un comando con parámetros. Por ejemplo:  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 Este ejemplo aprovecha la mayor flexibilidad de la cláusula WHERE de SQL para obtener el resultado que necesita.  
  
> [!NOTE]
>  Cuando utiliza las cláusulas WHERE, parámetros no pueden usar los tipos de datos SQL para text, ntext e image o producirá un error que contiene la descripción siguiente: `Invalid operator for data type`.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)

