---
title: SQL Server Native Client con LocalDB | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 127569d1-a9f7-49bf-a561-c084986a8871
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1da6a606a8a79aa96cff1cd9b51dd234fe729b94
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395149"
---
# <a name="sql-server-native-client-support-for-localdb"></a>Compatibilidad de SQL Server Native Client con LocalDB
  A partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], estará disponible una versión ligera de SQL Server, denominada LocalDB. En este tema se describe cómo conectarse a una base de datos en una instancia de LocalDB.  
  
## <a name="remarks"></a>Notas  
 Para obtener más información acerca de LocalDB, incluyendo cómo instalarlo y configurar la instancia de LocalDB, vea:  
  
-   [Referencia de SQL Server Express LocalDB](../../sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2014 Express LocalDB](../../../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
 En resumen, LocalDB permite:  
  
-   Usar `sqllocaldb.exe i` para detectar el nombre de la instancia predeterminada.  
  
-   Usar la palabra clave de la cadena de conexión de `AttachDBFilename` para especificar a qué el archivo de base de datos se debe adjuntar el servidor. Cuando se usa `AttachDBFilename`, si no especifica el nombre de la base de datos con el **base de datos** palabra clave de cadena de conexión, la base de datos se quitará de la instancia de LocalDB cuando se cierra la aplicación.  
  
-   Especifique una instancia de LocalDB en la cadena de conexión:  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 Si fuera necesario, puede crear una instancia de LocalDB con sqllocaldb.exe. También puede utilizar sqlcmd.exe para agregar y modificar las bases de datos de una instancia de LocalDB. Por ejemplo, `sqlcmd -S (localdb)\v11.0`.  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](sql-server-native-client-features.md)  
  
  
