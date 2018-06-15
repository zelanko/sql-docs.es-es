---
title: TRIGGER_NESTLEVEL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- TRIGGER_NESTLEVEL
- TRIGGER_NESTLEVEL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- triggers [SQL Server], number executed
- number of triggers
- TRIGGER_NESTLEVEL function
ms.assetid: 6a33e74a-0cf9-4ae1-a1e4-4a137a3ea39d
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 86b31446821fae2ee03449c1e636f6624bee931b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33061822"
---
# <a name="triggernestlevel-transact-sql"></a>TRIGGER_NESTLEVEL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el número de desencadenadores que se han ejecutado para la instrucción que ha activado el desencadenador. TRIGGER_NESTLEVEL se utiliza en desencadenadores DML y DDL para determinar el nivel actual de anidamiento.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TRIGGER_NESTLEVEL ( [ object_id ] , [ 'trigger_type' ] , [ 'trigger_event_category' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_id*  
 Es el Id. de objeto de un desencadenador. Si se especifica *object_id*, se devuelve el número de veces que el desencadenador especificado se ha ejecutado para la instrucción. Si no se especifica *object_id*, se devuelve el número de veces que se han ejecutado todos los desencadenadores para la instrucción.  
  
 **'** *trigger_type* **'**  
 Especifica si se aplica TRIGGER_NESTLEVEL a los desencadenadores AFTER o a los desencadenadores INSTEAD OF. Especifique **AFTER** para desencadenadores AFTER. Especifique **IOT** para desencadenadores INSTEAD OF. Si se especifica *trigger_type*, *trigger_event_category* también debe especificarse.  
  
 **'** *trigger_event_category* **'**  
 Especifica si se aplica TRIGGER_NESTLEVEL a desencadenadores DML o DDL. Especifique **DML** para desencadenadores DML. Especifique **DDL** para desencadenadores DDL. Si se especifica *trigger_event_category*, *trigger_type* también debe especificarse. Tenga en cuenta que solo se puede especificar **AFTER** con **DDL**, ya que los desencadenadores DDL solo pueden ser desencadenadores AFTER.  
  
## <a name="remarks"></a>Notas  
 Cuando no se especifica ningún parámetro, TRIGGER_NESTLEVEL devuelve el número total de desencadenadores de la pila de llamadas. Esto incluye el propio desencadenador. La omisión de los parámetros puede darse cuando un desencadenador ejecuta comandos que causan la activación de otro desencadenador o de una serie de desencadenadores.  
  
 Para devolver el número total de desencadenadores en la pila de llamadas para un tipo de desencadenador y una categoría de eventos determinados, especifique *object_id* = 0.  
  
 TRIGGER_NESTLEVEL devuelve 0 si se ejecuta fuera de un desencadenador y cualquier parámetro es distinto de NULL.  
  
 Cuando algunos parámetros se especifican explícitamente como NULL, el valor de NULL se devuelve independientemente de si TRIGGER_NESTLEVEL se utilizó dentro o fuera de un desencadenador.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-testing-the-nesting-level-of-a-specific-dml-trigger"></a>A. Probar el nivel de anidamiento de un desencadenador DML específico  
  
```  
IF ( (SELECT TRIGGER_NESTLEVEL( OBJECT_ID('xyz') , 'AFTER' , 'DML' ) ) > 5 )  
   RAISERROR('Trigger xyz nested more than 5 levels.',16,-1)  
```  
  
### <a name="b-testing-the-nesting-level-of-a-specific-ddl-trigger"></a>B. Probar el nivel de anidamiento de un desencadenador DDL específico  
  
```  
IF ( ( SELECT TRIGGER_NESTLEVEL ( ( SELECT object_id FROM sys.triggers  
WHERE name = 'abc' ), 'AFTER' , 'DDL' ) ) > 5 )  
   RAISERROR ('Trigger abc nested more than 5 levels.',16,-1)  
```  
  
### <a name="c-testing-the-nesting-level-of-all-triggers-executed"></a>C. Probar el nivel de anidamiento de todos los desencadenadores ejecutados  
  
```  
IF ( (SELECT trigger_nestlevel() ) > 5 )  
   RAISERROR  
      ('This statement nested over 5 levels of triggers.',16,-1)  
```  
  
## <a name="see-also"></a>Ver también  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
