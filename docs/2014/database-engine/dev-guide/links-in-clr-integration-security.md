---
title: Vínculos en la seguridad de integración de CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- table-access links [CLR integration]
- security [CLR integration]
- invocation links [CLR integration]
- gated links [CLR integration]
ms.assetid: 168efd01-d12e-4bdf-a1b3-0b5c76474eaf
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 37aa64129658128bd7297f147f317166917e05a6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62781074"
---
# <a name="links-in-clr-integration-security"></a>Vínculos en el ámbito de seguridad de la integración CLR
  En esta sección se describe cómo los distintos fragmentos de código del usuario pueden llamarse entre sí en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ya sea en [!INCLUDE[tsql](../../includes/tsql-md.md)] o en uno de los lenguajes administrados. Estas relaciones entre objetos reciben el nombre de vínculos.  
  
## <a name="invocation-links"></a>Vínculos de invocación  
 Los vínculos de invocación corresponden a una invocación del código, ya sea de un usuario que llama a un objeto (como un lote [!INCLUDE[tsql](../../includes/tsql-md.md)] que llama a un procedimiento almacenado) o de un procedimiento almacenado o una función de Common Language Runtime (CLR). Los vínculos de invocación hacen que se compruebe un permiso `EXECUTE` en el destinatario.  
  
## <a name="table-access-links"></a>Vínculos de acceso a tablas  
 Los vínculos de acceso a tablas corresponden a valores de recuperación o modificación de una tabla, vista o función con valores de tabla. Son similares a los vínculos de invocación, pero tienen un control de acceso más exhaustivo en lo que se refiere a los permisos SELECT, INSERT, UPDATE y DELETE .  
  
## <a name="gated-links"></a>Vínculos canalizados  
 Los vínculos canalizados implican que, durante la ejecución, los permisos no se comprueban a través de la relación de objetos una vez que se ha establecido. Cuando hay un vínculo canalizado entre dos objetos (por ejemplo, un objeto **x** y un objeto **y**), los permisos en el objeto **y** y otros objetos a los que se obtiene acceso desde el objeto **y** solamente se comprueban en el momento de creación del objeto **x**. En el momento de la creación **** del objeto `REFERENCE` x, el permiso se comprueba en **y** con el propietario de **x**. En tiempo de ejecución (por ejemplo, cuando alguien llama al objeto **x**), no hay ningún permiso comprobado en **y** ni en otros objetos a los que hace referencia de forma estática. En tiempo de ejecución, un permiso adecuado se comprobará en el propio objeto **x** .  
  
 Los vínculos canalizados siempre se usan junto con una dependencia de metadatos entre dos objetos. Esta dependencia de metadatos es una relación establecida en catálogos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que impide que se quite un objeto siempre que haya otro objeto que dependa de él.  
  
 Los vínculos canalizados son muy útiles cuando resulta adecuado o sencillo conceder permisos a muchos objetos dependientes. Los vínculos canalizados se introducen entre los objetos que definen los puntos de entrada de [!INCLUDE[tsql](../../includes/tsql-md.md)] en los ensamblados CLR (por ejemplo, los agregados, tipos, funciones, desencadenadores y procedimientos CLR) y los ensamblados a partir de los cuales se definen. La seguridad canalizada en estos objetos implica que, para invocar un punto de entrada [!INCLUDE[tsql](../../includes/tsql-md.md)] definido en un ensamblado CLR, el autor de las llamadas solamente necesita un permiso adecuado en ese punto de entrada [!INCLUDE[tsql](../../includes/tsql-md.md)] . No es necesario que el autor de las llamadas tenga permisos en ese ensamblado o en cualquier otro ensamblado al que haga referencia de forma estática. Los permisos en el ensamblado se comprueban en el momento de creación del punto de entrada [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
## <a name="sql-server-authorization-based-security"></a>Seguridad basada en autorizaciones de SQL Server  
 A continuación se muestran las reglas básicas subyacentes a las comprobaciones de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para las invocaciones de y entre objetos de base de datos basados en CLR; las primeras tres reglas definen qué permisos deben comprobarse y en qué objeto; la cuarta regla define en qué contexto de ejecución debe comprobarse el permiso.  
  
1.  Todas las invocaciones requieren el permiso `EXECUTE`, a menos que tengan lugar dentro del mismo objeto; esto significa que las llamadas dentro del mismo ensamblado no requieren comprobaciones de permisos. Los permisos se comprueban en tiempo de ejecución.  
  
2.  Los vínculos canalizados requieren el permiso `REFERENCE` en el destinatario cuando se crea el objeto de llamada. El permiso se comprueba para el propietario del objeto de llamada cuando se crea el objeto.  
  
3.  Los vínculos de acceso a tablas requieren el permiso `SELECT`, `INSERT`, `UPDATE` o `DELETE` correspondiente en la tabla o vista a la que se obtiene acceso.  
  
4.  El permiso se comprueba en el contexto de ejecución actual. Pueden crearse procedimientos y funciones con un contexto de ejecución diferente al del autor de las llamadas. Los ensamblados siempre se crean con el contexto de ejecución del procedimiento, función o desencadenador que se define en el mismo.  
  
## <a name="see-also"></a>Consulte también  
 [Seguridad de la integración CLR](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
