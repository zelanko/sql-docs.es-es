---
title: Actualizar expresiones XPath OPENXML para quitar funciones no admitidas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- OPENXML queries
ms.assetid: b459abaf-8787-4b65-9231-ae30e5469fd0
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec0edb2e72143fd41709355a3e9cc338544289a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091692"
---
# <a name="update-openxml-xpath-expressions-to-remove-unsupported-functions"></a>Actualizar expresiones XPath OPENXML para quitar funciones no compatibles
  El Asesor de actualizaciones ha detectado que se está utilizando la funcionalidad de XPath. Es posible que tenga problemas con los cambios realizados en la funcionalidad de XPath para las características de OPENXML tras la actualización.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Ahora, MSXML 3.0 es el motor subyacente que se utiliza para procesar expresiones XPath usadas en consultas OPENXML. MSXML 3.0 tiene un motor XPath 1.0 más estricto en el que se ha quitado la compatibilidad con las siguientes funciones:  
  
-   format-number()  
  
-   formatNumber()  
  
-   current()  
  
-   element-available()  
  
-   function-available()  
  
-   system-property()  
  
## <a name="corrective-action"></a>Acción correctora  
 En el caso de format-number() y formatNumber(), puede utilizar [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para las demás funciones no compatibles que aparecen más arriba, no existen soluciones directas.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
