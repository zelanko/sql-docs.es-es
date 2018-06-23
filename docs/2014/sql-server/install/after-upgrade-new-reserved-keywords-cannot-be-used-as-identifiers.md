---
title: Después de la actualización, las nuevas palabras clave reservadas no se pueden utilizar como identificadores | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- keywords [SQL Server], after upgrade
- keywords [SQL Server], reserved
- keywords [SQL Server]
ms.assetid: cb242081-54f8-4273-a8ef-52f3751c25ef
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 177c36aaeca8e6cc9d84aae21e1f99fe0bb96867
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199062"
---
# <a name="after-upgrade-new-reserved-keywords-cannot-be-used-as-identifiers"></a>Después de la actualización, las nuevas palabras clave reservadas no se pueden utilizar como identificadores
  El Asesor de actualizaciones detectó el uso de palabras que son palabras clave reservadas. Una palabra clave reservada no se puede utilizar como identificador o nombre de objeto a menos que el nombre se delimite.  
  
## <a name="component"></a>Componente  
 Motor de base de datos  
  
## <a name="description"></a>Descripción  
 En el nivel de compatibilidad 90 o inferior, las palabras siguientes no son palabras clave reservadas y se pueden utilizar como identificadores o nombres de objeto en scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)]. En el nivel de compatibilidad 100, estas palabras son palabras clave totalmente reservadas y no se deben utilizar como identificadores o nombres de objeto.  
  
-   EXTERNAL  
  
-   MERGE  
  
-   PIVOT  
  
-   REVERT  
  
-   STOPLIST  
  
-   TABLESAMPLE  
  
-   UNPIVOT  
  
## <a name="corrective-action"></a>Acción correctora  
 Recomendamos que cambie el nombre del objeto. Si no es posible antes de actualizar, utilice uno de los métodos siguientes hasta que se pueda cambiar el nombre:  
  
-   Conserve el valor de nivel de compatibilidad de la base de datos en 90 o inferior.  
  
-   Consulte el objeto utilizando identificadores delimitados. Por ejemplo, la instrucción `CREATE TABLE [MERGE] ([MERGE] int);` utiliza corchetes para delimitar el nombre de objeto MERGE.  
  
## <a name="external-resources"></a>Recursos externos  
 [Palabras clave reservadas &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reserved-keywords-transact-sql)  
  
 [MERGE &#40;Transact-SQL&#41;](/sql/t-sql/statements/merge-transact-sql)  
  
 [Identificadores delimitados (motor de base de datos)](http://go.microsoft.com/fwlink/?LinkId=112509)  
  
 [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
