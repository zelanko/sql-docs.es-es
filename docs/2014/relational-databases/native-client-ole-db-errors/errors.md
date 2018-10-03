---
title: Errores | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
ms.assetid: bd0612f4-96ef-4919-b0f9-b5447210fe93
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4011730642355fb3161eed13428491e2692c9298
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158985"
---
# <a name="errors"></a>Errores
  Los objetos OLE/COM notifican errores a través del código de retorno HRESULT de funciones de miembro de objeto. Una estructura OLE/COM HRESULT es una estructura empaquetada de bits. OLE proporciona macros que eliminan referencias a los miembros de la estructura.  
  
 OLE/COM especifica la interfaz **IErrorInfo**. La interfaz expone métodos como **GetDescription**. Esto permite a los clientes extraer detalles de error de servidores OLE/COM. OLE DB extiende **IErrorInfo** para admitir el retorno de varios paquetes de información de error en una ejecución de función de miembro único.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede devolver varios errores. Una aplicación puede recuperar los errores de servidor de uno en uno mediante una llamada a [IMultipleResults::GetResult](http://go.microsoft.com/fwlink/?LinkId=129630) combinada con ISQLErrorInfo e IErrorRecords.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la OLE DB mejorado por registro **IErrorInfo**, personalizado `ISQLErrorInfo`y específico del proveedor [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) objeto error interfaces.  
  
 Para obtener información sobre cómo realizar un seguimiento de los errores, vea [Data Access Tracing](http://go.microsoft.com/fwlink/?LinkId=125805) (Seguimiento de acceso a datos). Para obtener información acerca de las mejoras de seguimiento de errores que agregó en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], consulte [acceso a información de diagnóstico en el registro de eventos extendidos](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Códigos de retorno](return-codes.md)  
  
-   [Información en interfaces de error](information-in-error-interfaces.md)  
  
-   [Detalle del error de SQL Server](sql-server-error-detail.md)  
  
-   [Recuperar información sobre errores](retrieving-error-information.md)  
  
-   [Resultados del mensaje de SQL Server](sql-server-message-results.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
