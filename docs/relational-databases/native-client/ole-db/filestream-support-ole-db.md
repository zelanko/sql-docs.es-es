---
title: Compatibilidad con FILESTREAM (OLE DB) Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB [FILESTREAM support]
- FILESTREAM [SQL Server], OLE DB
ms.assetid: c2bd3dfd-6103-43d1-859e-8ed8d19c58d3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: da09fc65de4be75798730fd0cc9785204a0c6917
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303716"
---
# <a name="filestream-support-ole-db"></a>Compatibilidad con FILESTREAM (OLE DB)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  A [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] partir [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de Native Client 10.0, OLE DB admite la característica FILESTREAM mejorada. Para obtener más información acerca de esta característica, vea [Compatibilidad con FILESTREAM](../../../relational-databases/native-client/features/filestream-support.md). Para ver ejemplos, consulte [FileStream y OLE DB](../../../relational-databases/native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Para enviar y recibir valores **varbinary(max)** mayores de 2 GB, una aplicación usa **DBTYPE_IUNKNOWN** en enlaces de resultados y parámetros. En el caso de los parámetros, el proveedor debe llamar a IUnknown::QueryInterface para ISequentialStream y para los resultados que devuelven ISequentialStream.  
  
 Para OLE DB, la comprobación relacionada con los valores ISequentialStream será menos estricta. Cuando *wType* es **DBTYPE_IUNKNOWN** en el struct **DBBINDING**, la comprobación de longitud se puede deshabilitar omitiendo **DBPART_LENGTH** en *dwPart* o estableciendo la longitud de los datos (en el desplazamiento *obLength* del búfer de datos) en ~0. En este caso, el proveedor no comprobará la longitud del valor y solicitará y devolverá todos los datos disponibles a través del flujo. Este cambio se aplicará a todos los tipos de objeto grandes (LOB) y XML, pero solo cuando se realice la conexión a los servidores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (o posteriores). Esto proporcionará mayor flexibilidad para los programadores, a la vez que se mantendrá la coherencia y la compatibilidad con versiones anteriores para las aplicaciones existentes y los servidores de nivel inferior.  
  
 Este cambio afecta a todas las interfaces que transfieren datos, principalmente IRowset::GetData, ICommand::Execute y IRowsetFastLoad::InsertRow.  
  
## <a name="see-also"></a>Consulte también  
 [Programación de SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
