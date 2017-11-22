---
title: "Inicie el Administrador de configuración (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b914ba9a-e4ec-4750-934a-c447fc8909e3
caps.latest.revision: "22"
ms.openlocfilehash: 98ae90d198b4a1b68e1b72305721611a8efa30ff
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="launch-the-configuration-manager"></a>Inicie el Administrador de configuración
Este tema proporciona instrucciones para iniciar el **Configuration Manager** para el dispositivo de sistema de la plataforma de análisis.  
  
## <a name="before-you-begin"></a>Antes de comenzar  
  
### <a name="prerequisites"></a>Requisitos previos  
El sistema de la plataforma de análisis**Configuration Manager** sólo se puede ejecutar el Administrador de dominio de aplicación. Para ejecutar esta herramienta, es necesaria la contraseña para el Administrador de dominio de aplicación. Para crear otros administradores APS, vea [crear un administrador de dominio AP &#40; Ap &#41; ](create-an-aps-domain-administrator-aps.md).  
  
## <a name="Accessing"></a>Inicie la herramienta Administrador de configuración  
Para ejecutar el Administrador de configuración, utilice Escritorio remoto para conectarse al nodo de Control de PDW (***PDW_region*-CTL01**) nodo y conéctese como *appliance_domain* **\Administrator**. Al iniciar la **Configuration Manager** de programa, use la **ejecutar como administrador** opción para asegurarse de que se utilizan las credenciales de administrador.  
  
#### <a name="to-launch-from-a-browser-window"></a>Para iniciar desde una ventana del explorador  
  
1.  Abra un explorador y navegue al directorio `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
2.  Haga clic en `dwconfig.exe` y, a continuación, haga clic en **ejecutar como administrador**.  
  
#### <a name="to-launch-from-a-command-prompt"></a>Para iniciar desde un símbolo del sistema  
  
1.  En el escritorio, abra el **iniciar** menú, haga clic en **programas**, haga clic en **Accesorios**, haga clic en **símbolo** y, a continuación, haga clic en  **Ejecutar como administrador**.  
  
2.  En el símbolo del sistema, escriba el siguiente comando para cambiar el directorio: `cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"`.  
  
3.  En el símbolo del sistema, escriba `dwconfig.exe`.  
  
Después de la **Configuration Manager** está iniciado, verá toda funcionalidad disponible en el panel izquierdo. El resto de esta sección describe cómo realizar cada acción disponible en la herramienta.  
  
Para cerrar y salir **Configuration Manager**, haga clic en **salir** en la esquina inferior derecha de la pantalla.  
  
![SQL_Server_PDW_DWConfig_ApplTop](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>Vea también  
[Supervisar el dispositivo mediante la consola de administración &#40; Sistema de la plataforma de análisis &#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
