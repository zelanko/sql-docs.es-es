---
description: Ejecutar un comando (proveedor de OLE DB de Native Client)
title: Ejecutar un comando (proveedor de OLE DB de Native Client) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- commands [SQL Server Native Client]
- OLE DB, executing commands
- sessions [SQL Server Native Client]
- OLE DB extensions for XML
- SQL Server Native Client OLE DB provider, command execution
ms.assetid: bb0b3cbf-fe45-46ba-b2ec-c5a39e3c7081
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d62e574b27887200b86a201b38520e26c83cf878
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490792"
---
# <a name="executing-a-sql-server-native-client-command"></a>Ejecutar un comando SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Una vez establecida la conexión a un origen de datos, el consumidor llama al método **IDBCreateSession::CreateSession** para crear una sesión. La sesión actúa como un comando, conjunto de filas o fábrica de transacciones.  
  
 Para trabajar directamente con índices o tablas individuales, el consumidor solicita la interfaz **IOpenRowset**. El método **IOpenRowset::OpenRowset** se abre y devuelve un conjunto de filas que incluye todas las filas de un índice o tabla base única.  
  
 Para ejecutar un comando (como SELECT \* FROM Authors), el consumidor solicita la interfaz **IDBCreateCommand**. El consumidor puede ejecutar el método **IDBCreateCommand::CreateCommand** para crear un objeto de comando y solicitar la interfaz **ICommandText**. El método **ICommandText::SetCommandText** se utiliza para especificar el comando que se va a ejecutar.  
  
 El comando **Execute** se utiliza para ejecutar el comando. El comando puede ser cualquier instrucción SQL o nombre de procedimiento. No todos los comandos generan un objeto de conjunto de resultados (conjunto de filas). Comandos como SELECT * FROM Autores generan un conjunto de resultados.  
  
## <a name="see-also"></a>Consulte también  
 [Crear una aplicación de proveedor OLE DB de SQL Server Native Client](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
