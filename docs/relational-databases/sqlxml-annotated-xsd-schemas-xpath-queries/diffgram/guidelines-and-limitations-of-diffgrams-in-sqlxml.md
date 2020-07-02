---
title: Instrucciones y limitaciones de DiffGrams en SQLXML
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
ms.openlocfilehash: 113090c317e88d3e9a7e7db2bfcb7d4d14b4ea1f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85650072"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>Instrucciones y limitaciones de DiffGrams en SQLXML
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Recuerde lo siguiente al usar DiffGrams con SQLXML 4.0:  
  
-   Los tipos de objetos binarios grandes (BLOB) como **text/ntext** e imágenes no se deben usar en el **\<diffgr:before>** bloque de al trabajar con DiffGrams, porque esto los incluiría para su uso en el control de simultaneidad. Esto puede producir problemas con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debido a las limitaciones en la comparación para los tipos BLOB. Por ejemplo, la palabra clave LIKE se usa en la cláusula WHERE para comparar entre las columnas del tipo de datos **Text** ; sin embargo, se producirá un error en las comparaciones en el caso de los tipos BLOB donde el tamaño de los datos es mayor que 8 k.  
  
-   Los caracteres especiales en los datos **ntext** pueden producir problemas con SQLXML 4,0 debido a las limitaciones de la comparación de los tipos de BLOB. Por ejemplo, el uso de "[Serializable]" en el **\<diffgr:before>** bloque de un DiffGram cuando se usa en la comprobación de simultaneidad de una columna de tipo **ntext** producirá un error con la siguiente descripción del error SQLOLEDB:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
