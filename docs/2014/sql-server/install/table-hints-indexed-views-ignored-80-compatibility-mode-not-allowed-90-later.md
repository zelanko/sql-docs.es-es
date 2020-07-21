---
title: Las sugerencias de tabla de las definiciones de vistas indizadas se omiten en el modo de compatibilidad 80 y no se permiten en el modo 90 o posterior | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- query hints [SQL Server]
- indexed views [SQL Server], query hints
ms.assetid: 405dfcff-a3a6-4e6d-a53a-ed77bbacdd13
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: cf3cb2b06dc477d93c8fd42312b4835ded42afb4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85035952"
---
# <a name="table-hints-in-indexed-view-definitions-are-ignored-in-80-compatibility-mode-and-are-not-allowed-in-90-mode-or-later"></a>Las sugerencias de tabla en definiciones de vistas indizadas se omiten cuando el modo de compatibilidad es 80, mientras que en los modos 90 y superiores, no se permite su uso
  Las sugerencias de tabla en las definiciones de las vistas indizadas no se permiten en el modo de compatibilidad 90 o superior. Para obtener más información, vea los temas siguientes en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: "Diseñar vistas indizadas", "Crear vistas indizadas" y "Sugerencia de consulta ([!INCLUDE[tsql](../../includes/tsql-md.md)])".  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Las sugerencias de tabla se deben quitar de las definiciones de las vistas indizadas. Independientemente del modo de compatibilidad que se utilice, es recomendable que pruebe la aplicación. Al hacerlo, puede asegurarse de que funciona como es de esperar a la hora de crear, actualizar u obtener acceso a las vistas indizadas, incluyendo el caso en el que las vistas indizadas estén en concordancia con ciertas consultas.  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
