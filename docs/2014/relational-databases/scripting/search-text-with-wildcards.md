---
title: Buscar texto con caracteres comodín | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- vswildcardsbuilder
helpviewer_keywords:
- searches [SQL Server Management Studio], wildcards
- Query Editor [SQL Server Management Studio], wildcard searches
- wildcard options [SQL Server Management Studio]
ms.assetid: 449600f8-cc87-4b3f-878a-59c158a88a40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5c3efcef4eade7c6ad2b5a5d52a1fa26a4c4ffd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090241"
---
# <a name="search-text-with-wildcards"></a>Buscar texto con caracteres comodín
  Las expresiones siguientes pueden reemplazar a caracteres o dígitos en el campo **Buscar** del cuadro de diálogo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **de** .  
  
#### <a name="to-search-using-wildcards"></a>Para buscar mediante caracteres comodín  
  
1.  Para habilitar el uso de caracteres comodín en el campo **Buscar** en operaciones de **Búsqueda rápida**, **Buscar en archivos**, **Reemplazo rápido** o **Reemplazar en archivos** , active la opción **Usar** de **Opciones de búsqueda**y, a continuación, elija Caracteres comodín.  
  
2.  El botón triangular de la **Lista de referencia** situado junto al campo **Buscar** se activa. Haga clic en este botón para obtener una lista de los caracteres comodín disponibles. Al elegir alguno de los elementos del **Generador de expresiones**, éste se inserta en la cadena **Buscar** .  
  
 En la tabla siguiente se describen los caracteres comodín disponibles en la **Lista de referencias**.  
  
|Expresión|Sintaxis|Descripción|  
|----------------|------------|-----------------|  
|Un carácter cualquiera|?|Coincidencia con cualquier carácter individual.|  
|Un dígito cualquiera|#|Coincidencia con cualquier dígito individual. Por ejemplo, 7# devuelve números que incluyen un 7 seguido de otro número, como 71, pero no 17.|  
|Un carácter cualquiera no perteneciente al conjunto|[! ]|Coincidencia con cualquier carácter que no se haya especificado en el juego de caracteres.|  
|Cero o más caracteres cualesquiera|*|Coincidencia con uno o más caracteres. Por ejemplo, new* devuelve cualquier texto que incluya "new", como newfile.txt.|  
|Un carácter cualquiera del conjunto|[ ]|Coincidencia con cualquier carácter especificado en el juego de caracteres.|  
  
## <a name="see-also"></a>Vea también  
 [Buscar y reemplazar](search-and-replace.md)   
 [Buscar texto mediante expresiones regulares](search-text-with-regular-expressions.md)  
