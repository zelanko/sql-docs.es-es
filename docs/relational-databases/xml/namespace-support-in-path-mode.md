---
title: Compatibilidad con elementos de espacio de nombres en el modo PATH | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PATH FOR XML mode, namespace support
- namespaces [XML in SQL Server]
ms.assetid: 5f128ea2-0ceb-4b23-bce7-c8b3fd615466
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 733d1a16e352403ca55053ea45a464591e92d7fb
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

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
 [Usar el modo PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
