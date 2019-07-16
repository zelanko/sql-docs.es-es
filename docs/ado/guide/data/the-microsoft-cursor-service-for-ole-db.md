---
title: El servicio de cursores de Microsoft para OLE DB | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursor service for ole db [ADO]
- cursors [ADO], cursor service for OLE DB
ms.assetid: 1ac3bd9b-2d45-4cc8-88ec-bd8a218cfb49
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aeac8c848f01f01e8969f94c571ad15f5e7f615a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923919"
---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>El servicio de cursores de Microsoft para OLE DB
Cuando se selecciona un cursor de cliente, o establecer el **CursorLocation** propiedad **adUseClient**, está invocando el servicio de cursores de Microsoft para OLE DB. También podría ver referencias a "Client Cursor Engine", que es básicamente lo mismo en el contexto de ADO. Este servicio complementa las funciones de compatibilidad de cursor de proveedores de datos. Como resultado, puede percibir una funcionalidad relativamente uniforme en todos los proveedores de datos.  
  
 El servicio de cursores para OLE DB hace que las propiedades dinámicas que estén disponibles y mejora el comportamiento de ciertos métodos. Por ejemplo, el **optimizar** propiedad dinámica permite la creación de índices temporales para facilitar determinadas operaciones, como el **buscar** método.  
  
 El servicio de cursores habilita la compatibilidad con actualización por lotes en todos los casos. También simula más compatible con tipos de cursor, como los cursores dinámicos, cuando un proveedor de datos solo puede proporcionar cursores menos eficaces, como los cursores estáticos.  
  
## <a name="see-also"></a>Vea también  
 [Servicio de cursores de Microsoft para OLE DB (componente de servicio de ADO)](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)
