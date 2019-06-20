---
title: Ejecutar la aplicación Data Quality Client | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.browseforservers.f1
- sql13.dqs.connecttoserver.f1
ms.assetid: 0b2aa202-7ab2-4c9d-b0f1-802588053a1e
author: lrtoyou1223
ms.author: lle
manager: jroth
ms.openlocfilehash: b34e3fa7ba8bafd88ed9da4a237d624ebc45cad1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801419"
---
# <a name="run-the-data-quality-client-application"></a>Ejecutar la aplicación Data Quality Client

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Ejecute [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]e inicie sesión en una instancia de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Debe haber completado la instalación del [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] ejecutando el archivo DQSInstaller.exe. Para obtener más información, vea [Ejecutar DQSInstaller.exe para completar la instalación del servidor de calidad de datos](../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Para poder iniciar sesión en [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], es necesario disponer de uno de los tres roles de DQS (dqs_administrator, dqs_kb_editor o dqs_kb_operator) en la base de datos DQS_MAIN.  
  
##  <a name="Run"></a> Ejecutar Data Quality Client  
 Para ejecutar [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] en el equipo donde lo ha instalado:  
  
1.  Haga clic en **Inicio**, seleccione **Todos los programas**, seleccione **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**, seleccione **Data Quality Services**y, por último, haga clic en **Data Quality Client**.  
  
2.  En el cuadro de diálogo **Conectar al servidor** :  
  
    1.  Especifique el servidor al que desea conectar la aplicación [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Seleccione **(LOCAL)** para conectarse con [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] en el equipo local. También puede hacer clic en la flecha hacia abajo y seleccionar **\<Buscar más servidores>** en la red para conectarse a un servidor diferente (o al servidor local basándose en el nombre). Se mostrará el cuadro de diálogo **Buscar servidores** . Puede seleccionar un servidor en la pestaña **Servidores locales** o en la pestaña **Servidores de redes** .  
  
    2.  Para cifrar la transferencia de datos entre [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] y [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], haga clic en **Opciones**y luego active la casilla **Cifrar conexión** .  
  
3.  Haga clic en **Conectar**.  
  
 Aparece la página de inicio del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Para más información, vea [Página de inicio del cliente de calidad de datos](../data-quality-services/data-quality-client-home-screen.md).  
  
  
