---
title: Formatos de datos para importación o exportación masivas (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], choosing
- bulk importing [SQL Server], data formats
ms.assetid: 73fe6741-9437-4b26-b030-28b863e74399
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c43cb42cffba31f20b0e9717204f5475b5bb156d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66012082"
---
# <a name="data-formats-for-bulk-import-or-bulk-export-sql-server"></a>Formatos de datos para importación o exportación masivas (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede aceptar datos en formato de datos de caracteres o binarios nativos. Use el formato de caracteres al mover datos entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y otra aplicación (como [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel) u otro servidor de bases de datos (como Oracle o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Solo puede usar el formato nativo al transferir datos entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **En este tema:**  
  
-   [Formatos de datos para importación o exportación masivas](#ComponentsAndConcepts)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="ComponentsAndConcepts"></a> Formatos de datos para importación o exportación masivas  
 En la siguiente tabla se indica el formato de datos que resulta adecuado, de forma general, para usar dependiendo del modo en que los datos estén representados y el origen o el destino de la operación.  
  
|Operación|Nativa|Unicode nativo|Carácter|carácter Unicode|  
|---------------|------------|--------------------|---------------|-----------------------|  
|Transferencias masivas de datos entre varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un archivo de datos que no contenga caracteres del juego de caracteres de doble byte (DBCS). A menos que se use un archivo de formato, estas tablas deben definirse de forma idéntica.|Sí<sup>1</sup>|-|-|-|  
|Para las columnas `sql_variant`, es mejor el uso del formato de datos nativo, ya que preserva los metadatos de cada valor `sql_variant`, a diferencia de los formatos de caracteres o Unicode.|Sí|-|-|-|  
|Transferencias masivas de datos entre varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un archivo de datos que contenga caracteres DBCS o extendidos.|-|Sí|-|-|  
|Importación masiva de datos desde un archivo de texto generado por otro programa.|-|-|Sí|-|  
|Exportación masiva de datos a un archivo de texto para usarlo en otro programa.|-|-|Sí|-|  
|Transferencias masivas de datos entre varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un archivo de datos que contenga datos Unicode y no contenga caracteres DBCS o extendidos.|-|-|-|Sí|  
  
 <sup>1</sup> método más rápido para la exportación masiva de datos desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se usa **BCP**.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Especificar formatos de datos por razones de compatibilidad mediante bcp &#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)  
  
  
