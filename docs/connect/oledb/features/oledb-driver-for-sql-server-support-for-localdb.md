---
title: Compatibilidad del controlador OLE DB para SQL Server con LocalDB | Microsoft Docs
description: Compatibilidad del controlador OLE DB para SQL Server con LocalDB
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 099ffb2203397bd02b91af68651ccb42a23e2b5b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802969"
---
# <a name="ole-db-driver-for-sql-server-support-for-localdb"></a>Controlador OLE DB para la compatibilidad de SQL Server con LocalDB
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  A partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], estará disponible una versión ligera de SQL Server, denominada LocalDB. En este tema se describe cómo conectarse a una base de datos en una instancia de LocalDB.  
  
## <a name="remarks"></a>Notas  
 Para obtener más información acerca de LocalDB, incluyendo cómo instalarlo y configurar la instancia de LocalDB, vea:  
  
-   [Referencia de SQL Server Express LocalDB](../../../relational-databases/sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2016 Express LocalDB](../../../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
 En resumen, LocalDB permite:  
  
-   Usar **sqllocaldb.exe i** para detectar el nombre de la instancia predeterminada.  
  
-   Usar la palabra clave de la cadena de conexión de **AttachDBFilename** para especificar a qué el archivo de base de datos se debe adjuntar el servidor. Al utilizar **AttachDBFilename**, si no especifica el nombre de la base de datos con la palabra clave de la cadena de conexión **Database** , la base de datos se quitará de la instancia de LocalDB cuando se cierre la aplicación.  
  
-   Especifique una instancia de LocalDB en la cadena de conexión:  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 Si fuera necesario, puede crear una instancia de LocalDB con sqllocaldb.exe. También puede utilizar sqlcmd.exe para agregar y modificar las bases de datos de una instancia de LocalDB. Por ejemplo, **sqlcmd -S (localdb)\v11.0**.  
  
## <a name="see-also"></a>Consulte también  
 [Controlador OLE DB para las características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
