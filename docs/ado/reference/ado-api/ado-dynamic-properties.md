---
title: Propiedades dinámicas de ADO | Microsoft Docs
ms.prod: sql
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
author: rothja
ms.author: jroth
ms.openlocfilehash: 72fa5fd287b285ca7f917c5969b0e27e11837d25
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82749298"
---
# <a name="ado-dynamic-properties"></a>Propiedades dinámicas de ADO
Se pueden agregar propiedades dinámicas a las colecciones de [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) de los objetos [Connection](../../../ado/reference/ado-api/connection-object-ado.md), [Command](../../../ado/reference/ado-api/command-object-ado.md)o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) . El origen de estas propiedades es un proveedor de datos, como el [proveedor de OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), o un proveedor de servicios, como [Microsoft Cursor Service para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md). Consulte la documentación correspondiente del proveedor de datos o del proveedor de servicios para obtener más información sobre una propiedad dinámica específica.  
  
 El [Índice de propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) proporciona una referencia cruzada entre los nombres ADO y OLE DB para cada propiedad dinámica de proveedor de OLE DB estándar.  
  
 Las siguientes propiedades dinámicas son especialmente interesantes y también se documentan en los orígenes que se mencionaron anteriormente. En los temas de ayuda de ADO de la lista siguiente se documenta la funcionalidad especial con ADO.  
  
|||  
|-|-|  
|[Optimize](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) (Optimizar)|Especifica si se debe crear un índice en este campo.|  
|[Aviso](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)|Especifica si el proveedor de OLE DB debe solicitar al usuario la información de inicialización.|  
|[Nombre de la reformación](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Especifica un nombre para el objeto de **conjunto de registros** .|  
|[Comando Resync](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Especifica una cadena de comandos proporcionada por el usuario que el método **Resync** emite para actualizar los datos de la tabla denominada en la propiedad dinámica de **tabla única** .|  
|[Tabla única, esquema único, catálogo único](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**Tabla única** Especifica el nombre de la tabla base en la que se permiten las actualizaciones, las inserciones y las eliminaciones.<br /><br /> **Esquema único** Especifica el esquema o el nombre del propietario de la tabla.<br /><br /> **Catálogo único** Especifica el catálogo o el nombre de la base de datos que contiene la tabla.|  
|[Actualizar resincronización](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)|Especifica si el método **UpdateBatch** va seguido de una operación de método **Resync** implícita y, en ese caso, el ámbito de esa operación.|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Consulte también  
 [Referencia de la API de ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Colecciones de ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Constantes enumeradas de ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apéndice B: errores de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos de ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Métodos de ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objetos ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Objetos e interfaces de ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propiedades de ADO](../../../ado/reference/ado-api/ado-properties.md)
