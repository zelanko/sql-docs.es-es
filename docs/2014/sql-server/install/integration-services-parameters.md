---
title: Parámetros de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, parameters
ms.assetid: b1bb3ea3-8097-4e76-b9c2-78a0f46a23bc
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 76a5ebe7018fdc58f02a4d2454d40f172c752c4e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059271"
---
# <a name="integration-services-parameters"></a>Parámetros de Integration Services
  Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , puede decidir analizar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquetes en el equipo o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] empaquetar archivos en el sistema de archivos. Si analiza los archivos en el sistema de archivos, proporcione una ruta de acceso a la carpeta que contiene los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="options"></a>Opciones  
 **Analizar paquetes SSIS en el equipo**  
 Seleccione esta opción para analizar los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el equipo. Esta opción está seleccionada de forma predeterminada.  
  
 **Analizar archivos de paquete SSIS**  
 Seleccione esta opción para analizar los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el sistema de archivos.  
  
 **Ruta de acceso a los paquetes de SSIS**  
 Busque una ruta de acceso UNC o local que contenga sus paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. No es necesario que incluya nombres de archivo. Si no se puede tener acceso a la ruta de acceso especificada, no puede hacer clic en **siguiente**. De forma predeterminada, la ruta de acceso está en blanco. Este campo solo está habilitado cuando se selecciona **analizar archivos de paquete SSIS**.  
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con el asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Referencia de la interfaz de usuario del Asesor de actualizaciones](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
