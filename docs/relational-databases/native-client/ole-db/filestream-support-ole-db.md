---
title: Compatibilidad con FILESTREAM (OLE DB) | Microsoft Docs
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
ms.openlocfilehash: 48202e2a4dea8447d02e093f731915cbf3ab6ee4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787731"
---
# <a name="filestream-support-ole-db"></a>Compatibilidad con FILESTREAM (OLE DB)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]

  A partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10,0, OLE DB admite la característica FileStream mejorada. Para obtener más información acerca de esta característica, vea [compatibilidad de FileStream](../../../relational-databases/native-client/features/filestream-support.md). Para ver ejemplos, consulte [FileStream y OLE DB](../../../relational-databases/native-client-ole-db-how-to/filestream/filestream-and-ole-db.md).  
  
 Para enviar y recibir valores **varbinary(max)** mayores de 2 GB, una aplicación usa **DBTYPE_IUNKNOWN** en enlaces de resultados y parámetros. En el caso de los parámetros, el proveedor debe llamar a IUnknown::QueryInterface para ISequentialStream y para los resultados que devuelven ISequentialStream.  
  
 Para OLE DB, la comprobación relacionada con los valores ISequentialStream será menos estricta. Cuando *wType* es **DBTYPE_IUNKNOWN** en el struct **DBBINDING**, la comprobación de longitud se puede deshabilitar omitiendo **DBPART_LENGTH** en *dwPart* o estableciendo la longitud de los datos (en el desplazamiento *obLength* del búfer de datos) en ~0. En este caso, el proveedor no comprobará la longitud del valor y solicitará y devolverá todos los datos disponibles a través del flujo. Este cambio se aplicará a todos los tipos de objeto grandes (LOB) y XML, pero solo cuando se realice la conexión a los servidores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (o posteriores). Esto proporcionará mayor flexibilidad para los programadores, a la vez que se mantendrá la coherencia y la compatibilidad con versiones anteriores para las aplicaciones existentes y los servidores de nivel inferior.  
  
 Este cambio afecta a todas las interfaces que transfieren datos, principalmente IRowset::GetData, ICommand::Execute y IRowsetFastLoad::InsertRow.  
  
## <a name="see-also"></a>Consulte también  
 [Programación de SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
