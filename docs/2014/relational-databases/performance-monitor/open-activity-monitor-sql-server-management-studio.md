---
title: Apertura del Monitor de actividad (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Activity Monitor [SQL Server], setting the refresh interval
- refresh interval for Activity Monitor
- Activity Monitor [SQL Server], opening
- opening Activity Monitor
ms.assetid: 0a6eeb16-f02b-479d-9a60-543e40ebf46b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cf893c3d46530a8d4457e3d7e434be792d5647ae
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171665"
---
# <a name="open-activity-monitor-sql-server-management-studio"></a>Abrir el Monitor de actividad (SQL Server Management Studio)
  En este tema se describe cómo abrir el Monitor de actividad para obtener información sobre los procesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la forma en que estos procesos afectan a la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. También se describe cómo establecer el intervalo de actualización del Monitor de actividad.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para abrir el Monitor de actividad con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
-   **Configuración del intervalo de actualización utilizando lo siguiente:**  [SQL Server Management Studio](#Refresh)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
 El Monitor de actividad ejecuta consultas en la instancia supervisada para obtener información de sus paneles de información. Cuando el intervalo de actualización se establece en menos de 10 segundos, el tiempo utilizado para ejecutar estas consultas puede afectar al rendimiento del servidor  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Para ver el Monitor de actividad, el usuario debe tener el permiso VIEW SERVER STATE. Para ver la sección de E/S de archivo de datos del Monitor de actividad, debe tener permisos CREATE DATABASE, ALTER ANY DATABASE o VIEW ANY DEFINITION además de VIEW SERVER STATE.  
  
 Para detener (KILL) un proceso, el usuario debe ser miembro de los roles fijos de servidor sysadmin o processadmin.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-open-activity-monitor-in-sql-server-management-studio"></a>Para abrir el Monitor de actividad en SQL Server Management Studio  
  
1.  En la barra de herramientas estándar de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , haga clic en **Monitor de actividad**.  
  
2.  En el cuadro de diálogo **Conectar al servidor** , seleccione el nombre del servidor y el modo de autenticación y, a continuación, haga clic en **Conectar**.  
  
 También puede abrir el Monitor de actividad en cualquier momento presionando CTRL+ALT A.  
  
#### <a name="to-open-activity-monitor-in-object-explorer"></a>Para abrir el Monitor de actividad en el Explorador de objetos  
  
-   En el Explorador de objetos, haga clic con el botón secundario en el nombre de instancia y, a continuación, seleccione **Monitor de actividad**.  
  
#### <a name="to-open-activity-monitor-when-opening-sql-server-management-studio"></a>Para abrir el Monitor de actividad al abrir SQL Server Management Studio  
  
1.  En el menú **Herramientas** , haga clic en **Opciones**.  
  
2.  En el cuadro de diálogo **Opciones** , expanda **Entorno**y, a continuación, seleccione **General**.  
  
3.  En el cuadro **Al iniciar** , seleccione **Abrir el Explorador de objetos y el Monitor de actividad**.  
  
4.  Para activar los cambios, cierre y vuelva a abrir [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
###  <a name="Refresh"></a> Para establecer el intervalo de actualización del Monitor de actividad  
  
-   Abra el Monitor de actividad.  
  
-   Haga clic con el botón derecho en **Información general**, seleccione **Intervalo de actualización**y después seleccione el intervalo en el que el Monitor de actividad debería obtener nueva información de la instancia.  
  
  
