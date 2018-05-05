---
title: Captura de filas | Documentos de Microsoft
description: Capturar filas mediante la interfaz IRowset
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- IRowset interface
- OLE DB Driver for SQL Server, fetching
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 51f88888b2d6387bb406511b1330dba2113752d7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="fetching-rows"></a>Capturar filas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El **IRowset** es la interfaz de conjunto de filas base. El **IRowset** interfaz proporciona métodos para capturar filas secuencialmente, obtener los datos de las filas y administra las filas. Los consumidores utilizan los métodos de **IRowset** para todas las operaciones básicas de conjunto de filas. Esto incluye la captura y liberación de filas y la obtención de los valores de columna.  
  
 Cuando un consumidor Obtiene un puntero de interfaz en un conjunto de filas, el primer paso es normalmente determinar las capacidades del conjunto de filas utilizando la **IRowsetInfo:: GetProperties** método. Esto devuelve información acerca de las interfaces expuestas por el conjunto de filas y también de las capacidades del conjunto de filas que no se presentan como interfaces distintas, como el número máximo de filas activas y el número de filas que pueden tener actualizaciones pendientes al mismo tiempo.  
  
 El paso siguiente para los consumidores es determinar las características, o los metadatos, de las columnas del conjunto de filas. Para ello utilizan la **IColumnsInfo** método para obtener información de columna simple o **IColumnsRowset** método para obtener información de columna extendida. El **GetColumnInfo** método devuelve la información siguiente:  
  
-   El número de columnas del conjunto de resultados.  
  
-   Una matriz de estructuras DBCOLUMNINFO, una por columna.  
  
     El orden de las estructuras es el orden en que las columnas aparecen en el conjunto de filas. Cada estructura DBCOLUMNINFO incluye los metadatos de columna, como el nombre de la columna, el ordinal de la columna, la longitud máxima posible de un valor de la columna, el tipo de datos de la columna, la precisión y la longitud.  
  
-   El puntero a un almacenamiento para todos los valores de cadena dentro de un bloque de asignación único.  
  
 El consumidor determina qué columnas necesita basándose en los metadatos o en el comando de texto que generó el conjunto de filas. Determina los ordinales de las columnas necesarias de la clasificación de la información de columna devuelta por **IColumnsInfo** o de los ordinales del conjunto de filas de metadatos de columna devueltos por **IColumnsRowset**.  
  
 El **IColumnsInfo** y **IColumnsRowset** interfaces se utilizan para extraer información acerca de las columnas del conjunto de filas. El **IColumnsInfo** interfaz devuelve un conjunto limitado de información, mientras que **IColumnsRowset** proporciona todos los metadatos.  
  
> [!NOTE]  
>  En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] versión 7.0 y anteriores, la columna de metadatos opcionales DBCOLUMN_COMPUTEMODE devuelto por **IColumnsInfo:: GetColumnsInfo** devuelve DBSTATUS_S_ISNULL (en lugar de los valores que describen si la columna es calcula) porque no se puede determinar si se calcula la columna subyacente.  
  
 Los ordinales se utilizan para especificar un enlace a una columna. Un enlace es una estructura que asocia un elemento de la estructura del consumidor a una columna. El enlace puede enlazar el valor de datos, la longitud y el valor de estado de la columna.  
  
 Un conjunto de enlaces se reúne en un descriptor de acceso. Esto se crea mediante la **IAccessor:: CreateAccessor** método. Un descriptor de acceso puede contener varios enlaces para que se puedan recuperar los datos de varias columnas o establecerse en una llamada única. El consumidor puede crear varios descriptores de acceso para coincidir con modelos de uso distintos en distintas partes de la aplicación. Puede crear y liberar los descriptores de acceso mientras que el conjunto de filas sigue existiendo.  
  
 Para capturar filas de la base de datos, el consumidor llama a un método, como **IRowset:: GetNextRows** o **IRowsetLocate:: GetRowsAt**. Estas operaciones de captura colocan los datos de filas del servidor en el búfer de filas del proveedor. El consumidor no tiene acceso directo al búfer de filas del proveedor. El consumidor usa **IRowset:: GetData** para copiar datos desde el búfer del proveedor en el búfer del consumidor y **IRowsetChange:: SetData** para copiar los cambios en los datos del búfer del consumidor en el búfer del proveedor.  
  
 El consumidor llama el **GetData** método y pasa el identificador a una fila, el identificador de un descriptor de acceso y un puntero a un búfer asignado por el consumidor. **GetData** convierte los datos y devuelve las columnas como se especifica en los enlaces utilizados para crear el descriptor de acceso. El consumidor puede llamar a **GetData** más de una vez para una fila, mediante los descriptores de acceso diferentes y búferes y, por tanto, el consumidor puede obtener varias copias de los mismos datos.  
  
 Los datos de las columnas de longitud variable se pueden tratar de varias maneras. Primero, tales columnas se pueden enlazar a una sección finita de la estructura del consumidor. Esto produce un truncamiento cuando la longitud de los datos supera la longitud del búfer. El consumidor puede determinar que se ha producido ese truncamiento comprobando el estado DBSTATUS_S_TRUNCATED. La longitud devuelta siempre es la longitud verdadera en bytes, para que el consumidor pueda determinar también cuántos datos se han truncado.  
  
 Cuando el consumidor ha finalizado la captura o actualización de filas, libera con la **ReleaseRows** método. Esto libera los recursos de la copia de las filas del conjunto de filas y crea espacio para las nuevas filas. A continuación, el consumidor puede repetir su ciclo de captura o creación de filas y obtener acceso a los datos de ellas.  
  
 Cuando el consumidor ha finalizado con el conjunto de filas, se llama a la **IAccessor:: ReleaseAccessor** método para liberar los descriptores de acceso. Lo llama el **IUnknown:: Release** método en todas las interfaces expuestas por el conjunto de filas para liberar el conjunto de filas. Cuando se libera el conjunto de filas, fuerza la liberación de las filas o descriptores de acceso restantes que el consumidor pueda contener.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Posición de captura siguiente](../../oledb/ole-db-rowsets/fetching-rows-next-fetch-position.md)  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
