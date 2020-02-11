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
ms.openlocfilehash: a78db07f5ba445c54108558b2ff222bd217c2bbe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924243"
---
# <a name="service-providers-and-components"></a>Proveedores de servicios y componentes
Los proveedores de servicios son componentes que amplían la funcionalidad de los proveedores de datos mediante la implementación de interfaces extendidas que no son compatibles de forma nativa con el almacén de datos.  
  
 Universal Data Access proporciona una *arquitectura de componentes* que permite a los componentes individuales y especializados implementar conjuntos discretos de funcionalidad de base de datos, o "servicios", sobre almacenes menos compatibles. Por lo tanto, en lugar de obligar a cada almacén de datos a proporcionar su propia implementación de funcionalidad ampliada o forzar a las aplicaciones genéricas a implementar la funcionalidad de la base de datos internamente, los componentes de servicio proporcionan una implementación común que cualquier aplicación puede Use al acceder a cualquier almacén de datos. El hecho de que alguna funcionalidad esté implementada de forma nativa por el almacén de datos y otros a través de componentes genéricos sea transparente para la aplicación.  
  
 Por ejemplo, un motor de cursor, como [el servicio de cursor para OLE DB](https://msdn.microsoft.com/57638feb-4ecd-4051-becb-8f828d21cf44), es un componente de servicio que puede consumir datos de un almacén de datos secuencial de solo avance para generar datos desplazables. Entre otros proveedores de servicios usados normalmente por ADO se incluye el [proveedor de persistencia de microsoft OLE DB (proveedor de servicios ADO)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) (para guardar datos en un archivo), el [servicio de forma de datos de Microsoft para OLE DB (proveedor de servicios ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (para los **conjuntos de registros**jerárquicos) y el [proveedor de comunicación remota de Microsoft OLE DB (proveedor de servicios de ADO)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) .  
  
 Para obtener más información sobre el servicio y los proveedores de datos, vea [Apéndice A: proveedores](../../../ado/guide/appendixes/appendix-a-providers.md).
