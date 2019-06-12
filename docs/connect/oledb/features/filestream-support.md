---
title: Compatibilidad con FILESTREAM | Microsoft Docs
description: Compatibilidad con FILESTREAM del controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server [FILESTREAM support]
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: ebaaf0da2a051106b690f80d4524e675358450c4
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66777785"
---
# <a name="filestream-support"></a>Compatibilidad con FILESTREAM
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Empezando por [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], controlador de OLE DB para SQL Server admite la característica mejorada FILESTREAM. Para obtener ejemplos, vea [Filestream y OLE DB](../../oledb/ole-db-how-to/filestream/filestream-and-ole-db.md).  

FILESTREAM proporciona un modo de almacenar y obtener acceso a valores binarios grandes, ya sea a través de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o mediante acceso directo al sistema de archivos de Windows. Un valor binario grande es un valor superior a 2 gigabytes (GB). Para obtener más información sobre la compatibilidad mejorada con FILESTREAM, vea [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md).  
  
Cuando se abra una conexión de base de datos, **@@TEXTSIZE** se establecerá en -1 ("ilimitado") de forma predeterminada.  
  
También es posible obtener acceso a columnas FILESTREAM y actualizarlas mediante las API del sistema de archivos de Windows.  
  
Para obtener más información, vea [Obtener acceso a los datos FILESTREAM con OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md).  
  
## <a name="querying-for-filestream-columns"></a>Consulta de columnas FILESTREAM  
Los conjuntos de filas de esquema de OLE DB no notificarán si una columna es una columna FILESTREAM. ITableDefinition de OLE DB no puede utilizarse para crear una columna FILESTREAM.    
  
Para crear columnas FILESTREAM o detectar qué columnas existentes son columnas FILESTREAM, puede usar la columna **is_filestream** de la vista de catálogo [sys.columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).  
  
A continuación se muestra un ejemplo:  
  
```sql  
-- Create a table with a FILESTREAM column.  
CREATE TABLE Bob_01 (GuidCol1 uniqueidentifier ROWGUIDCOL NOT NULL UNIQUE DEFAULT NEWID(), IntCol2 int, varbinaryCol3 varbinary(max) FILESTREAM);  
  
-- Find FILESTREAM columns.  
SELECT name FROM sys.columns WHERE is_filestream=1;  
  
-- Determine whether a column is a FILESTREAM column.  
SELECT is_filestream FROM sys.columns WHERE name = 'varbinaryCol3' AND object_id IN (SELECT object_id FROM sys.tables WHERE name='Bob_01');  
```  
  
## <a name="down-level-compatibility"></a>Compatibilidad con niveles inferiores  
Si el cliente se compiló con controlador OLE DB para SQL Server y la aplicación se conecta a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]), a continuación, **varbinary (max)** comportamiento será compatible con el comportamiento introducidos por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Es decir, el tamaño máximo de los datos devueltos se limitará a 2 GB. Los resultados cuyo valor supere los 2 GB, se truncarán, y se devolverá una advertencia de tipo "datos de cadena truncados por la derecha". 
  
Cuando la compatibilidad de tipo de datos se establezca en 80, el comportamiento del cliente será coherente con el comportamiento del cliente de nivel inferior.  
  
En el caso de los clientes que utilicen SQLOLEDB u otros proveedores lanzados al mercado con anterioridad a la versión [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], **varbinary(max)** se asignará a una imagen.  
  
## <a name="comments"></a>Comentarios
- Para enviar y recibir **varbinary (max)** valores mayores que 2 GB, una aplicación usa **DBTYPE_IUNKNOWN** en enlaces de parámetro y resultado. Para los parámetros del proveedor debe llamar a IUnknown:: QueryInterface de ISequentialStream y de resultados que devuelven ISequentialStream.  

-  Para OLE DB, comprobación relacionadas con los valores de ISequentialStream será más flexible. Cuando *wType* es **DBTYPE_IUNKNOWN** en el **DBBINDING** struct, comprobación de la longitud puede ser deshabilitado omitiendo **DBPART_LENGTH** desde *dwPart* o estableciendo la longitud de los datos (en desplazamiento *obLength* en el búfer de datos) en ~ 0. En este caso, el proveedor no comprobará la longitud del valor y solicitará y devolverá todos los datos disponibles a través del flujo. Este cambio se aplicará a todos los tipos de objeto grandes (LOB) y XML, pero solo cuando se realice la conexión a los servidores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (o posteriores). Esto proporcionará mayor flexibilidad para los programadores, a la vez que se mantendrá la coherencia y la compatibilidad con versiones anteriores para las aplicaciones existentes y los servidores de nivel inferior.  Este cambio afecta a todas las interfaces que transfieren datos, principalmente IRowset:: GetData, ICommand:: Execute e IRowsetFastLoad:: insertRow.
 

## <a name="see-also"></a>Consulte también  
 [Controlador OLE DB para las características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
