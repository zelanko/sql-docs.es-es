---
title: Proveedores de servicios y componentes | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d44d3ce48da69c734b381058637b15b7afd0736c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="service-providers-and-components"></a>Proveedores de servicios y componentes
Proveedores de servicios son componentes que extienden la funcionalidad de los proveedores de datos mediante la implementación de interfaces extendidas que no son compatibles de forma nativa con el almacén de datos.  
  
 Proporciona acceso universal a los datos de un *arquitectura de componentes* que permite que los componentes individuales y especializados implementar conjuntos discretos de funcionalidad de base de datos, o "servicios", en almacenes con menos funcionalidades. Por lo tanto, en lugar de forzar cada almacén de datos para proporcionar su propia implementación de la funcionalidad ampliada o forzar aplicaciones genéricas para implementar la funcionalidad de la base de datos internamente, los componentes de servicios proporcionan una implementación común que cualquier aplicación puede usar al obtener acceso a cualquier almacén de datos. El hecho de que se implementa alguna funcionalidad de forma nativa por el almacén de datos y la otra mediante componentes genéricos es transparente para la aplicación.  
  
 Por ejemplo, un cursor motor, como [el servicio de Cursor para OLE DB](http://msdn.microsoft.com/en-us/57638feb-4ecd-4051-becb-8f828d21cf44), es un componente de servicio que puede consumir datos desde un almacén de datos secuencial, de sólo avance para generar datos desplazables. Otros proveedores de servicio suele usadas ADO son el [proveedor Microsoft OLE DB persistencia (proveedor de servicios ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) (para guardar datos en un archivo), el [servicio de forma de datos de Microsoft para OLE DB (proveedor de servicios ADO) ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (para jerárquica **conjuntos de registros**) y el [proveedor Microsoft OLE DB Remoting (proveedor de servicios ADO)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) (para llamar a proveedores de datos en un equipo remoto).  
  
 Para obtener más información acerca de los proveedores de servicio y los datos, vea [Apéndice A: proveedores](../../../ado/guide/appendixes/appendix-a-providers.md).
