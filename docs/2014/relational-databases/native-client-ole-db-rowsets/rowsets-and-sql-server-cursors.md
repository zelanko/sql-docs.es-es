---
title: Conjuntos de filas y cursores de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB rowsets, cursors
- SQL Server Native Client OLE DB provider, rowsets
- rowsets [OLE DB], cursors
- properties [OLE DB]
- cursors [OLE DB]
ms.assetid: 26a11e26-2a3a-451e-8f78-fba51e330ecb
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7c1768beb903e214260c2b6a37486bfc2583c0c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416365"
---
# <a name="rowsets-and-sql-server-cursors"></a>Conjuntos de filas y cursores de servidor de SQL Server
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve conjuntos de resultados a los consumidores mediante dos métodos:  
  
-   Conjuntos de resultados predeterminados que:  
  
    -   Minimizan la sobrecarga.  
  
    -   Proporcionan un rendimiento máximo en la captura de datos.  
  
    -   Solo admiten la funcionalidad de cursor predeterminado de solo avance y solo lectura.  
  
    -   Devuelven filas de una en una al consumidor.  
  
    -   Solo admiten una instrucción activa a la vez en una conexión.  
  
         Una vez ejecutada una instrucción, no podrá ejecutarse ninguna otra instrucción en la conexión hasta que el consumidor haya recuperado todos los resultados o se haya cancelado la instrucción.  
  
    -   Admiten todas las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Cursores de servidor que:  
  
    -   Admiten toda la funcionalidad de cursor.  
  
    -   Pueden devolver bloques de filas al consumidor.  
  
    -   Admiten varias instrucciones activas en una única conexión.  
  
    -   Equilibran la funcionalidad de cursor con respecto al rendimiento.  
  
         La compatibilidad con la funcionalidad de cursor puede disminuir el rendimiento relativo a un conjunto de resultados predeterminado. Esto puede compensarse si el consumidor puede usar la funcionalidad de cursor para recuperar un conjunto de filas más pequeño.  
  
    -   No admiten cualquier instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que devuelva más de un único conjunto de resultados.  
  
 Los consumidores pueden solicitar distintos comportamientos de cursor en un conjunto de filas estableciendo determinadas propiedades del conjunto de filas. Si el consumidor no establece ninguna de estas propiedades de conjunto de filas o establece todas en sus valores predeterminados, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client implementa el conjunto de filas con un conjunto de resultados predeterminado. Si cualquiera de estas propiedades se establece en un valor distinto del predeterminado, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client implementa el conjunto de filas mediante un cursor de servidor.  
  
 Las siguientes propiedades de conjunto de filas indican al proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client que use cursores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Algunas propiedades pueden combinarse con otras sin ningún riesgo. Por ejemplo, un conjunto de filas que exhibe las propiedades DBPROP_IRowsetChange y DBPROP_IRowsetScroll será un conjunto de filas de marcador que exhibe un comportamiento de actualización inmediato. Otras propiedades se excluyen mutuamente. Por ejemplo, un conjunto de filas que exhibe DBPROP_OTHERINSERT no puede contener marcadores.  
  
|Id. de propiedad|Valor|Comportamiento del conjunto de filas|  
|-----------------|-----------|---------------------|  
|DBPROP_SERVERCURSOR|VARIANT_TRUE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas es secuencial y solamente admite desplazamiento y captura hacia delante. Se admite la posición de fila relativa. El texto de comando puede incluir una cláusula ORDER BY.|  
|DBPROP_CANSCROLLBACKWARDS o DBPROP_CANFETCHBACKWARDS|VARIANT_TRUE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas admite desplazamiento y captura en cualquier dirección. Se admite la posición de fila relativa. El texto de comando puede incluir una cláusula ORDER BY.|  
|DBPROP_BOOKMARKS o DBPROP_LITERALBOOKMARKS|VARIANT_TRUE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas es secuencial y solamente admite desplazamiento y captura hacia delante. Se admite la posición de fila relativa. El texto de comando puede incluir una cláusula ORDER BY.|  
|DBPROP_OWNUPDATEDELETE o DBPROP_OWNINSERT o DBPROP_OTHERUPDATEDELETE|VARIANT_TRUE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas admite desplazamiento y captura en cualquier dirección. Se admite la posición de fila relativa. El texto de comando puede incluir una cláusula ORDER BY.|  
|DBPROP_OTHERINSERT|VARIANT_TRUE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas admite desplazamiento y captura en cualquier dirección. Se admite la posición de fila relativa. El texto de comando puede incluir una cláusula ORDER BY si existe un índice en las columnas a las que se hace referencia.<br /><br /> DBPROP_OTHERINSERT no puede ser VARIANT_TRUE si el conjunto de filas contiene marcadores. Si se intenta crear un conjunto de filas con esta propiedad de visibilidad y marcadores, se genera un error.|  
|DBPROP_IRowsetLocate o DBPROP_IRowsetScroll|VARIANT_TRUE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas admite desplazamiento y captura en cualquier dirección. Marcadores y posiciones absolutas a través de la **IRowsetLocate** interfaz son compatibles con el conjunto de filas. El texto de comando puede incluir una cláusula ORDER BY.<br /><br /> DBPROP_IRowsetLocate y DBPROP_IRowsetScroll requieren marcadores en el conjunto de filas. Si se intenta crear un conjunto de filas con marcadores y DBPROP_OTHERINSERT se establece en VARIANT_TRUE, se genera un error.|  
|DBPROP_IRowsetChange o DBPROP_IRowsetUpdate|VARIANT_TRUE|Puede actualizar los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas es secuencial y solamente admite desplazamiento y captura hacia delante. Se admite la posición de fila relativa. Todos los comandos que admiten cursores actualizables pueden admitir estas interfaces.|  
|DBPROP_IRowsetLocate o DBPROP_IRowsetScroll y DBPROP_IRowsetChange o DBPROP_IRowsetUpdate|VARIANT_TRUE|Puede actualizar los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas admite desplazamiento y captura en cualquier dirección. Los marcadores y posiciones absolutas a través **IRowsetLocate** se admiten en el conjunto de filas. El texto de comando puede incluir una cláusula ORDER BY.|  
|DBPROP_IMMOBILEROWS|VARIANT_FALSE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas solamente admite desplazamiento hacia delante. Se admite la posición de fila relativa. El texto de comando puede incluir una cláusula ORDER BY si existe un índice en las columnas a las que se hace referencia.<br /><br /> DBPROP_IMMOBILEROWS solo está disponible en conjuntos de filas que pueden mostrar las filas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] insertadas mediante comandos en otras sesiones o por parte de otros usuarios. Si se intenta abrir un conjunto de filas con la propiedad establecida en VARIANT_FALSE en cualquier conjunto de filas para el que DBPROP_OTHERINSERT no puede ser VARIANT_TRUE, se produce un error.|  
|DBPROP_REMOVEDELETED|VARIANT_TRUE|No puede actualizar los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través del conjunto de filas. El conjunto de filas solamente admite desplazamiento hacia delante. Se admite la posición de fila relativa. El texto de comando puede incluir una cláusula ORDER BY a menos que esté restringido por otra propiedad.|  
  
 Un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] filas del proveedor OLE DB de Native Client admitidos un cursor de servidor pueden crearse fácilmente en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla base o vista utilizando la **IOpenRowset:: OpenRowset** método. Especifique la tabla o vista por su nombre, pasando el conjunto de filas requiere conjuntos de propiedades en el *rgPropertySets* parámetro.  
  
 El texto de comando que crea un conjunto de filas se restringe cuando el consumidor requiere que un cursor de servidor admita el conjunto de filas. Concretamente, el texto de comando se restringe a una única instrucción SELECT que devuelve un único resultado de conjunto de filas, o bien, a un procedimiento almacenado que implementa una única instrucción SELECT que devuelve un único resultado de conjunto de filas.  
  
 En estas dos tablas se muestran las asignaciones de varias propiedades OLE DB y los modelos de cursor. También se muestran las propiedades de conjunto de filas que deberían establecerse para usar un determinado tipo de modelo de cursor.  
  
 Cada celda de la tabla contiene un valor de propiedad de conjunto de filas para cada modelo de cursor específico. El tipo de datos de todas las propiedades de conjunto de filas anteriormente indicadas en este tema es VT_BOOL y el valor predeterminado es VARIANT_FALSE. En la tabla se usan los símbolos siguientes.  
  
 F = valor predeterminado (VARIANT_FALSE)  
  
 T = VARIANT_TRUE  
  
 \- = VARIANT_TRUE o VARIANT_FALSE  
  
 Para usar un tipo de modelo de cursor determinado, busque la columna correspondiente al modelo de cursor y busque todas las propiedades de conjunto de filas que tengan el valor 'T' en la columna. Establezca estas propiedades de conjunto de filas en VARIANT_TRUE para usar ese modelo de cursor específico. Las propiedades del conjunto de filas que contienen '-' como valor pueden establecerse en VARIANT_TRUE o VARIANT_FALSE.  
  
|Modelos de cursor o propiedades de conjunto de filas|Valor predeterminado<br /><br /> result<br /><br /> conjunto<br /><br /> (SL)|Rápido<br /><br /> solo <br /><br /> avance<br /><br /> (SL)|Estático<br /><br /> (SL)|Keyset<br /><br /> conjuntos de claves<br /><br /> (SL)|  
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
 Cuando un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursor admite un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] filas del proveedor OLE DB de Native Client, el número de elementos de la fila controlar el parámetro de matriz de la **IRowset:: GetNextRows** o **IRowsetLocate:: GetRowsAt**  métodos define el tamaño de bloque de cursor. Las filas indicadas por los identificadores de la matriz son los miembros del bloque de cursor.  
  
 Los conjuntos de filas que admiten marcadores, los identificadores de fila recuperan mediante el uso de la **IRowsetLocate:: Getrowsbybookmark** método definen los miembros del bloque de cursor.  
  
 Independientemente del método usado para rellenar el conjunto de filas y formar el bloque de cursor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el bloque de cursor estará activo hasta que se ejecute el siguiente método de captura de filas en el conjunto de filas.  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas](rowsets.md)  
  
  
