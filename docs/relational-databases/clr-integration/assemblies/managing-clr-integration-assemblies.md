---
title: Administrar ensamblados de integración CLR | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- database objects [CLR integration], assemblies
- common language runtime [SQL Server], assemblies
- assemblies [CLR integration], managing
ms.assetid: bdbbf325-14f6-460e-a35a-d3861d3c961e
caps.latest.revision: 56
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9c4883867e93c1f8a9e782f1e0a70d8ca6f53160
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="managing-clr-integration-assemblies"></a>Administrar ensamblados de integración CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El código administrado se compila y, a continuación, se implementa en unidades denominadas ensamblado. Un ensamblado se empaqueta como un archivo DLL o ejecutable (.exe). Aunque un archivo ejecutable se puede ejecutar solo, una DLL se debe hospedar en una aplicación existente. Los ensamblados DLL administrados pueden cargarse y hospedados por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requiere que el ensamblado se registre en una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la instrucción CREATE ASSEMBLY para poder cargarlo en el proceso y usarlo. Los ensamblados también pueden actualizarse a partir de una versión más reciente mediante la instrucción ALTER ASSEMBLY o quitarse de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la instrucción DROP ASSEMBLY.  
  
 Información de ensamblado se almacena en la **sys.assembly_files** tabla en la base de datos que se ha instalado el ensamblado. El **sys.assembly_files** tabla contiene las columnas siguientes.  
  
|Columna|Description|  
|------------|-----------------|  
|assembly_id|Identificador definido para el ensamblado. Este número se asigna a todos los objetos relacionados con el mismo ensamblado.|  
|name|Nombre del objeto.|  
|file_id|Número que identifica cada objeto, con el primer objeto asociado a una determinada **assembly_id** se le asigna el valor de 1. Si varios objetos están asociados con el mismo **assembly_id**, a continuación, cada **file_id** valor se incrementa en 1.|  
|content|Representación hexadecimal del ensamblado o archivo.|  
  
## <a name="in-this-section"></a>En esta sección  
 [Creación de un ensamblado](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
 Describe la creación de los ensamblados SAFE, EXTERNAL_ACCESS y UNSAFE CLR en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Modificar un ensamblado](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)  
 Describe la actualización de los ensamblados CLR en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Quitar un ensamblado](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)  
 Describe cómo quitar los ensamblados CLR de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de la integración de CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Seguridad de acceso del código de integración CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
  
  
