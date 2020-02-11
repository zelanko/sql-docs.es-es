---
title: Compatibilidad con FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], SQL Server Native Client
- SQL Server Native Client [FILESTREAM support]
ms.assetid: 1ad3400d-7fcd-40c9-87ae-f5afc61e0374
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33e447048f7058ee81b0b144f0aa94a370f6d670
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046271"
---
# <a name="filestream-support"></a>Compatibilidad con FILESTREAM
  FILESTREAM proporciona un modo de almacenar y obtener acceso a valores binarios grandes, ya sea a través de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o mediante acceso directo al sistema de archivos de Windows. Un valor binario grande es un valor superior a 2 gigabytes (GB). Para obtener más información acerca de la compatibilidad mejorada con FILESTREAM, vea [filestream &#40;SQL Server&#41;](../../blob/filestream-sql-server.md).  
  
 Cuando se abra una conexión de base de datos, `@@TEXTSIZE` se establecerá en -1 ("ilimitado") de forma predeterminada.  
  
 También es posible obtener acceso a columnas FILESTREAM y actualizarlas mediante las API del sistema de archivos de Windows.  
  
 Para obtener más información, vea los temas siguientes:  
  
-   [Compatibilidad con FILESTREAM &#40;OLE DB&#41;](../ole-db/filestream-support-ole-db.md)  
  
-   [Compatibilidad de FILESTREAM &#40;&#41;ODBC](../odbc/filestream-support-odbc.md)  
  
-   [Obtener acceso a los datos FILESTREAM con OpenSqlFilestream](../../blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>Consulta de columnas FILESTREAM  
 Los conjuntos de filas de esquema de OLE DB no notificarán si una columna es una columna FILESTREAM. ITableDefinition de OLE DB no puede utilizarse para crear una columna FILESTREAM.  
  
 Las funciones de catálogo como SQLColumns en ODBC no notificarán si una columna es una columna FILESTREAM.  
  
 Para crear columnas FILESTREAM o para detectar qué columnas existentes son columnas FILESTREAM, puede usar la `is_filestream` columna de la vista de catálogo [Sys. Columns](/sql/relational-databases/system-catalog-views/sys-columns-transact-sql) .  
  
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
 Si el cliente se compiló con la versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que se incluía [!INCLUDE[ssVersion2005](../../../includes/sscurrent-md.md)]con `varbinary(max)` , el comportamiento será compatible [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]con. Es decir, el tamaño máximo de los datos devueltos se limitará a 2 GB. Los resultados cuyo valor supere los 2 GB, se truncarán, y se devolverá una advertencia de tipo "datos de cadena truncados por la derecha".  
  
 Cuando la compatibilidad de tipo de datos se establezca en 80, el comportamiento del cliente será coherente con el comportamiento del cliente de nivel inferior.  
  
 En el caso de los clientes que usan SQLOLEDB u otros proveedores que [!INCLUDE[ssVersion2005](../../../includes/ssnoversion-md.md)] se publicaron `varbinary(max)` antes que Native Client, se asignarán a la imagen.  
  
## <a name="see-also"></a>Consulte también  
 [Características de SQL Server Native Client](sql-server-native-client-features.md)  
  
  
