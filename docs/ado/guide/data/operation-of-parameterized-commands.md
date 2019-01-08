---
title: Funcionamiento de los comandos con parámetros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
ms.assetid: 4fae0d54-83b6-4ead-99cc-bcf532daa121
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: faa4d4887079064ac6ccbe9536ac6c36fe8b9f79
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516994"
---
# <a name="operation-of-parameterized-commands"></a>Funcionamiento de los comandos con parámetros
Si está trabajando con un elemento secundario grande **Recordset**, especialmente en comparación con el tamaño del elemento primario **Recordset**, pero la necesidad de tener acceso a solo unos pocos capítulos secundarios, le resultará más eficaz usar un comando con parámetros.  
  
 Un *comando sin parámetros* recupera los todo primario y secundario **conjuntos de registros**, anexa una columna de capítulo con el elemento primario y, a continuación, asigna una referencia al capítulo secundario relacionado para cada fila principal .  
  
 Un *comando con parámetros* recupera el elemento primario todo **Recordset**, pero sólo recupera el **Recordset** cuando se tiene acceso a la columna de capítulo. Esta diferencia en la estrategia de recuperación puede aportar beneficios de rendimiento significativas.  
  
 Por ejemplo, puede especificar lo siguiente:  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 Las tablas primaria y secundaria tienen un nombre de columna en común, cust_id *.* El *comando secundario* tiene un "?" marcador de posición, al que hace referencia la cláusula RELATE (es decir, "... PARÁMETRO 0").  
  
> [!NOTE]
>  La cláusula del parámetro pertenece exclusivamente a la sintaxis del comando shape. No está asociado con cualquier ADO [parámetro](../../../ado/reference/ado-api/parameter-object.md) objeto o la [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección.  
  
 Cuando se ejecuta el comando parametrizado shape, ocurre lo siguiente:  
  
1.  El *comando primario* se ejecuta y devuelve un elemento primario **Recordset** desde la tabla Customers.  
  
2.  Una columna de capítulo se anexa al elemento primario **Recordset**.  
  
3.  Cuando se tiene acceso a la columna de capítulo de una fila principal, el *comando secundario* se ejecuta utilizando el valor del cliente como el valor del parámetro.  
  
4.  Todas las filas del conjunto de filas del proveedor de datos creado en el paso 3 se usan para rellenar el elemento secundario **Recordset**. En este ejemplo, que es todas las filas de la tabla Orders en la que cust_id es igual al valor de cliente. De forma predeterminada, el elemento secundario **Recordset**s se almacenarán en el cliente hasta que todas las referencias al elemento primario **Recordset** se liberan. Para cambiar este comportamiento, establezca el **Recordset** [propiedad dinámica](../../../ado/reference/ado-api/ado-dynamic-property-index.md) **filas secundarias de caché** a **False**.  
  
5.  Una referencia a las filas secundarias recuperadas (es decir, el capítulo del elemento secundario **Recordset**) se coloca en la columna de capítulo de la fila actual del elemento primario **Recordset**.  
  
6.  Los pasos 3 a 5 se repiten cuando se tiene acceso a la columna de capítulo de otra fila.  
  
 El **filas secundarias de caché** se establece la propiedad dinámica **True** de forma predeterminada. El comportamiento de almacenamiento en caché varía en función de los valores de parámetro de la consulta. En una consulta con un solo parámetro, el elemento secundario **Recordset** para un determinado parámetro de valor se almacenará en caché entre solicitudes para un elemento secundario con ese valor. El siguiente código muestra esto:  
  
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
  
 En una consulta con dos o más parámetros, se usa un elemento secundario en caché solo si todos los valores de parámetro coincide con los valores almacenados en caché.  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>Los comandos con parámetros y las relaciones secundarias de complejos primario  
 Además de utilizar comandos parametrizados para mejorar el rendimiento de una jerarquía de tipos de combinación, los comandos con parámetros pueden utilizarse para admitir relaciones más complejas de elementos primarios y secundarios. Por ejemplo, considere la posibilidad de una base de datos Little League con dos tablas: uno que consta de los equipos (team_id, nombre_equipo) y otra de juegos (date, home_team, visiting_team).  
  
 Con una jerarquía sin parámetros, hay ninguna manera se relacionan las tablas de los equipos y los juegos de manera que el elemento secundario **Recordset** para cada equipo que contiene su programación completa. Puede crear los capítulos que contienen la programación de inicio o la programación de la carretera, pero no ambos. Esto es porque la cláusula RELATE le limita a las relaciones de elementos primarios y secundarios del formulario (pc1 = cc1) AND (pc2 = pc2). Por lo tanto, si el comando incluye "RELATE team_id TO home_team, team_id TO visiting_team", se obtendría sólo juegos donde estaba desempeñando un equipo propio. Lo que quiere es "(team_id=home_team) o (team_id = visiting_team)", pero el proveedor de formas no admite la cláusula OR.  
  
 Para obtener el resultado deseado, puede usar un comando con parámetros. Por ejemplo:  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 En este ejemplo aprovecha la mayor flexibilidad de la cláusula WHERE de SQL para obtener el resultado que necesita.  
  
> [!NOTE]
>  Al utilizar cláusulas WHERE, parámetros no pueden usar los tipos de datos SQL para text, ntext e image o producirá un error que contiene la siguiente descripción: `Invalid operator for data type`.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)
