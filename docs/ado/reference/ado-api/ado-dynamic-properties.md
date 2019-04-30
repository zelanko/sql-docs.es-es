---
title: Propiedades dinámicas de ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO]
- properties [ADO], dynamic
ms.assetid: d7b06d72-f792-4328-93a2-5006b9e2c581
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c940fbdc48d900da77d03dfb3b806080cff0c04e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63249049"
---
# <a name="ado-dynamic-properties"></a>Propiedades dinámicas de ADO
Propiedades dinámicas se pueden agregar a la [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colecciones de la [conexión](../../../ado/reference/ado-api/connection-object-ado.md), [comando](../../../ado/reference/ado-api/command-object-ado.md), o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos. El origen de estas propiedades es un proveedor de datos, como el [proveedor OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), o un proveedor de servicios, como el [servicio de cursores de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md). Hacen referencia al proveedor de datos adecuado o la documentación del proveedor de servicio para obtener más información sobre una propiedad dinámica concreta.  
  
 El [índice de propiedades dinámicas de ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) proporciona una referencia cruzada entre los nombres ADO y OLE DB para cada propiedad dinámica del proveedor OLE DB estándar.  
  
 Las siguientes propiedades dinámicas son especialmente interesantes y también se documentan en los orígenes que se mencionaron anteriormente. La funcionalidad especial con ADO se documenta en los temas de Ayuda de ADO en la lista siguiente.  
  
|||  
|-|-|  
|[Optimización](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)|Especifica si se debe crear un índice en este campo.|  
|[Prompt](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)|Especifica si el proveedor OLE DB debe solicitar al usuario información de inicialización.|  
|[Cambiar la forma de nombre](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)|Especifica un nombre para el **Recordset** objeto.|  
|[Resincronizar comando](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)|Especifica la cadena de un comando proporcionado por el usuario que la **Resync** problemas del método para actualizar los datos en la tabla mencionada en el **Unique Table** propiedad dinámica.|  
|[Tabla única, Unique Schema, Unique Catalog](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**Tabla única** especifica el nombre de la tabla base en la que se permiten actualizaciones, inserciones y eliminaciones.<br /><br /> **Esquema único** especifica el esquema o el nombre del propietario de la tabla.<br /><br /> **Catálogo único** especifica el catálogo o el nombre de la base de datos que contiene la tabla.|  
|[Resincronización de la actualización](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)|Especifica si el **UpdateBatch** método va seguido de un modo implícito **Resync** operación del método y si es así, el ámbito de esa operación.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de API de ADO](../../../ado/reference/ado-api/ado-api-reference.md)   
 [Colecciones de ADO](../../../ado/reference/ado-api/ado-collections.md)   
 [Constantes enumeradas de ADO](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Apéndice B: Errores de ADO](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [Eventos de ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Métodos de ADO](../../../ado/reference/ado-api/ado-methods.md)   
 [Modelo de objetos ADO](../../../ado/reference/ado-api/ado-object-model.md)   
 [Interfaces y los objetos ADO](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Propiedades de ADO](../../../ado/reference/ado-api/ado-properties.md)
