---
title: Compatibilidad con FILESTREAM | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], SQL Server Native Client
- SQL Server Native Client [FILESTREAM support]
ms.assetid: 1ad3400d-7fcd-40c9-87ae-f5afc61e0374
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d87fe1e36603dd8880ba258d44ee7cb32b3efcd5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="filestream-support"></a>Compatibilidad con FILESTREAM
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  FILESTREAM proporciona un modo de almacenar y obtener acceso a valores binarios grandes, ya sea a través de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o mediante acceso directo al sistema de archivos de Windows. Un valor binario grande es un valor superior a 2 gigabytes (GB). Para obtener más información acerca de la compatibilidad mejorada con FILESTREAM, vea [FILESTREAM &#40; SQL Server &#41; ](../../../relational-databases/blob/filestream-sql-server.md).  
  
 Cuando se abre una conexión de base de datos, **@@TEXTSIZE**  se establecerá en -1 ("sin límite"), de forma predeterminada.  
  
 También es posible obtener acceso a columnas FILESTREAM y actualizarlas mediante las API del sistema de archivos de Windows.  
  
 Para obtener más información, consulte los temas siguientes:  
  
-   [Compatibilidad con FILESTREAM &#40; OLE DB &#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [Compatibilidad con FILESTREAM &#40; ODBC &#41;](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [Obtener acceso a los datos FILESTREAM con OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>Consulta de columnas FILESTREAM  
 Los conjuntos de filas de esquema de OLE DB no notificarán si una columna es una columna FILESTREAM. ITableDefinition en OLE DB no puede utilizarse para crear una columna FILESTREAM.  
  
 Funciones de catálogo como SQLColumns de ODBC no notificará si una columna es una columna FILESTREAM.  
  
 Para crear columnas FILESTREAM o detectar qué columnas existentes son columnas FILESTREAM, puede usar el **is_filestream** columna de la [sys.columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) vista de catálogo.  
  
 A continuación se muestra un ejemplo:  
  
```  
-- Create a table with a FILESTREAM column.  
CREATE TABLE Bob_01 (GuidCol1 uniqueidentifier ROWGUIDCOL NOT NULL UNIQUE DEFAULT NEWID(), IntCol2 int, varbinaryCol3 varbinary(max) FILESTREAM);  
  
-- Find FILESTREAM columns.  
SELECT name FROM sys.columns WHERE is_filestream=1;  
  
-- Determine whether a column is a FILESTREAM column.  
SELECT is_filestream FROM sys.columns WHERE name = 'varbinaryCol3' AND object_id IN (SELECT object_id FROM sys.tables WHERE name='Bob_01');  
```  
  
## <a name="down-level-compatibility"></a>Compatibilidad con niveles inferiores  
 Si el cliente se compiló con la versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que se incluía con [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], y la aplicación se conecta a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], **varbinary (max)** comportamiento es compatible con [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Es decir, el tamaño máximo de los datos devueltos se limitará a 2 GB. Para los valores de resultado mayor que 2 GB, se producirá un truncamiento y se devolverá una advertencia "cadena datos truncados por la derecha".  
  
 Cuando la compatibilidad de tipo de datos se establezca en 80, el comportamiento del cliente será coherente con el comportamiento del cliente de nivel inferior.  
  
 Para los clientes que utilicen SQLOLEDB u otros proveedores que se hayan publicado antes el [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, **varbinary (max)** se van a asignar a la imagen.  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
