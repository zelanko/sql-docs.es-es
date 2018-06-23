---
title: Creación de objetos de base de datos con la integración de Common Language Runtime (CLR) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- database objects [CLR integration], building
- common language runtime [SQL Server], building database objects
- managed code [SQL Server], database objects
- building database objects [CLR integration]
- .NET Framework routines [SQL Server]
ms.assetid: ce34132c-bfa3-447b-9131-b6e17c672efe
caps.latest.revision: 47
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 070e9df2a42cbed665de1b076600d333926f6ea1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199705"
---
# <a name="building-database-objects-with-common-language-runtime-clr-integration"></a>Crear objetos de base de datos con la integración de Common Language Runtime (CLR)
  Puede crear objetos de base de datos mediante la [!INCLUDE[ssNoVersion](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se conoce como una "rutina CLR". Estas rutinas incluyen:  
  
-   Funciones definidas por el usuario con valores escalares (UDF escalares)  
  
-   Funciones definidas por el usuario con valores de tabla (TVF)  
  
-   Procedimientos definidos por el usuario (UDP)  
  
-   Desencadenadores definidos por el usuario  
  
 Las rutinas CLR tienen la misma estructura en código administrado. Están asignadas a los métodos público, estático (compartidos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET) de una clase. Además de las rutinas, los tipos definidos por el usuario (UDT) y las funciones de agregado definidas por el usuario también se pueden definir mediante .NET Framework. Los UDT y los agregados definidos por el usuario están asignados a las clases de .NET Framework completas.  
  
 Cada tipo de rutina de .NET Framework tiene una [!INCLUDE[tsql](../../../includes/ssnoversion-md.md)] que la [!INCLUDE[tsql](../../../includes/tsql-md.md)] equivalente se puede utilizar. Por ejemplo, los UDF escalares se pueden usar en cualquier expresión escalar. Un TVF se puede usar en cualquier cláusula FROM. Un procedimiento se puede invocar en una instrucción EXEC o bien, desde una aplicación cliente.  
  
> [!NOTE]  
>  La ejecución de un objeto CLR (función definida por el usuario, tipo definido por el usuario o desencadenador) en el Common Language Runtime puede tener lugar en varios subprocesos (el plan paralelo), si el optimizador de consultas decide que es beneficioso. Sin embargo, si una función definida por el usuario tiene acceso a los datos, la ejecución estará en un plan de serie. Cuando se ejecuta en una versión de servidor anterior a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], si una función definida por el usuario contiene parámetros LOB o valores devueltos, la ejecución también debe estar en un plan en serie.  
  
 En la siguiente tabla se enumeran los temas incluidos en esta sección.  
  
 [Introducción a la integración CLR](getting-started-with-clr-integration.md)  
 Proporciona una breve información general de las bibliotecas y los espacios de nombres requeridos para compilar objetos mediante la integración CLR con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Incluye un procedimiento almacenado CLR "Hello World" de ejemplo.  
  
 [Bibliotecas de .NET Framework admitidas](supported-net-framework-libraries.md)  
 Proporciona información sobre las bibliotecas de .NET Framework admitidas por la integración CLR.  
  
 [Restricciones del modelo de programación de la integración CLR](clr-integration-programming-model-restrictions.md)  
 Proporciona información sobre las restricciones del modelo de programación de integración CLR.  
  
 [Tipos de datos de SQL Server en .NET Framework](../../clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
 Información general de tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y sus equivalentes de .NET Framework.  
  
 [Información general de atributos personalizados de integración de CLR](../../../database-engine/dev-guide/overview-of-clr-integration-custom-attributes.md)  
 Proporciona información sobre los atributos personalizados de integración CLR.  
  
 [Funciones CLR definidas por el usuario](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)  
 Describe cómo implementar y usar los distintos tipos de funciones CLR: funciones de agregado definidas por el usuario, escalares y con valores de tabla.  
  
 [Tipos definidos por el usuario de CLR](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
 Describe cómo implementar y usar los tipos definidos por el usuario CLR.  
  
 [Procedimientos almacenados de CLR](../../../database-engine/dev-guide/clr-stored-procedures.md)  
 Describe cómo implementar y usar los procedimientos almacenados CLR.  
  
 [Desencadenadores CLR](../../../database-engine/dev-guide/clr-triggers.md)  
 Describe cómo implementar y usar los desencadenadores CLR.  
  
## <a name="see-also"></a>Vea también  
 [Common Language Runtime &#40;CLR&#41; descripción de la integración](../common-language-runtime-integration-overview.md)  
  
  