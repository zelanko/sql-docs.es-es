---
title: Compatibilidad con FILESTREAM (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad6aa7b55906e68dba6615140ef2c6afcc3efaa5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62668938"
---
# <a name="filestream-support-ole-db"></a>Compatibilidad con FILESTREAM (OLE DB)
  A partir [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, OLE DB es compatible con la característica mejorada FILESTREAM. Para obtener más información sobre esta característica, consulte [compatibilidad con FILESTREAM](../features/filestream-support.md). Para obtener ejemplos, vea [Filestream y OLE DB](../../native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Para enviar y recibir valores `varbinary(max)` mayores de 2 GB, una aplicación usa `DBTYPE_IUNKNOWN` en enlaces de resultados y parámetros. Para los parámetros del proveedor debe llamar a IUnknown:: QueryInterface de ISequentialStream y de resultados que devuelven ISequentialStream.  
  
 Para OLE DB, comprobación relacionadas con los valores de ISequentialStream será más flexible. Cuando *wType* es `DBTYPE_IUNKNOWN` en el `DBBINDING` struct, comprobación de la longitud puede ser deshabilitado omitiendo `DBPART_LENGTH` desde *dwPart* o estableciendo la longitud de los datos (en desplazamiento *obLength* en el búfer de datos) en ~ 0. En este caso, el proveedor no comprobará la longitud del valor y solicitará y devolverá todos los datos disponibles a través del flujo. Este cambio se aplicará a todos los tipos de objeto grandes (LOB) y XML, pero solo cuando se realice la conexión a los servidores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (o posteriores). Esto proporcionará mayor flexibilidad para los programadores, a la vez que se mantendrá la coherencia y la compatibilidad con versiones anteriores para las aplicaciones existentes y los servidores de nivel inferior.  
  
 Este cambio afecta a todas las interfaces que transfieren datos, principalmente IRowset:: GetData, ICommand:: Execute e IRowsetFastLoad:: insertRow.  
  
## <a name="see-also"></a>Vea también  
 [Programación de SQL Server Native Client](../sql-server-native-client-programming.md)  
  
  
