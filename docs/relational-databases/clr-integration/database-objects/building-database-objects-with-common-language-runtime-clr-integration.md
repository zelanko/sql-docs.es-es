---
title: Objetos de base de datos de compilación de Common Language Runtime (CLR)
description: Cree objetos de base de datos mediante la integración de SQL Server con el Common Language Runtime de .NET Framework (CLR).
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- database objects [CLR integration], building
- common language runtime [SQL Server], building database objects
- managed code [SQL Server], database objects
- building database objects [CLR integration]
- .NET Framework routines [SQL Server]
ms.assetid: ce34132c-bfa3-447b-9131-b6e17c672efe
author: rothja
ms.author: jroth
ms.openlocfilehash: 5dc38fc39a0f4d876adc99a0aff87d2acaad1545
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789558"
---
# <a name="building-database-objects-with-common-language-runtime-clr-integration"></a>Generar objetos de base de datos con la integración de Common Language Runtime (CLR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  Puede generar objetos de base de datos mediante la integración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con .NET Framework Common Language Runtime (CLR). El código administrado que se ejecuta dentro de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se conoce como "rutina de CLR". Estas rutinas incluyen:  
  
-   Funciones definidas por el usuario con valores escalares (UDF escalares)  
  
-   Funciones definidas por el usuario con valores de tabla (TVF)  
  
-   Procedimientos definidos por el usuario (UDP)  
  
-   Desencadenadores definidos por el usuario  
  
 Las rutinas CLR tienen la misma estructura en código administrado. Están asignadas a los métodos público, estático (compartidos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET) de una clase. Además de las rutinas, los tipos definidos por el usuario (UDT) y las funciones de agregado definidas por el usuario también se pueden definir mediante .NET Framework. Los UDT y los agregados definidos por el usuario están asignados a las clases de .NET Framework completas.  
  
 Cada tipo de rutina de .NET Framework tiene una declaración de [!INCLUDE[tsql](../../../includes/tsql-md.md)] y se usa en cualquier parte de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la que el equivalente de [!INCLUDE[tsql](../../../includes/tsql-md.md)] se puede utilizar. Por ejemplo, los UDF escalares se pueden usar en cualquier expresión escalar. Un TVF se puede usar en cualquier cláusula FROM. Un procedimiento se puede invocar en una instrucción EXEC o bien, desde una aplicación cliente.  
  
> [!NOTE]  
>  La ejecución de un objeto CLR (función definida por el usuario, tipo definido por el usuario o desencadenador) en el Common Language Runtime puede tener lugar en varios subprocesos (el plan paralelo), si el optimizador de consultas decide que es beneficioso. Sin embargo, si una función definida por el usuario tiene acceso a los datos, la ejecución estará en un plan de serie. Cuando se ejecuta en una versión de servidor anterior a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], si una función definida por el usuario contiene parámetros LOB o valores devueltos, la ejecución también debe estar en un plan en serie.  
  
 En la siguiente tabla se enumeran los temas incluidos en esta sección.  
  
 [Introducción a la integración CLR](../../../relational-databases/clr-integration/database-objects/getting-started-with-clr-integration.md)  
 Proporciona una breve información general de las bibliotecas y los espacios de nombres requeridos para compilar objetos mediante la integración CLR con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Incluye un procedimiento almacenado CLR "Hello World" de ejemplo.  
  
 [Bibliotecas de .NET Framework admitidas](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)  
 Proporciona información sobre las bibliotecas de .NET Framework admitidas por la integración CLR.  
  
 [Restricciones del modelo de programación de la integración CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
 Proporciona información sobre las restricciones del modelo de programación de integración CLR.  
  
 [Tipos de datos de SQL Server en .NET Framework](../../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
 Información general de tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y sus equivalentes de .NET Framework.  
  
 [Información general de los atributos personalizados de la integración CLR](https://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)  
 Proporciona información sobre los atributos personalizados de integración CLR.  
  
 [Funciones definidas por el usuario de CLR](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)  
 Describe cómo implementar y usar los distintos tipos de funciones CLR: funciones de agregado definidas por el usuario, escalares y con valores de tabla.  
  
 [Tipos CLR definidos por el usuario](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
 Describe cómo implementar y usar los tipos definidos por el usuario CLR.  
  
 [Procedimientos almacenados CLR](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)  
 Describe cómo implementar y usar los procedimientos almacenados CLR.  
  
 [Desencadenadores de CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
 Describe cómo implementar y usar los desencadenadores CLR.  
  
## <a name="see-also"></a>Consulte también  
 [Información general sobre la integración de Common Language Runtime &#40;CLR&#41;](../../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)  
  
  
