---
title: Inicie el Administrador de configuración - Analytics Platform System | Microsoft Docs
description: Instrucciones para iniciar la herramienta Administrador de configuración para la aplicación Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 087360981a7c31de6980755cfee4f98f88f48a15
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502455"
---
# <a name="launch-the-configuration-manager-in-analytics-platform-system"></a>Inicie el Administrador de configuración de Analytics Platform System
Este tema proporciona instrucciones para iniciar el **Configuration Manager** para la aplicación Analytics Platform System.  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
### <a name="prerequisites"></a>Requisitos previos  
El sistema Analytics Platform System**Configuration Manager** solo se puede ejecutar el Administrador de dominio del dispositivo. Para ejecutar esta herramienta, necesitará la contraseña para el Administrador de dominio de aplicación. Para crear otros administradores APS, vea [crear un administrador de dominio de APS &#40;APS&#41;](create-an-aps-domain-administrator-aps.md).  
  
## <a name="Accessing"></a>Inicie la herramienta Administrador de configuración  
Para ejecutar el Administrador de configuración, utilice Escritorio remoto para conectarse al nodo de Control de PDW (**_PDW_region_-CTL01**) nodo e inicie sesión como _appliance_domain_ **\Administrator**. Al iniciar el **Configuration Manager** de programa, use la **ejecutar como administrador** opción para asegurarse de que se usan las credenciales de administrador.  
  
#### <a name="to-launch-from-a-browser-window"></a>Iniciar desde una ventana del explorador  
  
1.  Abra un explorador y navegue hasta el directorio `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
2.  Haga clic en `dwconfig.exe` y, a continuación, haga clic en **ejecutar como administrador**.  
  
#### <a name="to-launch-from-a-command-prompt"></a>Para iniciar desde un símbolo del sistema  
  
1.  En el escritorio, abra el **iniciar** menú, haga clic en **programas**, haga clic en **Accesorios**, haga clic en **símbolo** y, a continuación, haga clic en  **Ejecutar como administrador**.  
  
2.  En el símbolo del sistema, escriba el siguiente comando para cambiar el directorio: `cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"`.  
  
3.  En el símbolo del sistema, escriba `dwconfig.exe`.  
  
Después de la **Configuration Manager** está iniciado, verá todas las funciones disponibles aparecen en el panel izquierdo. El resto de esta sección explica cómo realizar cada acción disponible en la herramienta.  
  
Para cerrar y salir **Configuration Manager**, haga clic en **salir** en la esquina inferior derecha de la pantalla.  
  
![SQL_Server_PDW_DWConfig_ApplTop](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>Vea también  
[Supervisión del dispositivo mediante el uso de la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
