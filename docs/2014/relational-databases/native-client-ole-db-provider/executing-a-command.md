---
title: Ejecución de un comando | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 47307455468a20351c3a3cda2a619e6296fb29ad
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704730"
---
# <a name="executing-a-command"></a>Ejecutar un comando
  Una vez establecida la conexión a un origen de datos, el consumidor llama al método **IDBCreateSession::CreateSession** para crear una sesión. La sesión actúa como un comando, conjunto de filas o fábrica de transacciones.  
  
 Para trabajar directamente con índices o tablas individuales, el consumidor solicita la interfaz `IOpenRowset`. El método `IOpenRowset::OpenRowset` se abre y devuelve un conjunto de filas que incluye todas las filas de un índice o tabla base única.  
  
 Para ejecutar un comando (como SELECT \* from authors), el consumidor solicita la `IDBCreateCommand` interfaz. El consumidor puede ejecutar el método `IDBCreateCommand::CreateCommand` para crear un objeto de comando y solicitar la interfaz `ICommandText`. El método `ICommandText::SetCommandText` se usa para especificar el comando que se va a ejecutar.  
  
 El comando `Execute` se utiliza para ejecutar el comando. El comando puede ser cualquier instrucción SQL o nombre de procedimiento. No todos los comandos generan un objeto de conjunto de resultados (conjunto de filas). Comandos como SELECT * FROM Autores generan un conjunto de resultados.  
  
## <a name="see-also"></a>Consulte también  
 [Crear una aplicación de proveedor OLE DB de SQL Server Native Client](creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
