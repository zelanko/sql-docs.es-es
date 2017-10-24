---
title: Update() (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATE()_TSQL
- UPDATE()
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], UPDATE function
- testing column updates
- UPDATE function
- UPDATE() function
- detecting changes
- columns [SQL Server], change detection
- UPDATE statement [SQL Server], UPDATE function
- verifying column updates
- checking column updates
ms.assetid: 8e3be25b-2e3b-4d1f-a610-dcbbd8d72084
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 644848af581b0db5a26b9958db4660b4cab66163
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="update---trigger-functions-transact-sql"></a>UPDATE - funciones de desencadenador (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve un valor booleano que indica si se intentó utilizar INSERT o UPDATE en una columna especificada de una tabla o vista. UPDATE() se utiliza en cualquier lugar del cuerpo de un desencadenador INSERT o UPDATE de [!INCLUDE[tsql](../../includes/tsql-md.md)] para probar si el desencadenador debe ejecutar ciertas acciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
UPDATE ( column )   
```  
  
## <a name="arguments"></a>Argumentos  
 *columna*  
 Es el nombre de la columna que se va a probar para una acción INSERT o UPDATE. Debido a que el nombre de la tabla se especifica en la cláusula ON del desencadenador, no lo incluya antes del nombre de la columna. La columna puede tener cualquier [tipo de datos](../../t-sql/data-types/data-types-transact-sql.md) admite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No obstante, no se pueden utilizar columnas calculadas en este contexto.  
  
## <a name="return-types"></a>Tipos devueltos  
 Boolean  
  
## <a name="remarks"></a>Comentarios  
 UPDATE() devuelve TRUE independientemente de si un intento de INSERT o UPDATE tiene éxito.  
  
 Para probar una acción INSERT o UPDATE para más de una columna, especifique una actualización independiente (*columna*) cláusula después de la primera de ellas. También puede probar acciones INSERT o UPDATE en varias columnas con COLUMNS_UPDATED, que devuelve un patrón de bits que indica las columnas que se insertaron o se actualizaron.  
  
 IF UPDATE devuelve el valor TRUE en las acciones INSERT porque en las columnas se insertaron valores explícitos o implícitos (NULL).  
  
> [!NOTE]  
>  IF UPDATE (*columna*n) cláusula funciona igual que un IF Si... ELSE o WHILE (cláusula) y puede utilizar BEGIN... Bloque final. Para obtener más información, vea [lenguaje de Control de flujo &#40; Transact-SQL &#41; ](~/t-sql/language-elements/control-of-flow.md).  
  
 UPDATE (*columna*) puede usarse en cualquier lugar dentro del cuerpo de un [!INCLUDE[tsql](../../includes/tsql-md.md)] desencadenador.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea un desencadenador que imprime un mensaje para el cliente si alguien intenta actualizar las columnas `StateProvinceID` o `PostalCode` de la tabla `Address`.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
      WHERE name = 'reminder' AND type = 'TR')  
   DROP TRIGGER Person.reminder;  
GO  
CREATE TRIGGER reminder  
ON Person.Address  
AFTER UPDATE   
AS   
IF ( UPDATE (StateProvinceID) OR UPDATE (PostalCode) )  
BEGIN  
RAISERROR (50009, 16, 10)  
END;  
GO  
-- Test the trigger.  
UPDATE Person.Address  
SET PostalCode = 99999  
WHERE PostalCode = '12345';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [COLUMNS_UPDATED &#40; Transact-SQL &#41;](../../t-sql/functions/columns-updated-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  

