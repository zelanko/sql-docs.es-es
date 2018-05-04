---
title: Crear un controlador OLE DB para la aplicación de SQL Server | Documentos de Microsoft
description: Crear un controlador de OLE DB para la aplicación de SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
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
manager: craigg
ms.openlocfilehash: 697e3f5e563c360f744e5703ca74b3b5557bfbf8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
