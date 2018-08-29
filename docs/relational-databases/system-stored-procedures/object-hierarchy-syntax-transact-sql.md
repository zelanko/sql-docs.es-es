---
title: Objeto de la sintaxis de jerarquía (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], hierarchy syntax
ms.assetid: 7ed8df86-9fd2-4e09-96bc-5381fec85f65
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 979d67b930d95817c0c27f671885c9b5fd9fb0d4
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43032543"
---
# <a name="object-hierarchy-syntax-transact-sql"></a>Sintaxis de jerarquía de objetos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  El *propertyname* parámetro de sp_OAGetProperty y sp_OASetProperty y *methodname* parámetro de sp_OAMethod admiten una sintaxis de jerarquía de objetos similar al de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Cuando se utiliza esta sintaxis especial, estos parámetros tienen la forma general siguiente:  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
'TraversedObject.PropertyOrMethod'  
```  
  
## <a name="arguments"></a>Argumentos  
 *TraversedObject*  
 Es un objeto OLE en la jerarquía bajo el *objecttoken* especificado en el procedimiento almacenado. Utilice la sintaxis de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para especificar un conjunto de colecciones, propiedades de objetos y métodos que devuelven objetos. Cada especificador de objeto del conjunto debe estar separado con un punto .  
  
 Un elemento del conjunto puede ser el nombre de una colección. Utilice esta sintaxis para especificar una colección:  
  
 Colección ("*elemento*")  
  
 Las comillas dobles (") son necesarias. No se acepta la sintaxis de signo de admiración de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] (!) para las recopilaciones.  
  
 *PropertyOrMethod*  
 Es el nombre de una propiedad o método de la *TraversedObject*.  
  
 Para especificar todos los índices o parámetros de métodos mediante los parámetros sp_OAGetProperty, sp_OASetProperty o sp_OAMethod  (incluida la compatibilidad con los parámetros de resultado de sp_OAMethod), utilice esta sintaxis:  
  
 *PropertyOrMethod*  
  
 Para especificar todos los índices o parámetros de métodos entre paréntesis (para que se pasen por alto todos los índices o parámetros de métodos de sp_OAGetProperty, sp_OASetProperty o sp_OAMethod) utilice esta sintaxis:  
  
 *PropertyOrMethod*([ *ParameterName*: =] "*parámetro*" [,...])  
  
 Las comillas dobles (") son necesarias. Todos los parámetros con nombre deben especificarse después de especificar todos los parámetros de posición.  
  
## <a name="remarks"></a>Notas  
 Si *TraversedObject* no se especifica, *PropertyOrMethod* es necesario.  
  
 Si *PropertyOrMethod* no se especifica, el *TraversedObject* se devuelve como un parámetro de salida de token de objeto del procedimiento almacenado de automatización OLE. Si *PropertyOrMethod* se especifica, la propiedad o método de la *TraversedObject* se llama a, y el valor de propiedad o valor devuelto del método se devuelve como un parámetro de salida de la automatización OLE procedimiento almacenado.  
  
 Si algún elemento en el *TraversedObject* lista no devuelve un objeto OLE, se produce un error.  
  
 Para obtener más información acerca de la sintaxis de objetos OLE de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], vea la documentación de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].  
  
 Para obtener más información sobre los códigos de retorno HRESULT, vea [sp_OACreate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
 Los siguientes son ejemplos de sintaxis de jerarquía de objetos que utilizan un objeto SQLServer de SQL-DMO.  
  
```  
-- Get the AdventureWorks2012 Person.Address Table object.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address")',  
   @table OUT  
  
-- Get the Rows property of the AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").Rows',  
   @rows OUT  
  
-- Call the CheckTable method to validate the   
-- AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAMethod @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").CheckTable',  
   @checkoutput OUT  
```  
  
## <a name="see-also"></a>Vea también  
 [Script de ejemplo de automatización OLE](../../relational-databases/stored-procedures/ole-automation-sample-script.md)   
 [Procedimientos almacenados de automatización OLE &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
  
