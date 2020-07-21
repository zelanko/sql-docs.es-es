---
title: Ensamblados (Motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration]
- assemblies [CLR integration], about assemblies
- managed code [SQL Server], assemblies
ms.assetid: 4b146437-3061-47f6-9e8c-26eeea10b54e
author: rothja
ms.author: jroth
ms.openlocfilehash: 0ebd47e354b77a57768a396b2c5d5dd8e3c570d2
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954265"
---
# <a name="assemblies-database-engine"></a>Ensamblados (motor de base de datos)
  En los temas de esta sección se ofrece información que le ayudará a comprender, diseñar e implementar ensamblados.  
  
 Los ensamblados son archivos DLL que se utilizan en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para implementar funciones, procedimientos almacenados, desencadenadores, agregados definidos por el usuario y tipos definidos por el usuario que se escriben en uno de los lenguajes de código administrado hospedados por el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR), en lugar de en [!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
 Un ensamblado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es un objeto que hace referencia a un módulo de aplicación administrada (archivo .dll) creado en [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Common Language Runtime. Un ensamblado contiene metadatos de clase y código administrado. El primer paso para crear los siguientes objetos de base de datos es cargar un ensamblado en una instancia de SQL Server:  
  
-   Funciones CLR. Para obtener más información, vea [Create CLR Functions](../user-defined-functions/create-clr-functions.md).  
  
-   Procedimientos almacenados CLR. Para obtener más información, vea [procedimientos almacenados CLR](../../database-engine/dev-guide/clr-stored-procedures.md).  
  
-   Desencadenadores CLR. Para obtener más información, vea [crear desencadenadores CLR](../triggers/create-clr-triggers.md).  
  
-   Funciones de agregado definidas por el usuario. Para obtener más información, consulte [crear agregados definidos por el usuario](../user-defined-functions/create-user-defined-aggregates.md).  
  
-   Tipos definidos por el usuario. Para obtener más información, vea [Tipos definidos por el usuario de CLR](../native-client/features/using-user-defined-types.md).  
  
 Los ensamblados realizan las funciones siguientes en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   Contienen el código administrado que ejecuta la funcionalidad de uno o más de los objetos de base de datos CLR antes mencionados.  
  
-   Contienen metadatos que incluyen el número de versión y la referencia cultural del ensamblado, una clave pública opcional que identifica de manera única la lista de clases del ensamblado, los métodos definidos en el ensamblado y la arquitectura de procesador del ensamblado.  
  
-   Administran el grado en el que el código administrado puede tener acceso a los recursos externos mediante la regulación de los permisos de acceso a código.  
  
-   Contienen metadatos sobre las dependencias de otros ensamblados a los que el ensamblado hace referencia.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Diseñar ensamblados](assemblies-designing.md)|Explica las consideraciones previas a la creación de un ensamblado. Se incluyen el empaquetado de los ensamblados, los permisos de acceso a código y otras restricciones.|  
|[Implementar ensamblados](assemblies-implementing.md)|Se explica cómo crear y quitar ensamblados, cómo y cuándo se pueden modificar y cómo se recuperan los metadatos sobre los ensamblados.|  
|[Obtener información acerca de los ensamblados](assemblies-getting-information.md)|Enumera las vistas de catálogo y las funciones que se pueden utilizar para consultar metadatos sobre ensamblados.|  
  
## <a name="see-also"></a>Consulte también  
 [Conceptos de programación en el ámbito de la integración de Common Language Runtime &#40;CLR&#41;](common-language-runtime-clr-integration-programming-concepts.md)  
  
  
