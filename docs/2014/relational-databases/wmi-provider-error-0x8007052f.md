---
title: Error de WMI 0x8007052f | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- 0x8007052f (WMI error)
ms.assetid: a33f12bd-15c4-42a8-b343-de44c3e87729
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c1668c2b4c96f23283f0eca87fdbac591f52b75f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211602"
---
# <a name="wmi-error-0x8007052f"></a>Error de WMI 0x8007052f
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|0x8007052f|  
|Origen del evento|Error de proveedor WMI|  
|Componente|Administrador de configuración de SQL Server|  
|Nombre simbólico|N/D|  
|Texto del mensaje|Error de inicio de sesión: restricción de cuenta de usuario. Razones posibles: no se admiten contraseñas en blanco, restricciones en las horas de inicio de sesión, o se ha aplicado una restricción de directiva.|  
  
## <a name="explanation"></a>Explicación  
 Este error puede producirse al usar el Administrador de configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para pasar a las cuentas integradas (Servicio de red, Servicio local o Sistema local) cuando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se ejecuta en un clúster de Windows Server o un controlador de dominio de Windows Server. No ejecute servicios en cuentas integradas en un clúster de Windows Server o un controlador de dominio de Windows Server. Para obtener recomendaciones sobre cuentas de servicio, vea el tema Configurar cuentas de servicio de Windows en los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="user-action"></a>Acción del usuario  
 Configure [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para usar una cuenta de dominio.  
  
  
