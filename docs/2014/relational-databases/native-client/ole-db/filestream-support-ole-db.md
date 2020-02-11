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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62668938"
---
# <a name="filestream-support-ole-db"></a>Compatibilidad con FILESTREAM (OLE DB)
  A partir [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y Native Client 10,0, OLE DB admite la característica FileStream mejorada. Para obtener más información acerca de esta característica, vea [compatibilidad de FileStream](../features/filestream-support.md). Para obtener ejemplos, vea [FileStream y OLE DB](../../native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Para enviar y recibir valores `varbinary(max)` mayores de 2 GB, una aplicación usa `DBTYPE_IUNKNOWN` en enlaces de resultados y parámetros. En el caso de los parámetros, el proveedor debe llamar a IUnknown:: QueryInterface para ISequentialStream y para los resultados que devuelven ISequentialStream.  
  
 Por OLE DB, la comprobación relacionada con los valores de ISequentialStream será relajada. Cuando *wType* está `DBTYPE_IUNKNOWN` en el `DBBINDING` struct, la comprobación de longitud se puede deshabilitar `DBPART_LENGTH` omitiendo en *dwPart* o estableciendo la longitud de los datos (en el desplazamiento *obLength* en el búfer de datos) en ~ 0. En este caso, el proveedor no comprobará la longitud del valor y solicitará y devolverá todos los datos disponibles a través del flujo. Este cambio se aplicará a todos los tipos de objeto grandes (LOB) y XML, pero solo cuando se realice la conexión a los servidores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (o posteriores). Esto proporcionará mayor flexibilidad para los programadores, a la vez que se mantendrá la coherencia y la compatibilidad con versiones anteriores para las aplicaciones existentes y los servidores de nivel inferior.  
  
 Este cambio afecta a todas las interfaces que transfieren datos, principalmente IRowset:: GetData, ICommand:: Execute y IRowsetFastLoad:: InsertRow.  
  
## <a name="see-also"></a>Consulte también  
 [Programación de SQL Server Native Client](../sql-server-native-client-programming.md)  
  
  
