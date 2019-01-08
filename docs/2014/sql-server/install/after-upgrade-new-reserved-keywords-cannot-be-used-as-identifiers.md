---
title: Después de la actualización, las nuevas palabras clave reservadas no se puede utilizar como identificadores | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- keywords [SQL Server], after upgrade
- keywords [SQL Server], reserved
- keywords [SQL Server]
ms.assetid: cb242081-54f8-4273-a8ef-52f3751c25ef
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8db9bcef48b28594187aab34fb0049689d907a47
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376237"
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
  
-   Consulte el objeto utilizando identificadores delimitados. Por ejemplo, la instrucción `CREATE TABLE [MERGE] ([MERGE] int);` usa corchetes para delimitar el nombre de objeto MERGE.  
  
## <a name="external-resources"></a>Recursos externos  
 [Palabras clave reservadas &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reserved-keywords-transact-sql)  
  
 [MERGE &#40;Transact-SQL&#41;](/sql/t-sql/statements/merge-transact-sql)  
  
 [Identificadores delimitados (motor de base de datos)](https://go.microsoft.com/fwlink/?LinkId=112509)  
  
 [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
