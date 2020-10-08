---
title: Creación de una aplicación del controlador OLE DB para SQL Server | Microsoft Docs
description: Obtenga información sobre los pasos necesarios para crear una aplicación de OLE DB Driver for SQL Server y busque recursos adicionales.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, application creation
- applications [OLE DB Driver for SQL Server]
- OLE DB, creating applications
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed150ea18d1141e6116efe177e65836c235cf703
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727234"
---
# <a name="creating-an-ole-db-driver-for-sql-server-application"></a>Creación de un controlador OLE DB para la aplicación de SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La creación de una aplicación de OLE DB Driver for SQL Server implica estos pasos:  
  
1.  Establecer una conexión con un origen de datos.  
  
2.  Ejecutar un comando.  
  
3.  Procesar los resultados.  
  
> [!NOTE]  
>  Siempre que sea posible, utilice la autenticación de Windows. Si la autenticación de Windows no está disponible, solicite a los usuarios que escriban sus credenciales en tiempo de ejecución. No guarde las credenciales en un archivo. Si tiene que conservar las credenciales, debería cifrarlas con la [cryptoAPI de Win32](/windows/win32/seccng/cng-portal).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Establecer una conexión con un origen de datos](../../oledb/ole-db-driver/establishing-a-connection-to-a-data-source.md)  
  
-   [Ejecutar un comando](../../oledb/ole-db-driver/executing-a-command.md)  
  
-   [Procesar resultados](../../oledb/ole-db-driver/processing-results.md)  
  
-   [Acerca de las propiedades de OLE DB](../../oledb/ole-db-driver/about-ole-db-properties.md)  
  
-   [Uso de la cláusula OUTPUT con OLE DB en el controlador de OLE DB para SQL Server](../../oledb/ole-db-driver/using-the-output-clause-with-ole-db-in-oledb-driver-for-sql-server.md)  
  
## <a name="see-also"></a>Consulte también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
