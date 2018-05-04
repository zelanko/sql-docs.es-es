---
title: Errores | Documentos de Microsoft
description: Errores
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b95b26c453df083a6fc1e7463eb512bf30f7f271
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="errors"></a>Errores
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Los objetos OLE/COM notifican errores a través del código de retorno HRESULT de funciones de miembro de objeto. Una estructura OLE/COM HRESULT es una estructura empaquetada de bits. OLE proporciona macros que eliminan referencias a los miembros de la estructura.  
  
 OLE/COM especifica la **IErrorInfo** interfaz. La interfaz expone métodos como **GetDescription**. Esto permite a los clientes extraer detalles de error de servidores OLE/COM. OLE DB extiende **IErrorInfo** para admitir la devolución de varios paquetes de información de error en una ejecución de la función de miembro único.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede devolver varios errores. Una aplicación puede recuperar los errores de servidor uno a la vez mediante una llamada a [IMultipleResults:: GetResult](http://go.microsoft.com/fwlink/?LinkId=129630) combinado con ISQLErrorInfo y IErrorRecords.  
  
 El controlador OLE DB para SQL Server expone OLE DB mejorado por registro **IErrorInfo**, personalizado **ISQLErrorInfo**y específico del proveedor [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) error interfaces del objeto.  
  
 Para obtener información acerca de los errores de seguimiento, vea [seguimiento de acceso a datos](http://go.microsoft.com/fwlink/?LinkId=125805). Para obtener información acerca de las mejoras de seguimiento de errores que se agregó en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], consulte [acceso a información de diagnóstico en el registro de eventos extendidos](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Códigos de retorno](../../oledb/ole-db-errors/return-codes.md)  
  
-   [Información de Interfaces de Error](../../oledb/ole-db-errors/information-in-error-interfaces.md)  
  
-   [Detalles del Error SQL Server](../../oledb/ole-db-errors/sql-server-error-detail.md)  
  
-   [Error al recuperar la información](../../oledb/ole-db-errors/retrieving-error-information.md)  
  
-   [Resultados del mensaje de SQL Server](../../oledb/ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>Vea también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
