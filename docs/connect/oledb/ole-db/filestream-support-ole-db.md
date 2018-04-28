---
title: Compatibilidad con FILESTREAM (OLE DB) | Documentos de Microsoft
description: Compatibilidad con FILESTREAM (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efbe3ce15444b0c6556cf3cef0267e99bb55657f
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/11/2018
---
# <a name="filestream-support-ole-db"></a>Compatibilidad con FILESTREAM (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] y controlador OLE DB para SQL Server, OLE DB admite la característica mejorada FILESTREAM. Para obtener más información sobre esta característica, consulte [compatibilidad con FILESTREAM](../../oledb/features/filestream-support.md). Para obtener ejemplos, vea [Filestream y OLE DB](../../oledb/ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Para enviar y recibir **varbinary (max)** valores superiores a 2 GB, una aplicación usa **DBTYPE_IUNKNOWN** en enlaces de parámetro y el resultado. Para los parámetros del proveedor debe llamar a IUnknown:: QueryInterface para ISequentialStream y para obtener los resultados que devuelven ISequentialStream.  
  
 Para OLE DB, comprobación relacionadas con valores de ISequentialStream será menos estricta. Cuando *wType* es **DBTYPE_IUNKNOWN** en el **DBBINDING** struct, comprobación de la longitud puede ser deshabilitada omitiendo **DBPART_LENGTH** de *dwPart* o estableciendo la longitud de los datos (en desplazamiento *obLength* en el búfer de datos) en ~ 0. En este caso, el proveedor no comprobará la longitud del valor y solicitará y devolverá todos los datos disponibles a través del flujo. Este cambio se aplicará a todos los tipos de objeto grandes (LOB) y XML, pero solo cuando se realice la conexión a los servidores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (o posteriores). Esto proporcionará mayor flexibilidad para los programadores, a la vez que se mantendrá la coherencia y la compatibilidad con versiones anteriores para las aplicaciones existentes y los servidores de nivel inferior.  
  
 Este cambio afecta a todas las interfaces que transfieren datos, principalmente IRowset:: GetData, ICommand:: Execute e IRowsetFastLoad:: insertRow.  
  
## <a name="see-also"></a>Vea también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/oledb-driver-for-sql-server-programming.md)  
  
  
