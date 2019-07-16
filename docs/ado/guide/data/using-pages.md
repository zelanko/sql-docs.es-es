---
title: Utilizando páginas | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923512"
---
# <a name="using-pages"></a>Usando las páginas
Use la **PageCount** propiedad para determinar cuántas páginas de datos están en el **Recordset** objeto. *Páginas* son grupos de registros cuyo tamaño es igual a la **PageSize** configuración de la propiedad. Incluso si la última página está incompleta porque hay menos registros que el **PageSize** valor, cuenta como una página adicional en el **PageCount** valor. Si el **Recordset** objeto no admite esta propiedad, **PageCount** será -1 para indicar que el **PageCount** no es posible determinar.  
  
 Use la **PageSize** propiedad para determinar cuántos registros componen una página lógica de datos. Establecer un tamaño de página le permite usar el **AbsolutePage** propiedad para desplazarse al primer registro de una página determinada. Esto es útil en escenarios de servidor Web cuando desea permitir al usuario desplazarse por los datos, ve un cierto número de registros a la vez.  
  
 Esta propiedad puede establecerse en cualquier momento y su valor se usará para calcular la ubicación del primer registro de una página determinada.  
  
 Use la **AbsolutePage** propiedad para identificar el número de página en el que se encuentra el registro actual. Nuevamente, el proveedor debe admitir la funcionalidad adecuada para esta propiedad esté disponible.  
  
 **AbsolutePage** está basado en 1 y es igual a 1 cuando el registro actual es el primer registro en el **Recordset**. Establezca esta propiedad para desplazarse al primer registro de una página determinada. Obtener el número total de páginas de la **PageCount** propiedad.
