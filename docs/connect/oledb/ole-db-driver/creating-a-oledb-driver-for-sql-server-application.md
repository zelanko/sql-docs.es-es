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
ms.openlocfilehash: 49a9f20904c5719960cbffc7ca94c825def7231c
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862335"
---
# <a name="creating-an-ole-db-driver-for-sql-server-application"></a>Creación de un controlador OLE DB para la aplicación de SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La creación de una aplicación de OLE DB Driver for SQL Server implica estos pasos:  
  
1.  Establecer una conexión con un origen de datos.  
  
2.  Ejecutar un comando.  
  
3.  Procesar los resultados.  
  
> [!NOTE]  
>  Siempre que sea posible, utilice la autenticación de Windows. Si la autenticación de Windows no está disponible, solicite a los usuarios que escriban sus credenciales en tiempo de ejecución. No guarde las credenciales en un archivo. Si tiene que conservar las credenciales, debería cifrarlas con la [cryptoAPI de Win32](https://go.microsoft.com/fwlink/?LinkId=9504).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Establecer una conexión con un origen de datos](../../oledb/ole-db-driver/establishing-a-connection-to-a-data-source.md)  
  
-   [Ejecutar un comando](../../oledb/ole-db-driver/executing-a-command.md)  
  
-   [Procesar resultados](../../oledb/ole-db-driver/processing-results.md)  
  
-   [Acerca de las propiedades de OLE DB](../../oledb/ole-db-driver/about-ole-db-properties.md)  
  
-   [Uso de la cláusula OUTPUT con OLE DB en el controlador de OLE DB para SQL Server](../../oledb/ole-db-driver/using-the-output-clause-with-ole-db-in-oledb-driver-for-sql-server.md)  
  
## <a name="see-also"></a>Consulte también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
