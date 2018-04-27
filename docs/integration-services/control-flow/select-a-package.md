---
title: Seleccionar un paquete | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.selectapackage.f1
helpviewer_keywords:
- Select a Package dialog box
ms.assetid: 92b47a2b-21b5-460a-885d-6cc4bb567249
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5bf8cf86fce968150d94ef1893ebe34a2fa92c0b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="select-a-package"></a>Seleccionar un paquete
  Utilice el cuadro de diálogo **Seleccionar un paquete** para especificar el paquete desde el que la tarea Cola de mensajes puede recibir mensajes.  
  
## <a name="static-options"></a>Opciones estáticas  
 **Ubicación**  
 Especifique la ubicación del paquete. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Valor|Description|  
|-----------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Establezca la ubicación de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La selección de este valor muestra las opciones dinámicas, **Servidor**, **Utilizar autenticación de Windows**, **Utilizar autenticación de SQL Server**, **Nombre de usuario**y **Contraseña**.|  
|Archivo DTSX|Establezca la ubicación de un archivo DTSX. La selección de este valor muestra la opción dinámica **Nombre de archivo**.|  
  
## <a name="location-dynamic-options"></a>Opciones dinámicas de ubicación  
  
### <a name="location--sql-server"></a>Ubicación = SQL Server  
 **Nombre del paquete**  
 Seleccione un paquete que esté almacenado en el servidor especificado.  
  
 **Server**  
 Proporcione un nombre de servidor o seleccione un servidor de la lista.  
  
 **Utilizar autenticación de Windows**  
 Haga clic en esta opción para utilizar la autenticación de Windows.  
  
 **Utilizar autenticación de SQL Server**  
 Haga clic en esta opción para usar la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **User name**  
 Si está usando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , proporcione un nombre de usuario para usarlo cuando inicie sesión en el servidor.  
  
 **Contraseña**  
 Si está usando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , proporcione una contraseña.  
  
### <a name="location--dtsx-file"></a>Ubicación = archivo DTSX  
 **Nombre de archivo**  
 Proporcione la ruta de acceso a un paquete o haga clic en el botón Examinar **(…)** y busque el paquete.  
  
## <a name="see-also"></a>Ver también  
 [Tarea Cola de mensajes](../../integration-services/control-flow/message-queue-task.md)  
  
  
