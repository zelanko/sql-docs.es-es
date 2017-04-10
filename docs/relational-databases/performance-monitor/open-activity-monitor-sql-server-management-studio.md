---
title: "Abrir el Monitor de actividad (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "08/05/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Monitor de actividad [SQL Server], establecer el intervalo de actualización"
  - "intervalo de actualización del Monitor de actividad"
  - "Monitor de actividad [SQL Server], abrir"
  - "opening Activity Monitor"
ms.assetid: 0a6eeb16-f02b-479d-9a60-543e40ebf46b
caps.latest.revision: 38
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 38
---
# Abrir el Monitor de actividad (SQL Server Management Studio)

   
 El Monitor de actividad ejecuta consultas en la instancia supervisada para obtener información de sus paneles de información. Cuando el intervalo de actualización se establece en menos de 10 segundos, el tiempo utilizado para ejecutar estas consultas puede afectar al rendimiento del servidor  
  
  
##  <a name="Permissions"></a> Compruebe los permisos.  
 Para ver la actividad real, debe tener el permiso VIEW SERVER STATE. Para ver la sección de E/S de archivo de datos del Monitor de actividad, debe tener permisos CREATE DATABASE, ALTER ANY DATABASE o VIEW ANY DEFINITION además de VIEW SERVER STATE.  
  
 Para detener (KILL) un proceso, el usuario debe ser miembro de los roles fijos de servidor sysadmin o processadmin.  
  
  
## Abrir el Monitor de actividad  

### Método abreviado de teclado  
 - Presione **CTRL+ALT+A** para abrir el Monitor de actividad en cualquier momento.

 >**Sugerencia** Mantenga el puntero del mouse sobre cualquier icono en SSMS para saber qué es y qué método abreviado de teclado lo activa.

### Barra de herramientas

En la barra de herramientas estándar, haga clic en el icono **Monitor de actividad**. Este icono se encuentra en el medio, justo a la derecha de los botones Deshacer/rehacer.
![Activity_Monitor_icon](../../relational-databases/performance-monitor/media/activity-monitor-icon.png)  
  
Complete el cuadro de diálogo **Conectar con el servidor** si todavía no está conectado a una instancia de SQL Server que desea supervisar.
  
## Iniciar el Monitor de actividad y el Explorador de objetos en el inicio
  
1.  En el menú **Herramientas** , haga clic en **Opciones**.  
  
2.  En el cuadro de diálogo **Opciones**, expanda **Entorno** y, luego, seleccione **Inicio**.  
  
3.  En la lista desplegable **Al inicio**, seleccione **Abrir el Explorador de objetos y el Monitor de actividad**.  

4.  Haga clic en **Aceptar**.
  
![open_object_explorer](../../relational-databases/performance-monitor/media/open-object-explorer.png)
  
  
## Establecer el intervalo de actualización del Monitor de actividad  
  
1.   Abra el Monitor de actividad.  
  
2.   Haga clic con el botón derecho en **Información general**, seleccione **Intervalo de actualización** y después seleccione el intervalo en el que el Monitor de actividad debería obtener nueva información de la instancia.  
  
  