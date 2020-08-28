---
description: El servicio de cursores de Microsoft para OLE DB
title: El servicio de cursores de Microsoft para OLE DB | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursor service for ole db [ADO]
- cursors [ADO], cursor service for OLE DB
ms.assetid: 1ac3bd9b-2d45-4cc8-88ec-bd8a218cfb49
author: rothja
ms.author: jroth
ms.openlocfilehash: ce59aa28e8db4716b0e27c848ce774b489ff5891
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979376"
---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>El servicio de cursores de Microsoft para OLE DB
Cuando se selecciona un cursor del lado cliente o se establece la propiedad **CursorLocation** en **adUseClient**, se invoca el servicio de cursores de Microsoft para OLE DB. También puede ver referencias al "motor de cursor de cliente", que básicamente es lo mismo en el contexto de ADO. Este servicio complementa las funciones de compatibilidad de cursores de los proveedores de datos. Como resultado, puede percibir funcionalidad relativamente uniforme de todos los proveedores de datos.  
  
 El servicio de cursor para OLE DB hace que las propiedades dinámicas estén disponibles y mejora el comportamiento de ciertos métodos. Por ejemplo, la propiedad dinámica **Optimize** permite la creación de índices temporales para facilitar ciertas operaciones, como el método **Find** .  
  
 El servicio de cursor habilita la compatibilidad con la actualización por lotes en todos los casos. También simula tipos de cursor más compatibles, como los cursores dinámicos, cuando un proveedor de datos solo puede proporcionar cursores menos compatibles, como cursores estáticos.  
  
## <a name="see-also"></a>Consulte también  
 [Microsoft cursor Service para OLE DB (componente de servicio ADO)](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)
