---
title: Iniciar Configuration Manager
description: Instrucciones para iniciar la herramienta de Configuration Manager para el dispositivo de sistema de plataforma de análisis.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: be69331ec9f9daa091035d6ef21142c4f40d6a84
ms.sourcegitcommit: 442fbe1655d629ecef273b02fae1beb2455a762e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235172"
---
# <a name="launch-the-configuration-manager-in-analytics-platform-system"></a>Inicio del Configuration Manager en Analytics Platform System
En este tema se proporcionan instrucciones para iniciar el **Configuration Manager** para el dispositivo de sistema de plataforma de análisis.  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
### <a name="prerequisites"></a>Requisitos previos  
Solo el administrador de dominio de la aplicación puede ejecutar el **Configuration Manager** de sistema de la plataforma de análisis. Para ejecutar esta herramienta, necesita la contraseña del administrador de dominio del dispositivo. Para crear administradores de APS adicionales, consulte [crear un administrador de dominio aps &#40;aps&#41;](create-an-aps-domain-administrator-aps.md).  
  
## <a name="launch-the-configuration-manager-tool"></a><a name="Accessing"></a>Iniciar la herramienta de Configuration Manager  
Para ejecutar el Configuration Manager, use Escritorio remoto para conectarse al nodo de control PDW ( **_PDW_region_ -CTL01** ) e inicie sesión como _appliance_domain_**\Administrador** . Al iniciar el programa de **Configuration Manager** , use la opción **Ejecutar como administrador** para asegurarse de que se utilizan las credenciales de administrador.  
  
#### <a name="to-launch-from-a-browser-window"></a>Para iniciar desde una ventana del explorador  
  
1.  Abra un explorador y navegue hasta el directorio `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100` .  
  
2.  Haga clic con el botón secundario `dwconfig.exe` y, a continuación, haga clic en **Ejecutar como administrador** .  
  
#### <a name="to-launch-from-a-command-prompt"></a>Para iniciar desde un símbolo del sistema  
  
1.  En el escritorio, abra el menú **Inicio** , haga clic en **programas** , **accesorios** , haga clic con el botón secundario en **símbolo del sistema** y, a continuación, haga clic en **Ejecutar como administrador** .  
  
2.  En el símbolo del sistema, escriba el siguiente comando para cambiar los directorios: `cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"` .  
  
3.  En el símbolo del sistema, escriba `dwconfig.exe`.  
  
Una vez iniciado el **Configuration Manager** , verá todas las funciones disponibles en el panel izquierdo. En el resto de esta sección se describe cómo realizar cada una de las acciones disponibles en la herramienta.  
  
Para cerrar y salir de **Configuration Manager** , haga clic en **salir** en la esquina inferior derecha de cualquier pantalla.  
  
![Captura de pantalla del cuadro de diálogo Microsoft Analytics Platform System Configuration Manager que muestra la topología del dispositivo.](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>Consulte también  
[Supervise el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
