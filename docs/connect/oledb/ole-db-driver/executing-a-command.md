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
- drivers
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
ms.openlocfilehash: 48e6fd74fcf6468be92aac9d70a1c4b8ab3a967d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="executing-a-command"></a>Ejecutar un comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Una vez establecida la conexión a un origen de datos, el consumidor llama a la **IDBCreateSession::** método para crear una sesión. La sesión actúa como un comando, conjunto de filas o fábrica de transacciones.  
  
 Para trabajar directamente con índices o tablas individuales, el consumidor solicita la **IOpenRowset** interfaz. El **IOpenRowset:: OpenRowset** método abre y devuelve un conjunto de filas que incluye todas las filas de una única tabla base o índice.  
  
 Para ejecutar un comando (como SELECT \* FROM Authors), el consumidor solicita la **IDBCreateCommand** interfaz. El consumidor puede ejecutar la **IDBCreateCommand:: CreateCommand** método para crear un objeto de comando y solicitar la **ICommandText** interfaz. El **ICommandText:: SetCommandText** método se utiliza para especificar el comando que se va a ejecutar.  
  
 El **Execute** comando se usa para ejecutar el comando. El comando puede ser cualquier instrucción SQL o nombre de procedimiento. No todos los comandos generan un objeto de conjunto de resultados (conjunto de filas). Comandos como SELECT * FROM Autores generan un conjunto de resultados.  
  
## <a name="see-also"></a>Vea también  
 [Creación de un controlador OLE DB para la aplicación de SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
