---
title: Crear un controlador OLE DB para la aplicación de SQL Server | Documentos de Microsoft
description: Crear un controlador de OLE DB para la aplicación de SQL Server
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
- OLE DB Driver for SQL Server, application creation
- applications [OLE DB Driver for SQL Server]
- OLE DB, creating applications
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bbd9dafbd44b83d5e33c41980ca4c4fb9dc63e0e
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="creating-an-ole-db-driver-for-sql-server-application"></a>Crear un controlador OLE DB para la aplicación de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Crear un controlador de OLE DB para la aplicación de SQL Server incluye los siguientes pasos:  
  
1.  Establecer una conexión con un origen de datos.  
  
2.  Ejecutar un comando.  
  
3.  Procesar los resultados.  
  
> [!NOTE]  
>  Siempre que sea posible, utilice la autenticación de Windows. Si la autenticación de Windows no está disponible, solicite a los usuarios que escriban sus credenciales en tiempo de ejecución. No guarde las credenciales en un archivo. Si debe conservar las credenciales, debería cifrarlas con [cryptoAPI de Win32](http://go.microsoft.com/fwlink/?LinkId=9504).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Establecer una conexión con un origen de datos](../../oledb/ole-db-driver/establishing-a-connection-to-a-data-source.md)  
  
-   [Ejecutar un comando](../../oledb/ole-db-driver/executing-a-command.md)  
  
-   [Procesar resultados](../../oledb/ole-db-driver/processing-results.md)  
  
-   [Acerca de las propiedades OLE DB](../../oledb/ole-db-driver/about-ole-db-properties.md)  
  
-   [Uso de la cláusula OUTPUT con OLE DB en el controlador de OLE DB para SQL Server](../../oledb/ole-db-driver/using-the-output-clause-with-ole-db-in-oledb-driver-for-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para SQL Server &#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)  
  
  
