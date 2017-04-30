---
title: Error de WMI 0x8007052f | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- 0x8007052f (WMI error)
ms.assetid: a33f12bd-15c4-42a8-b343-de44c3e87729
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 15e258cfe62b9b6cecdcaf3b1fc2f467ba92fab7
ms.lasthandoff: 04/11/2017

---
# <a name="wmi-provider-error-0x8007052f"></a>Error de proveedor WMI 0x8007052f
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Id. de evento|0x8007052f|  
|Origen del evento|Error de proveedor WMI|  
|Componente|Administrador de configuración de SQL Server|  
|Nombre simbólico|N/D|  
|Texto del mensaje|Error de inicio de sesión: restricción de cuenta de usuario. Razones posibles: no se admiten contraseñas en blanco, restricciones en las horas de inicio de sesión, o se ha aplicado una restricción de directiva.|  
  
## <a name="explanation"></a>Explicación  
 Este error puede producirse al usar el Administrador de configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para pasar a las cuentas integradas (Servicio de red, Servicio local o Sistema local) cuando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se ejecuta en un clúster de Windows Server o un controlador de dominio de Windows Server. No ejecute servicios en cuentas integradas en un clúster de Windows Server o un controlador de dominio de Windows Server. Para obtener recomendaciones sobre cuentas de servicio, vea el tema Configurar cuentas de servicio de Windows en los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="user-action"></a>Acción del usuario  
 Configure [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para usar una cuenta de dominio.  
  
  
