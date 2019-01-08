---
title: Creación de una aplicación de proveedor SQL Server Native Client OLE DB | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, application creation
- applications [SQL Server Native Client]
- OLE DB, creating applications
ms.assetid: f3ae6815-f32d-4913-a1a2-2ba2f20cfd88
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e422ac6535900a287ae610a85241dc67172c4f7
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53357736"
---
# <a name="creating-a-sql-server-native-client-ole-db-provider-application"></a>Crear una aplicación de proveedor OLE DB de SQL Server Native Client
  Creación de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicación del proveedor OLE DB de Native Client incluye los siguientes pasos:  
  
1.  Establecer una conexión con un origen de datos.  
  
2.  Ejecutar un comando.  
  
3.  Procesar los resultados.  
  
> [!NOTE]  
>  Siempre que sea posible, utilice la autenticación de Windows. Si la autenticación de Windows no está disponible, solicite a los usuarios que escriban sus credenciales en tiempo de ejecución. No guarde las credenciales en un archivo. Si tiene que conservar las credenciales, debería cifrarlas con la [cryptoAPI de Win32](https://go.microsoft.com/fwlink/?LinkId=9504).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Establecer una conexión con un origen de datos](establishing-a-connection-to-a-data-source.md)  
  
-   [Ejecutar un comando](executing-a-command.md)  
  
-   [Procesar resultados](processing-results.md)  
  
-   [Acerca de las propiedades de OLE DB](about-ole-db-properties.md)  
  
-   [Usar la cláusula OUTPUT con OLE DB en SQL Server Native Client](using-the-output-clause-with-ole-db-in-sql-server-native-client.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
