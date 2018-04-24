---
title: 'Apéndice A: proveedores | Documentos de Microsoft'
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- providers [ADO]
- ADO, providers
- service providers [ADO]
- service components [ADO]
ms.assetid: e2581b47-b11e-4e1e-b96c-d39c77c5b48a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ab1ea25e0f2b08956b3462b7b79c8fb28602b3db
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="appendix-a-data-and-service-providers"></a>Apéndice A: datos y proveedores de servicios
En esta sección habla sobre tres tipos de proveedores: proveedores de datos, los proveedores de servicios y componentes de servicio. Los proveedores se dividen en dos categorías: aquellos que proporcionan datos y aquellos que proporcionan servicios. A *proveedor de datos* tiene sus propios datos y expone en formato tabular en su aplicación. A *proveedor de servicios* encapsula un servicio al producir y consumir datos, aumentan las características de las aplicaciones ADO. Un proveedor de servicios también se puede definir más como una *componente del servicio*, que debe funcionar conjuntamente con otros componentes o proveedores de servicios.

## <a name="data-providers"></a>Proveedores de datos
 ADO es eficaz y flexible porque puede conectarse a cualquiera de varios proveedores de datos y seguir exponiendo el mismo modelo de programación, sin tener en cuenta las características específicas de un proveedor determinado.

 Sin embargo, dado que cada proveedor de datos es único, cómo interactúa la aplicación con ADO variará ligeramente por el proveedor de datos. Las diferencias suelen clasificarse en tres categorías:

-   Parámetros de conexión en el [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad.

-   [Comando](../../../ado/reference/ado-api/command-object-ado.md) uso del objeto.

-   Específico del proveedor [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) comportamiento.

 Como se indica a continuación se muestran los detalles de cada uno de los proveedores de datos disponibles actualmente en Microsoft.

|Área|Tema|
|----------|-----------|
|Bases de datos ODBC|[Proveedor Microsoft OLE DB para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)|
|Servicios de Index Server de Microsoft|[Proveedor Microsoft OLE DB para servicios de Index Server de Microsoft](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Servicio de Active Directory|[Proveedor Microsoft OLE DB para el servicio de Microsoft Active Directory](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Bases de datos de Microsoft Jet|[Proveedor OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Proveedor Microsoft OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)|
|bases de datos Oracle|[Proveedor Microsoft OLE DB para Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)|
|Publicación en Internet|[Proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)|
|Orígenes de datos simples|[Proveedor sencillo de OLE DB de Microsoft](../../../ado/guide/appendixes/microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>Propiedades dinámicas específicas del proveedor
 El [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colecciones de la [conexión](../../../ado/reference/ado-api/connection-object-ado.md), [comando](../../../ado/reference/ado-api/command-object-ado.md), y [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos incluyen propiedades dinámicas específicas para el proveedor. Estas propiedades proporcionan información sobre la funcionalidad específica para el proveedor más allá de las propiedades integradas que ADO admite.

 Después de establecer la conexión y crear estos objetos, use la [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método en el **propiedades** colección del objeto para obtener las propiedades específicas del proveedor. Consulte la documentación del proveedor y el [Guía del programador de OLE DB](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) para obtener información detallada acerca de estas propiedades dinámicas.

## <a name="service-providers"></a>Proveedores de servicios
 Para usar un proveedor de servicios, debe proporcionar una palabra clave. También debe ser consciente de las propiedades dinámicas específicas del proveedor asociadas con cada proveedor de servicios. Se muestran detalles específicos del proveedor para cada proveedor de servicio que está actualmente disponible de Microsoft:

-   [Datos de Microsoft para dar forma al servicio para información general acerca OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Proveedor de persistencia de Microsoft OLE DB](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Proveedor de servicios remotos de OLE DB de Microsoft](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>Componentes del servicio
 El [servicio de cursores para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) componente del servicio complementa las funciones de compatibilidad de cursor de proveedores de datos. También requiere una palabra clave y tiene propiedades dinámicas.

 Para obtener más información acerca de los proveedores OLE DB, vea [Microsoft OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx).

## <a name="provider-commands"></a>Comandos de proveedor
 Para cada proveedor enumerado aquí, si las aplicaciones permiten a los usuarios especificar instrucciones SQL como comandos de proveedor, siempre debe validar la entrada del usuario y estar alerta ante ataques de piratas informáticos posibles mediante instrucciones SQL potencialmente peligrosas, como `DROP TABLE t1`, como parte de la entrada del usuario.

## <a name="see-also"></a>Vea también
 [Comando (objeto) (ADO)](../../../ado/reference/ado-api/command-object-ado.md) [objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) [proveedor Microsoft OLE DB para el servicio de Microsoft Active Directory ](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [Proveedor Microsoft OLE DB para servicios de Index Server de Microsoft](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md) [proveedor Microsoft OLE DB para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md) [proveedor Microsoft OLE DB para Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) [Proveedor Microsoft OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) [proveedor Microsoft OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) [colección Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [ Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
