---
title: Componentes de configuración | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], configuring
ms.assetid: 0b68ff48-12e4-41aa-b9e2-b39ed5023ea7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bcf7d34f8faf70f57373ad1a5dae55261799145b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63198412"
---
# <a name="configuration-components"></a>Componentes de configuración
> [!NOTE]  
>  Desde Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. ODBC explícitamente sólo debe instalar en versiones anteriores de Windows.  
  
 Orígenes de datos se configuran mediante el instalador de DLL, que a su vez llama a controlador de configuración de archivos DLL y las DLL de instalación de traductor según sean necesarios. El instalador de DLL se bien invoca directamente desde el Panel de Control o carga y llama a otro programa, conocido como el *programa de administración*. La siguiente ilustración muestra la relación entre los componentes de configuración.  
  
 ![Relación entre componentes de configuración](../../../odbc/reference/install/media/pr30.gif "pr30")  
  
 Para obtener más información acerca de estos componentes, vea los temas siguientes al final de esta sección.  
  
-   [Programa de instalación](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL instalador](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL de instalación del controlador](../../../odbc/reference/install/driver-setup-dll.md)  
  
## <a name="see-also"></a>Vea también  
 [Componentes de instalación](../../../odbc/reference/install/installation-components.md)
