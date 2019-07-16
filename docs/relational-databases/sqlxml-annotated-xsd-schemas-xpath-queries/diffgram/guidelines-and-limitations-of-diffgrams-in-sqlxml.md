---
title: Instrucciones y limitaciones de DiffGrams en SQLXML | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 64f19e8d7b5e67311f21b79c6f36572d9b2240d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073449"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>Instrucciones y limitaciones de DiffGrams en SQLXML
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Recuerde lo siguiente al usar DiffGrams con SQLXML 4.0:  
  
-   Tipos de objeto binario grande (BLOB) como **texto/ntext** y no se deben usar imágenes en el  **\<diffgr: antes de >** bloquear al trabajar con DiffGrams, porque esto los incluiría para su uso en control de simultaneidad. Esto puede producir problemas con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debido a las limitaciones en la comparación para los tipos BLOB. Por ejemplo, la palabra clave LIKE se usa en la cláusula WHERE para comparar entre las columnas de la **texto** de tipo de datos; sin embargo, las comparaciones se producirá un error en el caso de los tipos BLOB donde el tamaño de los datos es mayor que 8 KB.  
  
-   Caracteres especiales en **ntext** datos pueden causar problemas con SQLXML 4.0 debido a las limitaciones en la comparación para los tipos de BLOB. Por ejemplo, el uso de "[Serializable]" en el  **\<diffgr: antes de >** bloque de un DiffGram cuando se utiliza en la comprobación de simultaneidad de una columna de **ntext** se producirá un error de tipo con SQLOLEDB siguiente Descripción del error:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
