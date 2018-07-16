---
title: Creación y administración de índices de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], about
ms.assetid: f8a98486-5438-44a8-b454-9e6ecbc74f83
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 441434839fa15b1f9345ddecf55eef3f7f248724
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37307465"
---
# <a name="create-and-manage-full-text-indexes"></a>Crear y administrar índices de texto completo
  El motor de búsqueda de texto completo utiliza la información de los índices de texto completo para compilar las consultas de texto completo que pueden buscar rápidamente en una tabla palabras o combinaciones de palabras determinadas. Un índice de texto completo almacena información sobre las palabras relevantes y su ubicación en una o varias columnas de la tabla de una base de datos. Un índice de texto completo es un tipo especial de índice funcional basado en token que el motor de texto completo genera y mantiene para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El proceso de creación de un índice de texto completo difiere de la creación de otros tipos de índice. En lugar de crear una estructura de árbol B basada en un valor almacenado en una fila determinada, el motor de texto completo genera una estructura de índice invertida, apilada y comprimida que se basa en tokens individuales del texto que se indiza.  El tamaño de un índice de texto completo solo está limitado por los recursos de memoria disponibles del equipo en el que se ejecuta la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], los índices de texto completo se integran con el motor de base de datos, en lugar de residir en el sistema de archivos como en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para una base de datos nueva, el catálogo de texto completo es ahora un objeto virtual que no pertenece a ningún grupo de archivos; es simplemente un concepto lógico que hace referencia al grupo de índices de texto completo. Debe tener en cuenta que, durante la actualización de una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , para cualquier catálogo de texto completo que contenga archivos de datos, se crea un nuevo grupo de archivos. Para obtener más información, vea [Actualizar la búsqueda de texto completo](upgrade-full-text-search.md).  
  
> [!NOTE]  
>  En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores, el motor de texto completo reside en el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , en lugar de en un servicio independiente. Al integrar el motor de texto completo en el motor de base de datos, se mejora la capacidad de administración de texto completo, la optimización de consultas mixtas y el rendimiento total.  
  
 Solo se permite un índice de texto completo por cada tabla. Para crear un índice de texto completo en una tabla, ésta debe tener una única columna que no contenga valores NULL. Puede crear un índice de texto completo en columnas de tipo `char`, `varchar`, `nchar`, `nvarchar`, `text`, `ntext`, `image`, `xml`, `varbinary`, y `varbinary(max)` se pueden indizar para búsqueda de texto completo. Crear un índice de texto completo en una columna cuyos datos es de tipo `varbinary`, `varbinary(max)`, `image`, o `xml` requiere que especifique una columna de tipo. Una *columna de tipo* es una columna de tabla en la que se almacena la extensión de archivo (.doc, .pdf, .xls, etc.) del documento en cada fila.  
  
 El proceso para crear y mantener un índice de texto completo se denomina *rellenado* (o *rastreo*). Hay tres tipos de rellenado del índice de texto completo: completo, basado en el seguimiento de cambios y basado en una marca de tiempo incremental. Para obtener más información, vea [Rellenar índices de texto completo](populate-full-text-indexes.md).  
  
##  <a name="tasks"></a> Tareas comunes  
 **Para crear un índice de texto completo**  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
 **Para modificar un índice de texto completo**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
 **Para quitar un índice de texto completo**  
  
-   [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-index-transact-sql)  
  
 [En este tema](#top)  
  
##  <a name="structure"></a> Estructura de índice de texto completo  
 Para comprender el funcionamiento del motor de texto completo, es necesario entender la estructura de un índice de texto completo. En este tema se utiliza el extracto siguiente de la tabla **Document** de [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] como tabla de ejemplo. Este extracto muestra solo dos columnas, **DocumentID** y **Title** , y tres filas de la tabla.  
  
 En este ejemplo se presupone que se ha creado un índice de texto completo en la columna **Title** .  
  
|DocumentID|Title|  
|----------------|-----------|  
|1|Crank Arm and Tire Maintenance|  
|2|Front Reflector Bracket and Reflector Assembly 3|  
|3|Front Reflector Bracket Installation|  
  
 Por ejemplo, en la tabla siguiente, en la que se muestra el fragmento 1, aparece el contenido del índice de texto completo creado en la columna **Title** de la tabla **Document** . Los índices de texto completo contienen más información que la que se presenta en esta tabla. La tabla es una representación lógica de un índice de texto completo y se proporciona solo como demostración. Las filas están almacenadas en un formato comprimido para optimizar el uso del disco.  
  
 Observe que los datos se han invertido en comparación con los documentos originales. La inversión se produce porque las palabras clave se asignan a los identificadores del documento. Por esta razón, se suele hacer referencia a un índice de texto completo como índice invertido.  
  
 Observe también que la palabra clave "y" se ha quitado del índice de texto completo. Se hace esto porque "y" es una palabra irrelevante y quitar las palabras irrelevantes de un índice de texto completo puede conllevar un ahorro sustancial en el espacio en disco y mejorar por tanto el rendimiento de las consultas. Para obtener más información sobre las palabras irrelevantes, vea [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
 **Fragmento 1**  
  
|Palabra clave|ColId|DocId|Repetición|  
|-------------|-----------|-----------|----------------|  
|Crank|1|1|1|  
|Arm|1|1|2|  
|Tire|1|1|4|  
|Mantenimiento|1|1|5|  
|Front|1|2|1|  
|Front|1|3|1|  
|Reflector|1|2|2|  
|Reflector|1|2|5|  
|Reflector|1|3|2|  
|Bracket|1|2|3|  
|Bracket|1|3|3|  
|Ensamblado|1|2|6|  
|3|1|2|7|  
|Installation|1|3|4|  
  
 La columna **Keyword** contiene una representación de un solo token extraído durante la indización. Los separadores de palabras determinan en qué consiste un token.  
  
 La columna **ColId** contiene un valor correspondiente a una determinada tabla y columna indexada de texto completo.  
  
 La `DocId` columna contiene valores de un entero de ocho bytes que se asigna a un determinado valor de clave de texto completo en una tabla indizada de texto completo. Esta asignación es necesaria cuando la clave de texto completo no es de un tipo de datos enteros. En tales casos, las asignaciones de texto completo los valores de clave y `DocId` se mantienen los valores en una tabla independiente denominada tabla de asignación de DocId. Para consultar estas asignaciones, use el procedimiento almacenado del sistema [sp_fulltext_keymappings](/sql/relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql) . Para satisfacer una condición de búsqueda, los valores de DocId de la tabla anterior tienen que combinarse con la tabla de asignaciones de DocId para recuperar las filas de la tabla base que se consulta. Si el valor de la clave de texto completo de la tabla base es de un tipo entero, el valor actúa directamente como DocId y no se necesita ninguna asignación. Por consiguiente, utilizar valores de clave de texto completo enteros puede ayudar a optimizar las consultas de texto completo.  
  
 La columna **Occurrence** contiene un valor entero. Para cada valor de DocId hay una lista de valores de repetición correspondientes a las posiciones relativas de una palabra clave determinada en DocId. Los valores de repetición son útiles para determinar las coincidencias de frases o de proximidad, por ejemplo, frases que tienen valores de repetición adyacentes. También son útiles para calcular las puntuaciones de importancia; por ejemplo, el número de repeticiones de una palabra clave en una columna DocId se puede utilizar para determinar la puntuación.  
  
 [En este tema](#top)  
  
##  <a name="fragments"></a> Fragmentos de índice de texto completo  
 El índice de texto completo lógico normalmente se divide entre varias tablas internas. Cada tabla interna se conoce como un fragmento del índice de texto completo. Algunos de estos fragmentos podrían contener datos más recientes que otros. Por ejemplo, si un usuario actualiza la fila siguiente cuyo DocId es 3 y la tabla se somete automáticamente a seguimiento de los cambios, se crea un fragmento nuevo.  
  
|DocumentID|Title|  
|----------------|-----------|  
|3|Rear Reflector|  
  
 En el ejemplo siguiente, que muestra el fragmento 2, el fragmento contiene los datos más recientes sobre el DocId 3 comparados con el fragmento 1. Por consiguiente, cuando el usuario consulta "Rear Reflector", se usan los datos del fragmento 2 correspondientes a DocId 3. Cada fragmento se marca con una marca de tiempo de creación que se puede consultar usando la vista de catálogo [sys.fulltext_index_fragments](/sql/relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql) .  
  
 **Fragmento 2**  
  
|Palabra clave|ColId|DocId|Occ|  
|-------------|-----------|-----------|---------|  
|Rear|1|3|1|  
|Reflector|1|3|2|  
  
 Como se puede ver en el fragmento 2, las consultas de texto completo tienen que consultar cada fragmento internamente y descartar las entradas más antiguas. Por consiguiente, demasiados fragmentos del índice de texto completo pueden conducir a una degradación sustancial del rendimiento de las consultas. Para reducir el número de fragmentos, reorganice el catálogo de texto completo mediante la opción REORGANIZE de la instrucción [ALTER FULLTEXT CATALOG](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] . Esta instrucción lleva a cabo una *combinación maestra*, que combina todos los fragmentos en un único fragmento mayor y quita todas las entradas obsoletas del índice de texto completo.  
  
 Después de la reorganización, el índice del ejemplo contendría las filas siguientes:  
  
|Palabra clave|ColId|DocId|Occ|  
|-------------|-----------|-----------|---------|  
|Crank|1|1|1|  
|Arm|1|1|2|  
|Tire|1|1|4|  
|Mantenimiento|1|1|5|  
|Front|1|2|1|  
|Rear|1|3|1|  
|Reflector|1|2|2|  
|Reflector|1|2|5|  
|Reflector|1|3|2|  
|Bracket|1|2|3|  
|Ensamblado|1|2|6|  
|3|1|2|7|  
  
 [En este tema](#top)  
  
  
