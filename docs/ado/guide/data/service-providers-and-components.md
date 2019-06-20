---
title: Proveedores de servicios y componentes | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9bebbf4c89a04474cbf2d0c88704603cb4c3fef3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700388"
---
# <a name="service-providers-and-components"></a>Proveedores de servicios y componentes
Los proveedores de servicios son componentes que extienden la funcionalidad de los proveedores de datos mediante la implementación de interfaces extendidas que no son compatibles de forma nativa con el almacén de datos.  
  
 Proporciona acceso universal a datos un *arquitectura del componente* que permite a los componentes individuales y especializados implementar conjuntos discretos de la funcionalidad de la base de datos o "servicios", encima de los almacenes de menor capacidad. Por lo tanto, en lugar de forzar cada almacén de datos para proporcionar su propia implementación de la funcionalidad ampliada o forzar aplicaciones genéricas para implementar la funcionalidad de la base de datos internamente, los componentes de servicio proporcionan una implementación común que cualquier aplicación puede Utilice al tener acceso a cualquier almacén de datos. El hecho de que alguna funcionalidad se implementa de forma nativa por el almacén de datos y otros a través de componentes genéricos es transparente para la aplicación.  
  
 Por ejemplo, un cursor de motor, como [el servicio de cursores para OLE DB](https://msdn.microsoft.com/57638feb-4ecd-4051-becb-8f828d21cf44), es un componente de servicio que puede consumir datos desde un almacén de datos secuencial, de solo avance para generar datos desplazables. Otros proveedores de servicio suele usadas ADO son el [proveedor Microsoft OLE DB persistencia (proveedor de servicios de ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) (para guardar datos en un archivo), el [servicio de forma de datos de Microsoft para OLE DB (proveedor de servicios de ADO) ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (para jerárquica **conjuntos de registros**) y el [proveedor Microsoft OLE DB comunicación remota (proveedor de servicios de ADO)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) (para llamar a los proveedores de datos en un equipo remoto).  
  
 Para obtener más información acerca de los proveedores de servicio y los datos, vea [Apéndice A: Los proveedores](../../../ado/guide/appendixes/appendix-a-providers.md).
