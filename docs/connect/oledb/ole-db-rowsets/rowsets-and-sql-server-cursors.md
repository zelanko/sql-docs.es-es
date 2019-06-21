---
title: Conjuntos de filas y cursores de SQL Server | Microsoft Docs
description: Conjuntos de filas y cursores de SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB rowsets, cursors
- OLE DB Driver for SQL Server, rowsets
- rowsets [OLE DB], cursors
- properties [OLE DB]
- cursors [OLE DB]
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 503e0f8fcc7cac9a3001ec00fb872642c1fcecd8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803790"
---
# <a name="rowsets-and-sql-server-cursors"></a>Conjuntos de filas y cursores de servidor de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devuelve conjuntos de resultados a los consumidores mediante dos métodos:  
  
-   Conjuntos de resultados predeterminados que:  
  
    -   Minimizan la sobrecarga.  
  
    -   Proporcionan un rendimiento máximo en la captura de datos.  
  
    -   Solo admiten la funcionalidad de cursor predeterminado de solo avance y solo lectura.  
  
    -   Devuelven filas de una en una al consumidor.  
  
    -   Solo admiten una instrucción activa a la vez en una conexión.  
  
         Una vez ejecutada una instrucción, no podrá ejecutarse ninguna otra instrucción en la conexión hasta que el consumidor haya recuperado todos los resultados o se haya cancelado la instrucción.  
  
    -   Admiten todas las instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
-   Cursores de servidor que:  
  
    -   Admiten toda la funcionalidad de cursor.  
  
    -   Pueden devolver bloques de filas al consumidor.  
  
    -   Admiten varias instrucciones activas en una única conexión.  
  
    -   Equilibran la funcionalidad de cursor con respecto al rendimiento.  
  
         La compatibilidad con la funcionalidad de cursor puede disminuir el rendimiento relativo a un conjunto de resultados predeterminado. Esto puede compensarse si el consumidor puede usar la funcionalidad de cursor para recuperar un conjunto de filas más pequeño.  
  
    -   No admiten cualquier instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] que devuelva más de un único conjunto de resultados.  
  
 Los consumidores pueden solicitar distintos comportamientos de cursor en un conjunto de filas estableciendo determinadas propiedades del conjunto de filas. Si el consumidor no establece ninguna de estas propiedades del conjunto de filas o establece todas ellas en sus valores predeterminados, el controlador OLE DB para SQL Server implementa el conjunto de filas mediante un conjunto de resultados predeterminado. Si cualquiera de estas propiedades se establece en un valor distinto del valor predeterminado, el controlador OLE DB para SQL Server implementa el conjunto de filas mediante un cursor de servidor.  
  
 Las siguientes propiedades del conjunto de filas dirigir el controlador OLE DB para SQL Server use [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cursores. Algunas propiedades pueden combinarse con otras sin ningún riesgo. Por ejemplo, un conjunto de filas que exhibe las propiedades DBPROP_IRowsetChange y DBPROP_IRowsetScroll será un conjunto de filas de marcador que exhibe un comportamiento de actualización inmediato. Otras propiedades se excluyen mutuamente. Por ejemplo, un conjunto de filas que exhibe DBPROP_OTHERINSERT no puede contener marcadores.  
  
|Id. de propiedad|Valor|Comportamiento del conjunto de filas|  
|-----------------|-----------|---------------------|  
|DBPROP_SERVERCURSOR|VARIANT_TRUE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas es secuencial y solamente admite desplazamiento y captura hacia delante. Se admite la posición de fila relativa. El texto de comando puede incluir una cláusula ORDER BY.|  
|DBPROP_CANSCROLLBACKWARDS o DBPROP_CANFETCHBACKWARDS|VARIANT_TRUE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas admite desplazamiento y captura en cualquier dirección. Se admite la posición de fila relativa. El texto de comando puede incluir una cláusula ORDER BY.|  
|DBPROP_BOOKMARKS o DBPROP_LITERALBOOKMARKS|VARIANT_TRUE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas es secuencial y solamente admite desplazamiento y captura hacia delante. Se admite la posición de fila relativa. El texto de comando puede incluir una cláusula ORDER BY.|  
|DBPROP_OWNUPDATEDELETE o DBPROP_OWNINSERT o DBPROP_OTHERUPDATEDELETE|VARIANT_TRUE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas admite desplazamiento y captura en cualquier dirección. Se admite la posición de fila relativa. El texto de comando puede incluir una cláusula ORDER BY.|  
|DBPROP_OTHERINSERT|VARIANT_TRUE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas admite desplazamiento y captura en cualquier dirección. Se admite la posición de fila relativa. El texto de comando puede incluir una cláusula ORDER BY si existe un índice en las columnas a las que se hace referencia.<br /><br /> DBPROP_OTHERINSERT no puede ser VARIANT_TRUE si el conjunto de filas contiene marcadores. Si se intenta crear un conjunto de filas con esta propiedad de visibilidad y marcadores, se genera un error.|  
|DBPROP_IRowsetLocate o DBPROP_IRowsetScroll|VARIANT_TRUE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas admite desplazamiento y captura en cualquier dirección. Se admiten marcadores y posicionamiento absoluto mediante de la interfaz **IRowsetLocate** en el conjunto de filas. El texto de comando puede incluir una cláusula ORDER BY.<br /><br /> DBPROP_IRowsetLocate y DBPROP_IRowsetScroll requieren marcadores en el conjunto de filas. Si se intenta crear un conjunto de filas con marcadores y DBPROP_OTHERINSERT se establece en VARIANT_TRUE, se genera un error.|  
|DBPROP_IRowsetChange o DBPROP_IRowsetUpdate|VARIANT_TRUE|Puede actualizar los datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas es secuencial y solamente admite desplazamiento y captura hacia delante. Se admite la posición de fila relativa. Todos los comandos que admiten cursores actualizables pueden admitir estas interfaces.|  
|DBPROP_IRowsetLocate o DBPROP_IRowsetScroll y DBPROP_IRowsetChange o DBPROP_IRowsetUpdate|VARIANT_TRUE|Puede actualizar los datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas admite desplazamiento y captura en cualquier dirección. Se admiten marcadores y posicionamiento absoluto mediante la interfaz **IRowsetLocate** en el conjunto de filas. El texto de comando puede incluir una cláusula ORDER BY.|  
|DBPROP_IMMOBILEROWS|VARIANT_FALSE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas solamente admite desplazamiento hacia delante. Se admite la posición de fila relativa. El texto de comando puede incluir una cláusula ORDER BY si existe un índice en las columnas a las que se hace referencia.<br /><br /> DBPROP_IMMOBILEROWS solo está disponible en conjuntos de filas que pueden mostrar las filas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] insertadas mediante comandos en otras sesiones o por parte de otros usuarios. Si se intenta abrir un conjunto de filas con la propiedad establecida en VARIANT_FALSE en cualquier conjunto de filas para el que DBPROP_OTHERINSERT no puede ser VARIANT_TRUE, se produce un error.|  
|DBPROP_REMOVEDELETED|VARIANT_TRUE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas solamente admite desplazamiento hacia delante. Se admite la posición de fila relativa. El texto de comando puede incluir una cláusula ORDER BY a menos que esté restringido por otra propiedad.|  
  
 Puede crear con facilidad un conjunto de filas de controlador OLE DB para SQL Server compatible con un cursor de servidor en una vista o tabla base de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con el método **IOpenRowset::OpenRowset**. Especifique la tabla o vista con su nombre, pasando los conjuntos de propiedades de conjunto de filas correspondientes en el parámetro *rgPropertySets*.  
  
 El texto de comando que crea un conjunto de filas se restringe cuando el consumidor requiere que un cursor de servidor admita el conjunto de filas. Concretamente, el texto de comando se restringe a una única instrucción SELECT que devuelve un único resultado de conjunto de filas, o bien, a un procedimiento almacenado que implementa una única instrucción SELECT que devuelve un único resultado de conjunto de filas.  
  
 En estas dos tablas se muestran las asignaciones de varias propiedades OLE DB y los modelos de cursor. También se muestran las propiedades de conjunto de filas que deberían establecerse para usar un determinado tipo de modelo de cursor.  
  
 Cada celda de la tabla contiene un valor de propiedad de conjunto de filas para cada modelo de cursor específico. El tipo de datos de todas las propiedades de conjunto de filas anteriormente indicadas en este tema es VT_BOOL y el valor predeterminado es VARIANT_FALSE. En la tabla se usan los símbolos siguientes.  
  
 F = valor predeterminado (VARIANT_FALSE)  
  
 T = VARIANT_TRUE  
  
 \- = VARIANT_TRUE o VARIANT_FALSE  
  
 Para usar un tipo de modelo de cursor determinado, busque la columna correspondiente al modelo de cursor y busque todas las propiedades de conjunto de filas que tengan el valor 'T' en la columna. Establezca estas propiedades de conjunto de filas en VARIANT_TRUE para usar ese modelo de cursor específico. Las propiedades del conjunto de filas que contienen '-' como valor pueden establecerse en VARIANT_TRUE o VARIANT_FALSE.  
  
|Propiedades de conjunto de filas o modelos de cursores|Valor predeterminado<br /><br /> resultado<br /><br /> conjunto<br /><br /> (SL)|Rápido<br /><br /> solo<br /><br /> avance<br /><br /> (SL)|Estático<br /><br /> (SL)|Keyset<br /><br /> conjuntos de claves<br /><br /> (SL)|  
|--------------------------------------|-------------------------------------------|--------------------------------------------|-----------------------|----------------------------------|  
|DBPROP_SERVERCURSOR|F|T|T|T|  
|DBPROP_DEFERRED|F|F|-|-|  
|DBPROP_IrowsetChange|F|F|F|F|  
|DBPROP_IrowsetLocate|F|F|-|-|  
|DBPROP_IrowsetScroll|F|F|-|-|  
|DBPROP_IrowsetUpdate|F|F|F|F|  
|DBPROP_BOOKMARKS|F|F|-|-|  
|DBPROP_CANFETCHBACKWARDS|F|F|-|-|  
|DBPROP_CANSRCOLLBACKWARDS|F|F|-|-|  
|DBPROP_CANHOLDROWS|F|F|-|-|  
|DBPROP_LITERALBOOKMARKS|F|F|-|-|  
|DBPROP_OTHERINSERT|F|T|F|F|  
|DBPROP_OTHERUPDATEDELETE|F|T|F|T|  
|DBPROP_OWNINSERT|F|T|F|T|  
|DBPROP_OWNUPDATEDELETE|F|T|F|T|  
|DBPROP_QUICKSTART|F|F|-|-|  
|DBPROP_REMOVEDELETED|F|F|F|-|  
|DBPROP_IrowsetResynch|F|F|F|-|  
|DBPROP_CHANGEINSERTEDROWS|F|F|F|F|  
|DBPROP_SERVERDATAONINSERT|F|F|F|-|  
|DBPROP_UNIQUEROWS|-|F|F|F|  
|DBPROP_IMMOBILEROWS|-|-|-|T|  
  
|Propiedades de conjunto de filas/modelos de cursores|Dinámico (SL)|Conjunto de claves (L/E)|Dinámico (L/E)|  
|--------------------------------------|--------------------|---------------------|----------------------|  
|DBPROP_SERVERCURSOR|T|T|T|  
|DBPROP_DEFERRED|-|-|-|  
|DBPROP_IrowsetChange|F|-|-|  
|DBPROP_IrowsetLocate|F|-|F|  
|DBPROP_IrowsetScroll|F|-|F|  
|DBPROP_IrowsetUpdate|F|-|-|  
|DBPROP_BOOKMARKS|F|-|F|  
|DBPROP_CANFETCHBACKWARDS|-|-|-|  
|DBPROP_CANSRCOLLBACKWARDS|-|-|-|  
|DBPROP_CANHOLDROWS|F|-|F|  
|DBPROP_LITERALBOOKMARKS|F|-|F|  
|DBPROP_OTHERINSERT|T|F|T|  
|DBPROP_OTHERUPDATEDELETE|T|T|T|  
|DBPROP_OWNINSERT|T|T|T|  
|DBPROP_OWNUPDATEDELETE|T|T|T|  
|DBPROP_QUICKSTART|-|-|-|  
|DBPROP_REMOVEDELETED|T|-|T|  
|DBPROP_IrowsetResynch|-|-|-|  
|DBPROP_CHANGEINSERTEDROWS|F|-|F|  
|DBPROP_SERVERDATAONINSERT|F|-|F|  
|DBPROP_UNIQUEROWS|F|F|F|  
|DBPROP_IMMOBILEROWS|F|T|F|  
  
 Para un conjunto determinado de propiedades de conjunto de filas, el modelo de cursor seleccionado se determina tal y como se indica a continuación.  
  
 De la colección especificada de propiedades de conjunto de filas, obtenga un subconjunto de propiedades de los que se indicaban en las tablas anteriores. Divida estas propiedades en dos subgrupos en función del valor de marca de cada propiedad del conjunto de filas: requerido (T, F) u opcional (-). Para cada modelo de cursor, comience por la primera tabla y desplácese de izquierda a derecha. Compare los valores de las propiedades de los dos subgrupos con los valores de las propiedades correspondientes de esa columna. Se seleccionará el modelo de cursor que no presente ninguna discrepancia con las propiedades necesarias y que tenga el menor número de discrepancias con las propiedades opcionales. Si hay más de un modelo de cursor, se elegirá el que esté situado más a la izquierda.  
  
## <a name="sql-server-cursor-block-size"></a>Tamaño del bloque de cursor de SQL Server  
 Cuando un cursor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite un conjunto de filas de controlador OLE DB para SQL Server, el número de elementos del parámetro de la matriz de identificadores de filas de los métodos **IRowset::GetNextRows** o **IRowsetLocate::GetRowsAt** define el tamaño del bloque de cursor. Las filas indicadas por los identificadores de la matriz son los miembros del bloque de cursor.  
  
 En el caso de los conjuntos de filas que admiten marcadores, los identificadores de fila recuperados mediante el método **IRowsetLocate::GetRowsByBookmark** definen los miembros del bloque de cursor.  
  
 Independientemente del método usado para rellenar el conjunto de filas y formar el bloque de cursor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el bloque de cursor estará activo hasta que se ejecute el siguiente método de captura de filas en el conjunto de filas.  
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de filas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
