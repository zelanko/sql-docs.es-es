---
title: Determinación de lo que se admite | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], Supports method
- Supports method [ADO]
ms.assetid: 65090cba-6d46-4775-8d61-f6838e7752a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc42e9128ccc1ccb43996f554ffe280916884307
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925524"
---
# <a name="determining-what-is-supported"></a>Determinar qué se admite
El método **Supports** se usa para determinar si un objeto de **conjunto de registros** especificado admite un tipo determinado de funcionalidad. Tiene la siguiente sintaxis:  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>Observaciones  
 El método **Supports** devuelve un valor booleano que indica si el proveedor admite todas las características identificadas por el argumento CursorOptions. Puede usar el método **Supports** para determinar los tipos de funcionalidad que admite un objeto de **conjunto de registros** . Si el objeto de **conjunto de registros** admite las características cuyas constantes correspondientes están en *CursorOptions*, el método **Supports** devuelve **true**. De lo contrario, devuelve **false**.  
  
 Con el método **Supports** , puede comprobar la capacidad del objeto de **conjunto de registros** para agregar nuevos registros, utilizar marcadores, usar el método **Find** , usar el desplazamiento, usar la propiedad **index** y realizar actualizaciones por lotes. Para obtener una lista completa de las constantes y sus significados, vea [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md).  
  
 Aunque el método **Supports** puede devolver **true** para una funcionalidad determinada, no garantiza que el proveedor pueda hacer que la característica esté disponible en todas las circunstancias. El método **Supports** simplemente devuelve si el proveedor puede admitir la funcionalidad especificada, suponiendo que se cumplen ciertas condiciones. Por ejemplo, el método **Supports** puede indicar que un objeto de **conjunto de registros** admite actualizaciones, aunque el cursor se basa en una combinación de varias tablas; algunas columnas de las cuales no son actualizables.
