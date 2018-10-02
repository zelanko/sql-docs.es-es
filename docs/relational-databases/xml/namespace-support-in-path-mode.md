---
title: Compatibilidad con elementos de espacio de nombres en el modo PATH | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 19c932a3927e71208e4b1c82c8c3bce4cbadfd8b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47747043"
---
# <a name="namespace-support-in-path-mode"></a>Compatibilidad con elementos de espacio de nombres en el modo PATH
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Se incluye la compatibilidad con elementos de espacio de nombres en el modo PATH mediante WITH NAMESPACES. Por ejemplo, la consulta siguiente muestra la sintaxis WITH NAMESPACES para declarar un espacio de nombres ("a:") que se puede usar a continuación en la instrucción SELECT posterior:  
  
```  
WITH XMLNAMESPACES('a' as a)  
SELECT 1 as 'a:b'  
FOR XML PATH  
```  
  
## <a name="examples"></a>Ejemplos  
 Estas muestras ilustran la utilización del modo PATH en la creación de XML a partir de una consulta SELECT. Muchas de estas consultas se especifican usando los documentos XML de instrucciones de fabricación de bicicletas almacenados en la columna Instructions de la tabla ProductModel.  
  
## <a name="see-also"></a>Ver también  
 [Usar el modo PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
