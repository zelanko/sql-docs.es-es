---
title: Apertura del Monitor de actividad (SSMS)
description: Procedimiento para abrir el Monitor de actividad en SQL Server Management Studio (SSMS).
ms.custom: seo-dt-2019
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Activity Monitor [SQL Server], setting the refresh interval
- refresh interval for Activity Monitor
- Activity Monitor [SQL Server], opening
- opening Activity Monitor
ms.assetid: 0a6eeb16-f02b-479d-9a60-543e40ebf46b
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 0af1ae6d145836a313df8ba6e77f965aa17e0e9a
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165528"
---
# <a name="open-activity-monitor-in-sql-server-management-studio-ssms"></a>Apertura del Monitor de actividad en SQL Server Management Studio (SSMS)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
   
 El Monitor de actividad ejecuta consultas en la instancia supervisada para obtener información de sus paneles de información. Cuando el intervalo de actualización se establece en menos de 10 segundos, el tiempo utilizado para ejecutar estas consultas puede afectar al rendimiento del servidor  
  
  
##  <a name="Permissions"></a> Compruebe los permisos.  
 Para ver la actividad real, debe tener el permiso VIEW SERVER STATE. Para ver la sección de E/S de archivo de datos del Monitor de actividad, debe tener permisos CREATE DATABASE, ALTER ANY DATABASE o VIEW ANY DEFINITION además de VIEW SERVER STATE.  
  
 Para detener (KILL) un proceso, el usuario debe ser miembro de los roles fijos de servidor sysadmin o processadmin.  
  
  
## <a name="open-activity-monitor"></a>Abrir el Monitor de actividad  

### <a name="keyboard-shortcut"></a>Métodos abreviados de teclado  
 - Presione **CTRL+ALT+A** para abrir el Monitor de actividad en cualquier momento.

 >**Sugerencia** Mantenga el puntero del mouse sobre cualquier icono en SSMS para saber qué es y qué método abreviado de teclado lo activa.

### <a name="toolbar"></a>Barra de herramientas

En la barra de herramientas estándar, haga clic en el icono **Monitor de actividad** . Este icono se encuentra en el medio, justo a la derecha de los botones Deshacer/rehacer.
![Activity_Monitor_icon](../../relational-databases/performance-monitor/media/activity-monitor-icon.png)  
  
Complete el cuadro de diálogo **Conectar con el servidor** si todavía no está conectado a una instancia de SQL Server que desea supervisar.
  
## <a name="launch-activity-monitor-and-object-explorer-on-startup"></a>Iniciar el Monitor de actividad y el Explorador de objetos en el inicio
  
1.  En el menú **Herramientas** , haga clic en **Opciones**.  
  
2.  En el cuadro de diálogo **Opciones** , expanda **Entorno**y, luego, seleccione **Inicio**.  
  
3.  En la lista desplegable **Al inicio** , seleccione **Abrir el Explorador de objetos y el Monitor de actividad**.  

4.  Haga clic en **OK**.

![open_object_explorer](../../relational-databases/performance-monitor/media/open-object-explorer.png)
  
  
## <a name="set-the-activity-monitor-refresh-interval"></a>Establecer el intervalo de actualización del Monitor de actividad  
  
1.   Abra el Monitor de actividad.  
  
2.   Haga clic con el botón derecho en **Información general**, seleccione **Intervalo de actualización**y después seleccione el intervalo en el que el Monitor de actividad debería obtener nueva información de la instancia.  
  
  
