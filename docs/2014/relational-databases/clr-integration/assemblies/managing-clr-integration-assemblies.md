---
title: Administrar ensamblados de integración CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- database objects [CLR integration], assemblies
- common language runtime [SQL Server], assemblies
- assemblies [CLR integration], managing
ms.assetid: bdbbf325-14f6-460e-a35a-d3861d3c961e
author: rothja
ms.author: jroth
ms.openlocfilehash: f9acc56d72d2ed994f497676813e45ef0a914431
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84953786"
---
# <a name="managing-clr-integration-assemblies"></a>Administrar ensamblados de integración CLR
  El código administrado se compila y, a continuación, se implementa en unidades denominadas ensamblado. Un ensamblado se empaqueta como un archivo DLL o ejecutable (.exe). Aunque un archivo ejecutable se puede ejecutar solo, una DLL se debe hospedar en una aplicación existente. Los ensamblados DLL administrados pueden cargarse y hospedarse en [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]base de datos que usa la instrucción CREATE ASSEMBLy, antes de que se pueda cargar en el proceso y utilizar. Los ensamblados también pueden actualizarse a partir de una versión más reciente mediante la instrucción ALTER ASSEMBLY o quitarse de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la instrucción DROP ASSEMBLY.  
  
 La información del ensamblado se almacena en la tabla `sys.assembly_files` de la base de datos en la que se ha instalado el ensamblado. La tabla `sys.assembly_files` contiene las columnas siguientes:  
  
|Columna|Descripción|  
|------------|-----------------|  
|assembly_id|Identificador definido para el ensamblado. Este número se asigna a todos los objetos relacionados con el mismo ensamblado.|  
|name|Nombre del objeto.|  
|file_id|Un número que identifica cada objeto, siendo 1 el valor del primer objeto asociado a un `assembly_id` determinado. Si varios objetos están asociados al mismo `assembly_id`, 1 incrementa a continuación cada valor `file_id` subsiguiente.|  
|contenido|Representación hexadecimal del ensamblado o archivo.|  
  
## <a name="in-this-section"></a>En esta sección  
 [Crear un ensamblado](creating-an-assembly.md)  
 Describe la creación de los ensamblados SAFE, EXTERNAL_ACCESS y UNSAFE CLR en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Modificar un ensamblado](altering-an-assembly.md)  
 Describe la actualización de los ensamblados CLR en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Quitar un ensamblado](dropping-an-assembly.md)  
 Describe cómo quitar los ensamblados CLR de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Seguridad de la integración CLR](../security/clr-integration-security.md)   
 [Seguridad de acceso del código de integración CLR](../security/clr-integration-code-access-security.md)  
  
  
