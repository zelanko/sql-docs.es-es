---
title: Buscar texto con caracteres comodín
description: Obtenga información sobre cómo usar caracteres comodín en el campo "Buscar" de un cuadro de diálogo Buscar y reemplazar para especificar un patrón con el que comparar.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- vswildcardsbuilder
helpviewer_keywords:
- searches [SQL Server Management Studio], wildcards
- Query Editor [SQL Server Management Studio], wildcard searches
- wildcard options [SQL Server Management Studio]
ms.assetid: 449600f8-cc87-4b3f-878a-59c158a88a40
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c8e2766939038879d92de0f8f73b5c2eab38f45d
ms.sourcegitcommit: d855def79af642233cbc3c5909bc7dfe04c4aa23
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2020
ms.locfileid: "87122796"
---
# <a name="search-text-with-wildcards"></a>Buscar texto con caracteres comodín
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Las expresiones siguientes pueden reemplazar a caracteres o dígitos en el campo **Buscar** del cuadro de diálogo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Buscar y reemplazar**.  
  
#### <a name="to-search-using-wildcards"></a>Para buscar mediante caracteres comodín  
  
1.  Para habilitar el uso de caracteres comodín en el campo **Buscar** en operaciones de **Búsqueda rápida**, **Buscar en archivos**, **Reemplazo rápido** o **Reemplazar en archivos** , active la opción **Usar** de **Opciones de búsqueda**y, a continuación, elija Caracteres comodín.  
  
2.  El botón triangular de la **Lista de referencia** situado junto al campo **Buscar** se activa. Haga clic en este botón para obtener una lista de los caracteres comodín disponibles. Al elegir alguno de los elementos del **Generador de expresiones**, éste se inserta en la cadena **Buscar** .  
  
 En la tabla siguiente se describen los caracteres comodín disponibles en la **Lista de referencias**.  
  
|Expression|Sintaxis|Descripción|  
|----------------|------------|-----------------|  
|Un carácter cualquiera|?|Coincidencia con cualquier carácter individual.|  
|Un dígito cualquiera|#|Coincidencia con cualquier dígito individual. Por ejemplo, 7# devuelve números que incluyen un 7 seguido de otro número, como 71, pero no 17.|  
|Un carácter cualquiera no perteneciente al conjunto|[! ]|Coincidencia con cualquier carácter que no se haya especificado en el juego de caracteres.|  
|Cero o más caracteres cualesquiera|*|Coincidencia con uno o más caracteres. Por ejemplo, new* devuelve cualquier texto que incluya "new", como newfile.txt.|  
|Un carácter cualquiera del conjunto|[ ]|Coincidencia con cualquier carácter especificado en el juego de caracteres.|  
  
## <a name="see-also"></a>Consulte también  
 [Buscar y reemplazar](../../relational-databases/scripting/search-and-replace.md)   
 [Buscar texto mediante expresiones regulares](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
