---
title: Usar páginas | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- PageSize property [ADO]
- pages [ADO]
- Recordset object [ADO]
- AbsolutePage property [ADO]
- PageCount property [ADO]
ms.assetid: 442b08c5-ccc7-4192-a1cc-22f250867782
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0d697fa5b411d9000c03a700f6b4fe0e4b39aa5e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923512"
---
# <a name="using-pages"></a>Usando las páginas
Use la propiedad **PageCount** para determinar el número de páginas de datos que se encuentran en el objeto de **conjunto de registros** . *Las páginas* son grupos de registros cuyo tamaño es igual al valor de la propiedad **pageSize** . Incluso si la última página está incompleta porque hay menos registros que el valor de **pageSize** , cuenta como página adicional en el valor de **PageCount** . Si el objeto de **conjunto de registros** no admite esta propiedad, **PageCount** será-1 para indicar que **PageCount** es Indeterminista.  
  
 Utilice la propiedad **pageSize** para determinar el número de registros que conforman una página de datos lógica. Establecer un tamaño de página permite utilizar la propiedad **AbsolutePage** para desplace al primer registro de una página determinada. Esto resulta útil en escenarios Web-Server cuando desea permitir que el usuario recorra en páginas los datos, viendo un número determinado de registros a la vez.  
  
 Esta propiedad se puede establecer en cualquier momento y su valor se usará para calcular la ubicación del primer registro de una página determinada.  
  
 Utilice la propiedad **AbsolutePage** para identificar el número de página en el que se encuentra el registro actual. De nuevo, el proveedor debe admitir la funcionalidad adecuada para que esta propiedad esté disponible.  
  
 **AbsolutePage** es de base 1 y es igual a 1 cuando el registro actual es el primer registro del **conjunto de registros**. Establezca esta propiedad para pasar al primer registro de una página determinada. Obtenga el número total de páginas de la propiedad **PageCount** .
