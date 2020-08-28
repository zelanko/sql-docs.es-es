---
description: Determinar qué se admite
title: Determinación de lo que se admite | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], Supports method
- Supports method [ADO]
ms.assetid: 65090cba-6d46-4775-8d61-f6838e7752a6
author: rothja
ms.author: jroth
ms.openlocfilehash: c2caaf9e708b9a9fccd728472c7b13857978fdbe
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991386"
---
# <a name="determining-what-is-supported"></a>Determinar qué se admite
El método **Supports** se usa para determinar si un objeto de **conjunto de registros** especificado admite un tipo determinado de funcionalidad. Tiene la siguiente sintaxis:  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="remarks"></a>Observaciones  
 El método **Supports** devuelve un valor booleano que indica si el proveedor admite todas las características identificadas por el argumento CursorOptions. Puede usar el método **Supports** para determinar los tipos de funcionalidad que admite un objeto de **conjunto de registros** . Si el objeto de **conjunto de registros** admite las características cuyas constantes correspondientes están en *CursorOptions*, el método **Supports** devuelve **true**. De lo contrario, devuelve **false**.  
  
 Con el método **Supports** , puede comprobar la capacidad del objeto de **conjunto de registros** para agregar nuevos registros, utilizar marcadores, usar el método **Find** , usar el desplazamiento, usar la propiedad **index** y realizar actualizaciones por lotes. Para obtener una lista completa de las constantes y sus significados, vea [CursorOptionEnum](../../reference/ado-api/cursoroptionenum.md).  
  
 Aunque el método **Supports** puede devolver **true** para una funcionalidad determinada, no garantiza que el proveedor pueda hacer que la característica esté disponible en todas las circunstancias. El método **Supports** simplemente devuelve si el proveedor puede admitir la funcionalidad especificada, suponiendo que se cumplen ciertas condiciones. Por ejemplo, el método **Supports** puede indicar que un objeto de **conjunto de registros** admite actualizaciones, aunque el cursor se basa en una combinación de varias tablas; algunas columnas de las cuales no son actualizables.