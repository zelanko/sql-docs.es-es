---
title: MSSQLSERVER_1505 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1505 (Database Engine error)
ms.assetid: ef4df75d-0f36-4c8b-b36c-e427f65f91ca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec0a5700df76134eab8a4fe2278820691dad509e
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359317"
---
# <a name="mssqlserver1505"></a>MSSQLSERVER_1505
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1505|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DUP_KEY|  
|Texto del mensaje|La instrucción CREATE UNIQUE INDEX terminó porque se encontró una clave duplicada para el nombre de objeto '%.*ls' y el nombre de índice '%.*ls'. El valor de la clave duplicada es '%.\*ls'.  El valor de la clave duplicada es %ls.|  
  
## <a name="explanation"></a>Explicación  
 Este error se produce cuando se intenta crear un índice único y más de una fila de la tabla contiene el valor duplicado especificado. Un índice único se crea cuando se crea un índice y se especifica la palabra clave UNIQUE, o cuando se crea una restricción UNIQUE. La tabla no puede contener filas que tengan valores duplicados en las columnas definidas en el índice o la restricción.  
  
 Considere los datos de la tabla **Employee** siguiente:  
  
|LastName|FirstName|JobTitle|HireDate|  
|--------------|---------------|--------------|--------------|  
|Walters|Rob|Senior Tool Designer|2004-11-19|  
|Brown|Kevin|Marketing Assistant|NULL|  
|Brown|Jo|Design Engineer|NULL|  
|Walters|Rob|Tool Designer|2001-08-09|  
  
 No se puede crear un índice único en las combinaciones de columnas **LastName** o **LastName**, **FirstName** debido a la presencia de valores duplicados en las filas.  
  
 Menos obvia es la posibilidad de una infracción de unicidad en la columna **HireDate**. A efectos de índices, los valores NULL son comparables a igual. Por lo tanto, no se puede crear un índice o una restricción únicos si los valores de clave son NULL en más de una fila. Dados los datos anteriores, no se puede crear un índice único en las combinaciones de columnas **HireDate** o **LastName**, **HireDate**.  
  
 El mensaje de error 1505 devuelve la primera fila que infringe la restricción de unicidad. Puede haber otras filas duplicadas en la tabla. Para encontrar todas las filas duplicadas, consulte la tabla especificada y utilice las cláusulas GROUP BY y HAVING para notificar las filas duplicadas. Por ejemplo, la siguiente consulta devuelve las filas de la tabla **Employee** que tengan nombres y apellidos duplicados.  
  
 SELECT LastName, FirstName, count(*) FROM dbo.Employee GROUP BY LastName, FirstName HAVING count(\*) > 1;  
  
## <a name="user-action"></a>Acción del usuario  
 Considere las soluciones siguientes.  
  
-   Agregar o quitar columnas de la definición de restricción o de índice para crear un índice compuesto único. En el ejemplo anterior, puede que al agregar una columna **MiddleName** a la definición de índice o restricción se resuelva el problema de duplicación.  
  
-   Seleccionar columnas que se hayan definido como NOT NULL al elegir columnas para un índice o una restricción únicos. Esto elimina la posibilidad de que se produzca una infracción de unicidad cuando más de una fila contenga NULL en los valores de clave.  
  
-   Si los valores duplicados son consecuencia de errores de entrada de datos, corregir manualmente los datos y crear el índice o la restricción. Para obtener información acerca de cómo quitar filas duplicadas en una tabla, vea el artículo 139444 de Knowledge Base: [Cómo quitar filas duplicadas de una tabla en SQL Server](https://support.microsoft.com/kb/139444).  
  
## <a name="see-also"></a>Vea también  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [Crear índices únicos](../indexes/indexes.md)   
 [Crear restricciones UNIQUE](../tables/create-unique-constraints.md)  
  
  
