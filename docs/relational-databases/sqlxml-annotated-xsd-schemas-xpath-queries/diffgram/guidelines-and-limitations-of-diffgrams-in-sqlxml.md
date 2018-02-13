---
title: Instrucciones y limitaciones de DiffGrams en SQLXML | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2af871b240d318aaa027402a52a9c31498521b99
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>Instrucciones y limitaciones de DiffGrams en SQLXML
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Recuerde lo siguiente al usar DiffGrams con SQLXML 4.0:  
  
-   Tipos de objeto binario grande (BLOB) como **texto/ntext** y las imágenes no deben usarse en el  **\<diffgr: antes de >** bloquear al trabajar con DiffGrams, porque esto los incluiría para su uso en control de simultaneidad. Esto puede producir problemas con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debido a las limitaciones en la comparación para los tipos BLOB. Por ejemplo, se utiliza la palabra clave LIKE en la cláusula WHERE para comparar entre las columnas de la **texto** tipo de datos; sin embargo, las comparaciones se producirá un error en el caso de los tipos BLOB donde el tamaño de los datos es mayor que 8 KB.  
  
-   Caracteres especiales en **ntext** datos pueden causar problemas con SQLXML 4.0 debido a las limitaciones en la comparación para los tipos de BLOB. Por ejemplo, el uso de "[Serializable]" en la  **\<diffgr: antes de >** bloque de un DiffGram cuando se utiliza en la comprobación de simultaneidad de una columna de **ntext** se producirá un error de tipo con SQLOLEDB siguiente Descripción del error:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
