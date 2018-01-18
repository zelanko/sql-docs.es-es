---
title: "Ver el registro de aplicación de Windows | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application logs [SQL Server]
- Windows application logs [SQL Server]
- viewing Windows application logs
- errors [SQL Server], logs
- system logs [SQL Server]
- security logs [SQL Server]
- displaying Windows application logs
- logs [SQL Server], Windows application logs
ms.assetid: f9853b74-7db7-47cc-b957-e49ed5bc0a1a
caps.latest.revision: "20"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ca57e59ba3c8e837e9a03bfd313ad20b9e3ec4f
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="viewing-the-windows-application-log"></a>Ver el registro de la aplicación Windows
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para utilizar el registro de aplicación de Microsoft Windows, cada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sesión escribe eventos nuevos en dicho registro. A diferencia del registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no se crea un nuevo registro de aplicación cada vez que se inicia una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para ver y administrar el registro de la aplicación Windows, utilice el Visor de eventos de Windows o el Visor de registros de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Con el Visor de eventos se pueden ver tres registros.  
  
|Tipo de registro de Windows|Description|  
|----------------------|-----------------|  
|Registro del sistema|Registra los eventos registrados por los componentes del sistema operativo Windows. Por ejemplo, el error al cargar un controlador u otro componente del sistema durante el inicio se graba en el registro del sistema.|  
|Registro de seguridad|Registra eventos de seguridad, como los errores en intentos de inicios de sesión. Esto ayuda a realizar un seguimiento de los cambios en el sistema de seguridad y a identificar las posibles infracciones en la seguridad. Por ejemplo, los intentos de iniciar una sesión en el sistema se pueden grabar en este registro, según la configuración de auditorías del Administrador de usuarios.<br /><br /> Solo los miembros del rol fijo de servidor **sysadmin** pueden ver el registro de seguridad.|  
|Registro de la aplicación|Graba los eventos registrados por las aplicaciones. Por ejemplo, una aplicación de bases de datos puede registrar un error en un archivo en el registro de aplicación.|  
  
 Para obtener más información acerca de cómo utilizar el Visor de eventos, administrar el registro de la aplicación y entender la información que contiene, vea la documentación de Windows.  
  
 **Para ver el registro de aplicación Windows**  
  
 [Ver el registro de aplicación de Windows &#40;Windows&#41;](../../relational-databases/performance/view-the-windows-application-log-windows-10.md)  
  
  
