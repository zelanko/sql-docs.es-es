---
title: Conjuntos de filas | Documentos de Microsoft
description: Conjuntos de filas en el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], about rowsets
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets
- OLE DB rowsets, about rowsets
- rowsets [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cc869e7b45716113c529c7ae1194e47464907d23
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="rowsets"></a>Conjuntos de filas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Un conjunto de filas es el que contiene columnas de datos. Los conjuntos de filas son objetos centrales que permiten a todos los proveedores de datos OLE DB exponer los datos del conjunto de resultados en formato tabular.  
  
 Después de que un consumidor crea una sesión mediante el uso de la **IDBCreateSession::** método, el consumidor puede utilizar el **IOpenRowset** o **IDBCreateCommand** interfaz en la sesión que se va a crear un conjunto de filas. El controlador OLE DB para SQL Server es compatible con ambas interfaces. Los dos métodos se describen aquí.  
  
-   Crear un conjunto de filas mediante una llamada a la **IOpenRowset:: OpenRowset** método.  
  
     Esto es equivalente a crear un conjunto de filas sobre una tabla única. Este método se abre y devuelve un conjunto de filas que incluye todas las filas de una tabla base única. Uno de los argumentos a **OpenRowset** es un identificador de tabla que identifica la tabla desde la que se va a crear el conjunto de filas.  
  
-   Crear un objeto de comando mediante una llamada a la **IDBCreateCommand:: CreateCommand** método.  
  
     El objeto de comando ejecuta los comandos que el proveedor admite. Con el controlador OLE DB para SQL Server, el consumidor puede especificar cualquier [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucción, como una instrucción SELECT o una llamada a un procedimiento almacenado. Los pasos para crear un conjunto de filas utilizando un objeto de comando son:  
  
    1.  El consumidor llama el **IDBCreateCommand:: CreateCommand** método en la sesión que se va a obtener un objeto de comando que solicita la **ICommandText** interfaz en el objeto de comando. Esto **ICommandText** interfaz establece y recupera el texto del comando real. El consumidor rellena el comando de texto mediante una llamada a la **ICommandText:: SetCommandText** método.  
  
    2.  El usuario llama el **ICommand:: Execute** método en el comando. El objeto de conjunto de filas generado cuando se ejecuta el comando contiene el conjunto de resultados del comando.  
  
 El consumidor puede utilizar el **ICommandProperties** interfaz para obtener o establecer las propiedades del conjunto de filas devuelto por el comando ejecutado por el **ICommand:: Execute** interfaces. Las propiedades solicitadas normalmente son las interfaces que el conjunto de filas debe admitir. Además de las interfaces, el consumidor puede solicitar propiedades que modifican el comportamiento del conjunto de filas o la interfaz.  
  
 Conjuntos de filas con los consumidores liberan el **IRowset:: Release** método. Al liberar un conjunto de filas se liberan los identificadores de fila mantenidos por el consumidor en ese conjunto de filas. Al liberar un conjunto de filas no se liberan los descriptores de acceso. Si tiene una **IAccessor** interfaz, todavía tiene que liberarse.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Crear un conjunto de filas con IOpenRowset](../../oledb/ole-db-rowsets/creating-a-rowset-with-iopenrowset.md)  
  
-   [Crear conjuntos de filas con ICommand:: Execute](../../oledb/ole-db-rowsets/creating-rowsets-with-icommand-execute.md)  
  
-   [Propiedades del conjunto de filas y los comportamientos](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
-   [Conjuntos de filas y cursores SQL Server](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)  
  
-   [Captura de filas](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
-   [Capturar una única fila con IRow](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
-   [Marcadores](../../oledb/ole-db-rowsets/bookmarks.md)  
  
-   [Actualizar datos en conjuntos de filas](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para SQL Server &#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)  
  
  
