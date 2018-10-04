---
title: Sugerencias de tabla en indizan la vista de definiciones se omiten en el modo de compatibilidad 80 y no se permiten en el modo 90 o posterior | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- query hints [SQL Server]
- indexed views [SQL Server], query hints
ms.assetid: 405dfcff-a3a6-4e6d-a53a-ed77bbacdd13
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bf4f8e5c3ea23b1ab52199c884c2980bf52bc983
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48160055"
---
# <a name="table-hints-in-indexed-view-definitions-are-ignored-in-80-compatibility-mode-and-are-not-allowed-in-90-mode-or-later"></a>Las sugerencias de tabla en definiciones de vistas indizadas se omiten cuando el modo de compatibilidad es 80, mientras que en los modos 90 y superiores, no se permite su uso
  Las sugerencias de tabla en las definiciones de las vistas indizadas no se permiten en el modo de compatibilidad 90 o superior. Para obtener más información, vea los temas siguientes en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: "Diseñar vistas indizadas", "Crear vistas indizadas" y "Sugerencia de consulta ([!INCLUDE[tsql](../../includes/tsql-md.md)])".  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Las sugerencias de tabla se deben quitar de las definiciones de las vistas indizadas. Independientemente del modo de compatibilidad que se utilice, es recomendable que pruebe la aplicación. Al hacerlo, puede asegurarse de que funciona como es de esperar a la hora de crear, actualizar u obtener acceso a las vistas indizadas, incluyendo el caso en el que las vistas indizadas estén en concordancia con ciertas consultas.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
