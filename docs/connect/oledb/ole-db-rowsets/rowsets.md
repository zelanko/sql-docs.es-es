---
title: Conjuntos de filas (controlador OLE DB)
description: Obtenga información sobre las interfaces que admiten un consumidor mediante la creación de un conjunto de filas en una sesión en OLE DB Driver for SQL Server. Para más información, consulte los artículos que aparecen en esta sección.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], about rowsets
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets
- OLE DB rowsets, about rowsets
- rowsets [OLE DB]
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55100932092abeb81da7fa1c156ccb5a61fc193c
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88859945"
---
# <a name="rowsets"></a>Conjuntos de filas
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Un conjunto de filas es el que contiene columnas de datos. Los conjuntos de filas son objetos centrales que permiten a todos los proveedores de datos OLE DB exponer los datos del conjunto de resultados en formato tabular.  
  
 Después de que un consumidor crea una sesión mediante el método **IDBCreateSession::CreateSession**, el consumidor puede usar la interfaz **IDBCreateCommand** o **IOpenRowset** en la sesión para crear un conjunto de filas. OLE DB Driver for SQL Server admite ambas interfaces. Los dos métodos se describen aquí.  
  
-   Cree un conjunto de filas mediante una llamada al método **IOpenRowset::OpenRowset**.  
  
     Esto es equivalente a crear un conjunto de filas sobre una tabla única. Este método se abre y devuelve un conjunto de filas que incluye todas las filas de una tabla base única. Uno de los argumentos de **OpenRowset** es un identificador de tabla que identifica la tabla desde la que se va a crear el conjunto de filas.  
  
-   Cree un objeto de comando mediante una llamada al método **IDBCreateCommand::CreateCommand**.  
  
     El objeto de comando ejecuta los comandos que el proveedor admite. Con el controlador OLE DB para SQL Server, el consumidor puede especificar cualquier instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)], como una instrucción SELECT o una llamada a un procedimiento almacenado. Los pasos para crear un conjunto de filas utilizando un objeto de comando son:  
  
    1.  El consumidor llama al método **IDBCreateCommand::CreateCommand** en la sesión para obtener un objeto de comando que solicita la interfaz **ICommandText** en el objeto de comando. Esta interfaz **ICommandText** establece y recupera el texto del comando real. El consumidor rellena el comando de texto mediante una llamada al método **ICommandText::SetCommandText**.  
  
    2.  El usuario llama al método **ICommand::Execute** en el comando. El objeto de conjunto de filas generado cuando se ejecuta el comando contiene el conjunto de resultados del comando.  
  
 El consumidor puede usar la interfaz **ICommandProperties** para obtener o establecer las propiedades del conjunto de filas devuelto por el comando ejecutado por las interfaces **ICommand::Execute**. Las propiedades solicitadas normalmente son las interfaces que el conjunto de filas debe admitir. Además de las interfaces, el consumidor puede solicitar propiedades que modifican el comportamiento del conjunto de filas o la interfaz.  
  
 Los consumidores liberan los conjuntos de filas con el método **IRowset::Release**. Al liberar un conjunto de filas se liberan los identificadores de fila mantenidos por el consumidor en ese conjunto de filas. Al liberar un conjunto de filas no se liberan los descriptores de acceso. Si tiene una interfaz **IAccessor**, todavía tiene que liberarse.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Crear un conjunto de filas con IOpenRowset](../../oledb/ole-db-rowsets/creating-a-rowset-with-iopenrowset.md)  
  
-   [Crear conjuntos de filas con ICommand:: Execute](../../oledb/ole-db-rowsets/creating-rowsets-with-icommand-execute.md)  
  
-   [Propiedades y comportamientos de conjuntos de filas](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
-   [Conjuntos de filas y cursores de SQL Server](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)  
  
-   [Capturar filas](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
-   [Capturar una única fila con IRow](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
-   [Marcadores](../../oledb/ole-db-rowsets/bookmarks.md)  
  
-   [Actualizar datos en conjuntos de filas](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
## <a name="see-also"></a>Consulte también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
