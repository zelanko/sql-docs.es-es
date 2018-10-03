---
title: Instalar el Asesor de actualizaciones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- Upgrade Advisor [SQL Server], installing
ms.assetid: 1b7d6eca-1df1-47df-bbba-0fc485706a95
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 95bcdfca34b618043515c27030bc74104e4da590
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078075"
---
# <a name="installing-upgrade-advisor"></a>Instalar el Asesor de actualizaciones
  La ubicación en la que instala el Asesor de actualizaciones de SQL Server 2014 depende de lo que vaya a analizar. El Asesor de actualizaciones admite el análisis remoto de todos los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , excepto [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Si no está analizando instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], puede instalar el Asesor de actualizaciones en cualquier equipo que pueda conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y que cumpla con los [Upgrade Advisor Prerequisites](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md). Si está examinando instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], debe instalar el Asesor de actualizaciones en el servidor de informes.  
  
 Ejecute el archivo **SQLUA.msi** para instalar el Asesor de actualizaciones. Puede instalarlo desde el símbolo del sistema para las instalaciones desatendidas y automatizadas. Vea [Installing Upgrade Advisor from the Command Prompt](../../../2014/sql-server/install/installing-upgrade-advisor-from-the-command-prompt.md) para la sintaxis y ejemplos.  
  
 Obtener SQLUA.msi:  
  
-   En la carpeta **redist** del soporte del producto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Como parte de la [descarga SQL 2014 Feature Pack](http://www.microsoft.com/download/details.aspx?id=42295).  
  
## <a name="uninstalling-upgrade-advisor"></a>Desinstalar el Asesor de actualizaciones  
 Puede desinstalar el Asesor de actualizaciones mediante **Agregar o quitar programas**. La sintaxis del símbolo del sistema también admite la eliminación o desinstalación.  
  
  
