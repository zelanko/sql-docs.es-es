---
title: 'Apéndice A: Proveedores | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- providers [ADO]
- ADO, providers
- service providers [ADO]
- service components [ADO]
ms.assetid: e2581b47-b11e-4e1e-b96c-d39c77c5b48a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3f31e5522fdac506e31ffe0bbaa5ad76e3fae87b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701560"
---
# <a name="appendix-a-data-and-service-providers"></a>Apéndice A: Datos y proveedores de servicios
Esta sección tratan tres tipos de proveedores: proveedores de datos, los proveedores de servicios y componentes del servicio. Los proveedores se dividen en dos categorías: aquellos que proporcionan datos y aquellos que proporcionan servicios. Un *proveedor de datos* posee sus propios datos y los expone en formato tabular en la aplicación. Un *proveedor de servicios* encapsula un servicio al producir y consumir datos, aumentan las características de las aplicaciones ADO. Un proveedor de servicios también se puede definir aún más como un *componente del servicio*, que debe trabajar junto con otros proveedores de servicios o componentes.

## <a name="data-providers"></a>Proveedores de datos
 ADO es eficaz y flexible ya que puede conectarse a cualquiera de varios proveedores de datos y exponer sigue el modelo de programación mismo, independientemente de las características específicas de un proveedor determinado.

 Sin embargo, dado que cada proveedor de datos es único, cómo interactúa la aplicación con ADO variará ligeramente por el proveedor de datos. Normalmente, las diferencias se dividen en tres categorías:

-   Parámetros de conexión en el [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad.

-   [Comando](../../../ado/reference/ado-api/command-object-ado.md) uso de objetos.

-   Específico del proveedor [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) comportamiento.

 Como se indica a continuación se muestran los detalles de cada uno de los proveedores de datos están disponibles en Microsoft.

|Área|Tema|
|----------|-----------|
|Bases de datos ODBC|[Proveedor Microsoft OLE DB para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)|
|Servicios de Index Server de Microsoft|[Proveedor Microsoft OLE DB para servicios de Index Server de Microsoft](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Servicio de Active Directory|[Proveedor Microsoft OLE DB para el servicio de Microsoft Active Directory](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Microsoft Jet databases|[Proveedor OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Proveedor Microsoft OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)|
|bases de datos Oracle|[Proveedor Microsoft OLE DB para Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)|
|Publicación en Internet|[Proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)|
|Orígenes de datos simples|[Proveedor sencillo de OLE DB de Microsoft](../../../ado/guide/appendixes/microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>Propiedades dinámicas específicas del proveedor
 El [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colecciones de la [conexión](../../../ado/reference/ado-api/connection-object-ado.md), [comando](../../../ado/reference/ado-api/command-object-ado.md), y [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos incluyen propiedades dinámicas específicas de la proveedor. Estas propiedades proporcionan información sobre la funcionalidad específica para el proveedor más allá de las propiedades integradas que es compatible con ADO.

 Después de establecer la conexión y crear estos objetos, utilice el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método en el **propiedades** colección del objeto para obtener las propiedades específicas del proveedor. Consulte la documentación del proveedor y el [Guía del programador de OLE DB](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) para obtener información detallada acerca de estas propiedades dinámicas.

## <a name="service-providers"></a>Proveedores de servicios
 Para usar un proveedor de servicios, debe proporcionar una palabra clave. También debe tener en cuenta las propiedades dinámicas específicas del proveedor asociadas con cada proveedor de servicios. Se muestran detalles específicos del proveedor para cada proveedor de servicios que esté disponible de Microsoft:

-   [Datos de Microsoft para dar forma al servicio para información general acerca OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Proveedor de persistencia OLE DB de Microsoft](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Proveedor de servicios remotos de OLE DB de Microsoft](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>Componentes del servicio
 El [servicio de cursores para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) componente del servicio complementa las funciones de compatibilidad de cursor de proveedores de datos. También requiere una palabra clave y tiene las propiedades dinámicas.

 Para obtener más información acerca de los proveedores OLE DB, consulte [Microsoft OLE DB](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx).

## <a name="provider-commands"></a>Comandos de proveedor
 Para cada proveedor enumerado aquí, si las aplicaciones permiten a los usuarios escribir instrucciones SQL como comandos de proveedor, siempre debe validar la entrada del usuario y estar alerta ante los ataques de piratas informáticos posible mediante instrucciones SQL potencialmente peligrosas, como `DROP TABLE t1`, como parte de la entrada del usuario.

## <a name="see-also"></a>Vea también
 [Comando (ADO) del objeto](../../../ado/reference/ado-api/command-object-ado.md) [el objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) [proveedor Microsoft OLE DB para el servicio de Microsoft Active Directory ](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [Proveedor Microsoft OLE DB para servicios de Index Server de Microsoft](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md) [proveedor Microsoft OLE DB para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md) [proveedor Microsoft OLE DB para Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) [Proveedor Microsoft OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) [proveedor Microsoft OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) [colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [ Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
