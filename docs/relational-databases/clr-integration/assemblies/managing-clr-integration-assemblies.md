---
title: Administración de ensamblados de integración de CLR Microsoft Docs
description: Puede hospedar ensamblados DLL administrados en SQL Server.  Puede registrar, modificar y quitar ensamblados, así como administrar los archivos y permisos asociados.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 19b90d7994aa4b75a294f24345d43333d13a22df
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484837"
---
# <a name="managing-clr-integration-assemblies"></a>Administrar ensamblados de integración CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El código administrado se compila y, a continuación, se implementa en unidades denominadas ensamblado. Un ensamblado se empaqueta como un archivo DLL o ejecutable (.exe). Aunque un archivo ejecutable se puede ejecutar solo, una DLL se debe hospedar en una aplicación existente. Los ensamblados DLL administrados se [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]pueden cargar y hospedar en . [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requiere que el ensamblado se registre en una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la instrucción CREATE ASSEMBLY para poder cargarlo en el proceso y usarlo. Los ensamblados también pueden actualizarse a partir de una versión más reciente mediante la instrucción ALTER ASSEMBLY o quitarse de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la instrucción DROP ASSEMBLY.  
  
 La información del ensamblado se almacena en la tabla **sys.assembly_files** de la base de datos donde se ha instalado el ensamblado. La tabla **sys.assembly_files** contiene las siguientes columnas.  
  
|Columna|Descripción|  
|------------|-----------------|  
|assembly_id|Identificador definido para el ensamblado. Este número se asigna a todos los objetos relacionados con el mismo ensamblado.|  
|name|Nombre del objeto.|  
|file_id|Un número que identifica cada objeto, con el primer objeto asociado a un **assembly_id** dado se le da el valor de 1. Si varios objetos están asociados con el mismo **assembly_id**, cada valor **de file_id** posterior se incrementa en 1.|  
|content|Representación hexadecimal del ensamblado o archivo.|  
  
## <a name="in-this-section"></a>En esta sección  
 [Crear un ensamblado](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
 Describe la creación de los ensamblados SAFE, EXTERNAL_ACCESS y UNSAFE CLR en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Modificar un ensamblado](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)  
 Describe la actualización de los ensamblados CLR en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Quitar un ensamblado](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)  
 Describe cómo quitar los ensamblados CLR de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Seguridad de integración de CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Seguridad de acceso del código de integración CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
  
  
