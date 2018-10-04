---
title: Parámetros de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, parameters
ms.assetid: b1bb3ea3-8097-4e76-b9c2-78a0f46a23bc
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2b2b9fc62d26edbac0244bed07d20931fbb508f8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48210385"
---
# <a name="integration-services-parameters"></a>Parámetros de Integration Services
  Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], puede decidir analizar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquetes en el equipo, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] empaquetar los archivos del sistema de archivos. Si analiza los archivos en el sistema de archivos, proporcione una ruta de acceso a la carpeta que contiene los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="options"></a>Opciones  
 **Analizar paquetes SSIS en el equipo**  
 Seleccione esta opción para analizar los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el equipo. Esta opción está seleccionada de forma predeterminada.  
  
 **Analizar archivos de paquete SSIS**  
 Seleccione esta opción para analizar los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el sistema de archivos.  
  
 **Ruta de acceso a los paquetes SSIS**  
 Busque una ruta de acceso UNC o local que contenga sus paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. No es necesario que incluya nombres de archivo. Si no se puede tener acceso a la ruta de acceso que ha escrito, no puede hacer clic **siguiente**. De forma predeterminada, la ruta de acceso está en blanco. Este campo está habilitado solo cuando se selecciona **archivos de paquete SSIS analizar**.  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Actualización del Asistente para la referencia de la interfaz de usuario](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
