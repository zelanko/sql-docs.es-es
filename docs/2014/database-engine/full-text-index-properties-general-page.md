---
title: Propiedades del índice de texto completo (página general) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.fulltextindexproperties.general.f1
ms.assetid: f4dff61c-8c2f-4ff9-abe4-70a34421448f
author: rothja
ms.author: jroth
ms.openlocfilehash: b2ca5eef7905806f551b960d2ec912d1d5a8a09f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932986"
---
# <a name="full-text-index-properties-general-page"></a>Propiedades del índice de texto completo (página General)
  **Para ver o cambiar las propiedades modificables de un índice de texto completo**  
  
-   [Administrar índices de texto completo](../relational-databases/indexes/indexes.md)  
  
## <a name="ui-element-list"></a>Lista de elementos de la interfaz de usuario  
 **Catálogo de texto completo**  
 Muestra el nombre del catálogo de texto completo al que se asocia el índice de texto completo.  
  
 **Base de datos**  
 Muestra el nombre de la base de datos en la que el índice de texto completo reside.  
  
 **Tabla**  
 Muestra el nombre de la tabla en la que se define el índice de texto completo.  
  
 **Clave de índice de texto completo**  
 Muestra el nombre de la clave de índice de texto completo, que es un índice único en una columna única de la tabla.  
  
 **Estado de llenado de texto completo de tabla**  
 Muestra el estado de rellenado de una tabla con índice de texto completo.  
  
 Los valores posibles son los siguientes:  
  
 0 = Inactiva  
  
 1 = Rellenado completo en curso.  
  
 2 = Rellenado incremental en curso.  
  
 3 = Propagación de cambios de seguimiento en curso.  
  
 4 = Actualización de índices en segundo plano en curso, como el seguimiento de cambios automáticos.  
  
 5 = Indización de texto completo acelerada o pausada.  
  
 **Índice de texto completo activo**  
 Indica si la tabla tiene un índice de texto completo activo.  
  
 1 = True  
  
 0 = False  
  
 **Grupo de archivos de índice de texto completo**  
 Grupo de archivos al que pertenece el índice de texto completo.  
  
 **Lista de palabras irrelevantes de índice de texto completo**  
 Lista de palabras irrelevantes asociada al índice de texto completo. Una lista de [palabras irrelevantes](../relational-databases/search/full-text-search.md)es sinónimo de una lista de palabras sin trascendencia. La lista de palabras irrelevantes asociada a un índice de texto completo, si existe, se aplica a las consultas de texto completo en ese índice. Puede quitar la lista de palabras irrelevantes del índice seleccionando **\<OFF>** en la lista, o puede seleccionar una lista de palabras irrelevantes diferente; **\<SYSTEM>** indica la lista de palabras irrelevantes del sistema.  
  
 **Para crear una lista de palabras irrelevantes**  
  
-   [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../relational-databases/search/full-text-search.md)  
  
 **Lista de propiedades de búsqueda**  
 La lista de propiedades de búsqueda asociada actualmente al índice de texto completo, si la hay. Una lista de propiedades de búsqueda especifica un conjunto de propiedades de documento que se incluyen en el índice de texto completo asociado cuando este se rellena. Para obtener más información, vea [Buscar propiedades de documento con listas de propiedades de búsqueda](../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
 **\<Off>** indica que actualmente no hay ninguna lista de propiedades de búsqueda asociada al índice. Puede quitar la lista de propiedades de búsqueda actual del índice seleccionando **\<Off>** en la lista o puede seleccionar otra lista de propiedades de búsqueda en la lista. Esta lista solo contiene las listas de propiedades de búsqueda de la base de datos actual.  
  
> [!NOTE]  
>  Puede asociar una lista de propiedades de búsqueda a más de un índice de texto completo en la misma base de datos.  
  
 **Para crear una lista de propiedades de búsqueda**  
  
-   [Buscar propiedades de documento con listas de propiedades de búsqueda](../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
 **Recuento de elementos de texto completo de tabla**  
 Indica el número de filas que se han indizado con índice de texto completo correctamente.  
  
 Esta propiedad corresponde a la propiedad `TableFulltextItemCount` devuelta por la función OBJECTPROPERTYEX de [!INCLUDE[tsql](../includes/tsql-md.md)].  
  
 **Documentos de texto completo de tabla procesados**  
 Muestra el número de filas que se han procesado desde el comienzo de la indización de texto completo. En una tabla que se indiza para búsquedas en texto completo, todas las columnas de una fila se consideran como parte de un documento que se va a indizar. No se cuentan las filas eliminadas.  
  
|||  
|-|-|  
|0|Indica que la indización de texto completo se ha completado y no hay ningún rellenado activo.|  
|> 0|Con un rellenado activo, indica el número de documentos procesados por las operaciones de inserción u actualización desde que se realizara alguna de las operaciones siguientes: un rellenado, la habilitación del seguimiento de cambios con rellenado de índices de actualización en segundo plano (como el seguimiento de cambios automático), el cambio del esquema de índice de texto completo, la regeneración del catálogo de texto completo, la reinicialización de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], etc.|  
  
 **Cambios pendientes de texto completo de tabla**  
 Número de entradas de seguimiento de cambios pendientes de procesamiento.  
  
 0 = El seguimiento de cambios no está habilitado.  
  
 NULL = La tabla no tiene un índice de texto completo.  
  
 **Recuento de errores de texto completo de tabla**  
 Número de filas que no ha indizado la búsqueda de texto completo.  
  
 0 = El rellenado se ha completado.  
  
 \>0 = uno de los siguientes:  
  
-   Número de documentos no indizados desde el comienzo del rellenado de seguimiento de cambios de actualización completa, incremental o manual.  
  
-   Para el seguimiento de cambios con actualización de índices en segundo plano, el número de filas no indizadas desde el comienzo del rellenado o desde su reinicio. Esto podría ser debido a un cambio de esquema, una regeneración del catálogo, un reinicio del servidor, etc.  
  
 **Indexación de texto completo habilitada**  
 Especifica si la indización de texto completo está habilitada.  
  
|||  
|-|-|  
|**Reales**|habilitado|  
|**Es**|Disabled|  
  
 **Seguimiento de cambios**  
 Especifica si la tabla tiene el seguimiento de cambios de texto completo habilitado y, en ese caso, qué tipo. El seguimiento de cambios de texto completo mantiene un registro de las filas que se han modificado en una tabla o vista indizada configurada para la indización de texto completo. Estos cambios se pueden propagar al índice de texto completo.  
  
 Los valores de **Seguimiento de cambios** son los siguientes:  
  
|||  
|-|-|  
|**Desactivado**|El índice de texto completo no se actualiza con los cambios en los datos subyacentes.|  
|**Manual**|El índice de texto completo no se actualiza automáticamente cuando se producen cambios en los datos subyacentes. Sin embargo, estos cambios se mantienen y puede propagarlos al índice de texto completo según una programación usando el Agente SQL Server o de forma manual.|  
|**Automática**|El índice de texto completo se actualiza automáticamente cuando se producen cambios en los datos subyacentes de la tabla base.|  
  
 **Volver a llenar el índice**  
 Haga clic para iniciar un rellenado en el índice de texto completo en salir del cuadro de diálogo. Seleccione uno de los tipos de rellenado siguientes:  
  
|||  
|-|-|  
|**Completa**|Durante el rellenado completo de una tabla, se crean entradas de índice para todas las filas.|  
|**Incremental**|El rellenado incremental actualiza el índice de texto completo de las filas que se hayan agregado, eliminado o modificado desde el último rellenado o en su transcurso. Realizar un rellenado incremental requiere que la tabla base contenga una columna del tipo de datos `timestamp`.|  
|**Update**|El índice de texto completo se actualiza siempre que se modifican los datos de la tabla base.|  
  
## <a name="see-also"></a>Consulte también  
 [Introducción a la búsqueda de texto completo](../relational-databases/search/get-started-with-full-text-search.md)  
  
  
