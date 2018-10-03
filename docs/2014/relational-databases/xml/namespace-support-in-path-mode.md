---
title: Compatibilidad con elementos de espacio de nombres en el modo PATH | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- PATH FOR XML mode, namespace support
- namespaces [XML in SQL Server]
ms.assetid: 5f128ea2-0ceb-4b23-bce7-c8b3fd615466
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1d0c123a3cf77a04ee42f66ba0faf5bd995714c7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219875"
---
# <a name="namespace-support-in-path-mode"></a>Compatibilidad con elementos de espacio de nombres en el modo PATH
  Se incluye la compatibilidad con elementos de espacio de nombres en el modo PATH mediante WITH NAMESPACES. Por ejemplo, la consulta siguiente muestra la sintaxis WITH NAMESPACES para declarar un espacio de nombres ("a:") que se puede usar a continuación en la instrucción SELECT posterior:  
  
```  
WITH XMLNAMESPACES('a' as a)  
SELECT 1 as 'a:b'  
FOR XML PATH  
```  
  
## <a name="examples"></a>Ejemplos  
 Estas muestras ilustran la utilización del modo PATH en la creación de XML a partir de una consulta SELECT. Muchas de estas consultas se especifican usando los documentos XML de instrucciones de fabricación de bicicletas almacenados en la columna Instructions de la tabla ProductModel.  
  
## <a name="see-also"></a>Vea también  
 [Usar el modo PATH con FOR XML](use-path-mode-with-for-xml.md)  
  
  
