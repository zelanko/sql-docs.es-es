---
title: Compatibilidad con FILESTREAM (OLE DB) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ba270b26a5a290f5b5c6fdd2830f10b9bf695037
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106083"
---
# <a name="filestream-support-ole-db"></a>Compatibilidad con FILESTREAM (OLE DB)
  A partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0, OLE DB es compatible con la característica mejorada FILESTREAM. Para obtener más información sobre esta característica, consulte [compatibilidad con FILESTREAM](../features/filestream-support.md). Para obtener ejemplos, vea [Filestream y OLE DB](../../native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Para enviar y recibir valores `varbinary(max)` mayores de 2 GB, una aplicación usa `DBTYPE_IUNKNOWN` en enlaces de resultados y parámetros. Para los parámetros del proveedor debe llamar a IUnknown:: QueryInterface para ISequentialStream y para obtener los resultados que devuelven ISequentialStream.  
  
 Para OLE DB, comprobación relacionadas con valores de ISequentialStream será menos estricta. Cuando *wType* es `DBTYPE_IUNKNOWN` en el `DBBINDING` struct, comprobación de la longitud puede ser deshabilitada omitiendo `DBPART_LENGTH` de *dwPart* o estableciendo la longitud de los datos (en desplazamiento *obLength* en el búfer de datos) en ~ 0. En este caso, el proveedor no comprobará la longitud del valor y solicitará y devolverá todos los datos disponibles a través del flujo. Este cambio se aplicará a todos los tipos de objeto grandes (LOB) y XML, pero solo cuando se realice la conexión a los servidores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (o posteriores). Esto proporcionará mayor flexibilidad para los programadores, a la vez que se mantendrá la coherencia y la compatibilidad con versiones anteriores para las aplicaciones existentes y los servidores de nivel inferior.  
  
 Este cambio afecta a todas las interfaces que transfieren datos, principalmente IRowset:: GetData, ICommand:: Execute e IRowsetFastLoad:: insertRow.  
  
## <a name="see-also"></a>Vea también  
 [Programación de SQL Server Native Client](../sql-server-native-client-programming.md)  
  
  