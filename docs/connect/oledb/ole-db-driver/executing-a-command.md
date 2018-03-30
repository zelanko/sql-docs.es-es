---
title: Ejecutar un comando | Documentos de Microsoft
description: Ejecutar un comando
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- commands [OLE DB Driver for SQL Server]
- OLE DB, executing commands
- sessions [OLE DB Driver for SQL Server]
- OLE DB extensions for XML
- OLE DB Driver for SQL Server, command execution
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ac58c67053284ba6b60aebd9a47307f97c34886
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="executing-a-command"></a>Ejecutar un comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Una vez establecida la conexión a un origen de datos, el consumidor llama a la **IDBCreateSession::** método para crear una sesión. La sesión actúa como un comando, conjunto de filas o fábrica de transacciones.  
  
 Para trabajar directamente con índices o tablas individuales, el consumidor solicita la **IOpenRowset** interfaz. El **IOpenRowset:: OpenRowset** método abre y devuelve un conjunto de filas que incluye todas las filas de una única tabla base o índice.  
  
 Para ejecutar un comando (como SELECT \* FROM Authors), el consumidor solicita la **IDBCreateCommand** interfaz. El consumidor puede ejecutar la **IDBCreateCommand:: CreateCommand** método para crear un objeto de comando y solicitar la **ICommandText** interfaz. El **ICommandText:: SetCommandText** método se utiliza para especificar el comando que se va a ejecutar.  
  
 El **Execute** comando se usa para ejecutar el comando. El comando puede ser cualquier instrucción SQL o nombre de procedimiento. No todos los comandos generan un objeto de conjunto de resultados (conjunto de filas). Comandos como SELECT * FROM Autores generan un conjunto de resultados.  
  
## <a name="see-also"></a>Vea también  
 [Crear un controlador OLE DB para la aplicación de SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
