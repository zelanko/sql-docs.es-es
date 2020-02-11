---
title: 'Apéndice A: proveedores | Microsoft Docs'
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
ms.openlocfilehash: 4ffecfc87ec23fc4d62174dae31220511c9f72d4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926979"
---
# <a name="appendix-a-data-and-service-providers"></a>Apéndice A: proveedores de datos y servicios
En esta sección se tratan tres tipos de proveedores: proveedores de datos, proveedores de servicios y componentes de servicio. Los proveedores se dividen en dos categorías: aquellas que proporcionan datos y que proporcionan servicios. Un *proveedor de datos* posee sus propios datos y los expone en formato tabular a la aplicación. Un *proveedor de servicios* encapsula un servicio mediante la generación y el consumo de datos, lo que aumenta las características de las aplicaciones de ADO. También se puede definir un proveedor de servicios como *componente de servicio*, que debe funcionar junto con otros proveedores de servicios o componentes.

## <a name="data-providers"></a>Proveedores de datos
 ADO es eficaz y flexible porque puede conectarse a cualquiera de los distintos proveedores de datos y seguir exponiendo el mismo modelo de programación, independientemente de las características específicas de cualquier proveedor determinado.

 Sin embargo, dado que cada proveedor de datos es único, el modo en que la aplicación interactúa con ADO variará ligeramente en función del proveedor de datos. Las diferencias suelen corresponder a una de estas tres categorías:

-   Parámetros de conexión en la propiedad [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) .

-   Uso del objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) .

-   Comportamiento del [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) específico del proveedor.

 Los detalles de cada uno de los proveedores de datos disponibles actualmente en Microsoft se muestran como se indica a continuación.

|Área|Tema|
|----------|-----------|
|Bases de datos ODBC|[Proveedor Microsoft OLE DB para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)|
|Servicio de Index Server de Microsoft|[Proveedor Microsoft OLE DB para el Servicio de Microsoft Index Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md)|
|Servicio de Active Directory|[Proveedor de Microsoft OLE DB para el servicio Microsoft Active Directory](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)|
|Bases de datos de Microsoft Jet|[Proveedor de OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md)|
|Microsoft SQL Server|[Proveedor OLE DB de Microsoft para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)|
|bases de datos Oracle|[Proveedor OLE DB de Microsoft para Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md)|
|Publicación en Internet|[Proveedor de Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)|
|Orígenes de datos simples|[Proveedor simple de Microsoft OLE DB](../../../ado/guide/appendixes/microsoft-ole-db-simple-provider.md)|

## <a name="provider-specific-dynamic-properties"></a>Propiedades dinámicas específicas del proveedor
 Las colecciones de [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) de los objetos [Connection](../../../ado/reference/ado-api/connection-object-ado.md), [Command](../../../ado/reference/ado-api/command-object-ado.md)y [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) incluyen propiedades dinámicas específicas del proveedor. Estas propiedades proporcionan información sobre la funcionalidad específica del proveedor más allá de las propiedades integradas que admite ADO.

 Después de establecer la conexión y crear estos objetos, utilice el método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) en la colección **Properties** del objeto para obtener las propiedades específicas del proveedor. Consulte la documentación del proveedor y la [Guía del programador de OLE DB](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) para obtener información detallada acerca de estas propiedades dinámicas.

## <a name="service-providers"></a>Proveedores de servicios
 Para usar un proveedor de servicios, debe proporcionar una palabra clave. También debe tener en cuenta las propiedades dinámicas específicas del proveedor asociadas a cada proveedor de servicios. Los detalles específicos del proveedor se enumeran para cada proveedor de servicios que está disponible actualmente en Microsoft:

-   [Datos de Microsoft para dar forma al servicio para información general acerca OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)

-   [Proveedor de persistencia de Microsoft OLE DB](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)

-   [Proveedor de servicios remotos de Microsoft OLE DB](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)

## <a name="service-components"></a>Componentes del servicio
 El [servicio de cursor para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) componente de servicio complementa las funciones de compatibilidad de cursores de los proveedores de datos. También requiere una palabra clave y tiene propiedades dinámicas.

 Para obtener más información acerca de los proveedores de OLE DB, vea [OLE DB de Microsoft](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx).

## <a name="provider-commands"></a>Comandos de proveedor
 Para cada proveedor que se muestra aquí, si las aplicaciones permiten a los usuarios especificar instrucciones SQL como comandos de proveedor, siempre debe validar los datos proporcionados por el usuario y estar atento a posibles ataques de hacker mediante `DROP TABLE t1`instrucciones SQL potencialmente peligrosas, como, como parte de la entrada del usuario.

## <a name="see-also"></a>Consulte también
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/command-object-ado.md) [objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [proveedor de Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md) proveedor de [microsoft OLE DB para Microsoft Active Directory Service](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md) [Microsoft OLE DB Provider para el servicio de microsoft Index Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-indexing-service.md) [Microsoft OLE DB](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md) Provider para ODBC [proveedor OLE DB de Microsoft para Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) [proveedor de OLE DB de](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) Microsoft para SQL Server proveedor de Microsoft OLE DB para la colección de propiedades [de Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md) [(ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [ Object (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [Refresh (método) (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
