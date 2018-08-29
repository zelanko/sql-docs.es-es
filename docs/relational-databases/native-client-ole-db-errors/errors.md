---
title: Errores | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2d77f2c11798d128723f766790c601ef40c0c74e
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43073455"
---
# <a name="errors"></a>Errores
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Los objetos OLE/COM notifican errores a través del código de retorno HRESULT de funciones de miembro de objeto. Una estructura OLE/COM HRESULT es una estructura empaquetada de bits. OLE proporciona macros que eliminan referencias a los miembros de la estructura.  
  
 OLE/COM especifica la interfaz **IErrorInfo**. La interfaz expone métodos como **GetDescription**. Esto permite a los clientes extraer detalles de error de servidores OLE/COM. OLE DB extiende **IErrorInfo** para admitir el retorno de varios paquetes de información de error en una ejecución de función de miembro único.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede devolver varios errores. Una aplicación puede recuperar los errores de servidor de uno en uno mediante una llamada a [IMultipleResults::GetResult](http://go.microsoft.com/fwlink/?LinkId=129630) combinada con ISQLErrorInfo e IErrorRecords.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la OLE DB mejorado por registro **IErrorInfo**, personalizado **ISQLErrorInfo**y específico del proveedor [ISQLServerErrorInfo ](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) interfaces del objeto de error.  
  
 Para obtener información sobre cómo realizar un seguimiento de los errores, vea [Data Access Tracing](http://go.microsoft.com/fwlink/?LinkId=125805) (Seguimiento de acceso a datos). Para obtener información acerca de las mejoras de seguimiento de errores que agregó en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], consulte [acceso a información de diagnóstico en el registro de eventos extendidos](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Códigos de retorno](../../relational-databases/native-client-ole-db-errors/return-codes.md)  
  
-   [Información en interfaces de error](../../relational-databases/native-client-ole-db-errors/information-in-error-interfaces.md)  
  
-   [Detalle del error de SQL Server](../../relational-databases/native-client-ole-db-errors/sql-server-error-detail.md)  
  
-   [Recuperar información sobre errores](../../relational-databases/native-client-ole-db-errors/retrieving-error-information.md)  
  
-   [Resultados del mensaje de SQL Server](../../relational-databases/native-client-ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
