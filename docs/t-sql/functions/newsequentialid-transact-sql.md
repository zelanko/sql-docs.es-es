---
title: NEWSEQUENTIALID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/08/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NEWSEQUENTIALID
- NEWSEQUENTIALID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- NEWSEQUENTIALID function
- GUIDs [SQL Server]
ms.assetid: e06d2cab-f1ff-42f1-8550-6aaec57be36f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6993a36f0c1c67ffcfbb9897bcd36354088c8c5c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="newsequentialid-transact-sql"></a>NEWSEQUENTIALID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Crea un identificador único global (GUID) que es mayor que cualquier GUID generado previamente por esta función en un equipo específico desde que se inició Windows. Después de reiniciar Windows, el GUID se puede volver a iniciar desde un intervalo más bajo, pero sigue siendo globalmente único. Cuando una columna de GUID se utiliza como identificador de fila, el uso de NEWSEQUENTIALID puede ser más rápido que el uso de la función NEWID. La razón es que la función NEWID causa actividad aleatoria y utiliza menos páginas de datos en caché. El uso de NEWSEQUENTIALID también ayuda a rellenar por completo las páginas de datos y de índices.  
  
> [!IMPORTANT]  
>  Si la protección de la privacidad es de particular importancia, no utilice esta función. Es posible estimar el valor del GUID generado a continuación y, por tanto, obtener acceso a los datos asociados con dicho GUID.  
  
 NEWSEQUENTIALID es un contenedor de la función [UuidCreateSequential](http://go.microsoft.com/fwlink/?LinkId=164027) de Windows que tiene aplicado algo de [orden de bytes aleatorio](https://blogs.msdn.microsoft.com/dbrowne/2012/07/03/how-to-generate-sequential-guids-for-sql-server-in-net/).
  
> [!WARNING]  
>  La función UuidCreateSequential tiene dependencias de hardware. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se pueden general clústeres de valores secuenciales cuando las bases de datos (por ejemplo, las bases de datos independientes) se mueven a otros equipos. Cuando se usa Always On en [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)], se pueden generar clústeres de valores secuenciales si la base de datos conmuta por error a otro equipo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
NEWSEQUENTIALID ( )  
```  
  
## <a name="return-type"></a>Tipo devuelto  
 **uniqueidentifier**  
  
## <a name="remarks"></a>Notas  
 NEWSEQUENTIALID() solo se puede usar con restricciones DEFAULT en columnas de tabla de tipo **uniqueidentifier**. Por ejemplo:  
  
```  
CREATE TABLE myTable (ColumnA uniqueidentifier DEFAULT NEWSEQUENTIALID());   
```  
  
 Cuando NEWSEQUENTIALID() se utiliza en expresiones DEFAULT, no se puede combinar con otros operadores escalares. Por ejemplo, no se puede ejecutar lo siguiente:  
  
```  
CREATE TABLE myTable (ColumnA uniqueidentifier DEFAULT dbo.myfunction(NEWSEQUENTIALID()));  
```  
  
 En el ejemplo anterior, `myfunction()` es una función escalar definida por el usuario que acepta y devuelve un valor `uniqueidentifier`.  
  
 No se puede hacer referencia a NEWSEQUENTIALID en las consultas.  
  
 Puede usar NEWSEQUENTIALID para generar GUID a fin de reducir la contención de páginas y E/S aleatoria de nivel hoja en los índices.  
  
 Cada GUID generado utilizando NEWSEQUENTIALID es único en ese equipo. Los GUID generados utilizando NEWSEQUENTIALID solo son únicos en varios equipos si el equipo de origen tiene una tarjeta de red.  
  
## <a name="see-also"></a>Ver también  
 [NEWID &#40;Transact-SQL&#41;](../../t-sql/functions/newid-transact-sql.md)   
 [Operadores de comparación &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)  
  
  
