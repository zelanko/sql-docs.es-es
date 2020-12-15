---
description: Errores de SQL Server Native Client
title: Errores | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 081840769704810709a1c6445d167e5bb6a51328
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97433578"
---
# <a name="sql-server-native-client-errors"></a>Errores de SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Los objetos OLE/COM notifican errores a través del código de retorno HRESULT de funciones de miembro de objeto. Una estructura OLE/COM HRESULT es una estructura empaquetada de bits. OLE proporciona macros que eliminan referencias a los miembros de la estructura.  
  
 OLE/COM especifica la interfaz **IErrorInfo**. La interfaz expone métodos como **GetDescription**. Esto permite a los clientes extraer detalles de error de servidores OLE/COM. OLE DB extiende **IErrorInfo** para admitir el retorno de varios paquetes de información de error en una ejecución de función de miembro único.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede devolver varios errores. Una aplicación puede recuperar los errores de servidor de uno en uno mediante una llamada a [IMultipleResults::GetResult](/previous-versions/windows/desktop/ms721289(v=vs.85)) combinada con ISQLErrorInfo e IErrorRecords.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client expone el OLE DB con registro mejorado: **IErrorInfo**, el **ISQLErrorInfo** personalizado y las interfaces del objeto de error [ISQLServerErrorInfo](../native-client-ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md) específicas del proveedor.  
  
 Para obtener información sobre cómo realizar un seguimiento de los errores, vea [Data Access Tracing](/previous-versions/sql/sql-server-2008/cc765421(v=sql.100)) (Seguimiento de acceso a datos). Para información sobre las mejoras en el seguimiento de errores agregadas en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], consulte [Acceso a información de diagnóstico en el registro de eventos extendidos](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Códigos de retorno](../../relational-databases/native-client-ole-db-errors/return-codes.md)  
  
-   [Información en interfaces de error](../../relational-databases/native-client-ole-db-errors/information-in-error-interfaces.md)  
  
-   [Detalle del error de SQL Server](../../relational-databases/native-client-ole-db-errors/sql-server-error-detail.md)  
  
-   [Recuperar información sobre errores](../../relational-databases/native-client-ole-db-errors/retrieving-error-information.md)  
  
-   [Resultados del mensaje de SQL Server](../../relational-databases/native-client-ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
