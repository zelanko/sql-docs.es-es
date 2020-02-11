---
title: Seleccionar un paquete | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.selectapackage.f1
helpviewer_keywords:
- Select a Package dialog box
ms.assetid: 92b47a2b-21b5-460a-885d-6cc4bb567249
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 026c588f2fc35a6cb256a63046ad91e5d1b5641a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62830252"
---
# <a name="select-a-package"></a>Seleccionar un paquete
  Utilice el cuadro de diálogo **Seleccionar un paquete** para especificar el paquete desde el que la tarea Cola de mensajes puede recibir mensajes.  
  
## <a name="static-options"></a>Opciones estáticas  
 **Ubicación**  
 Especifique la ubicación del paquete. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Descripción|  
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
  
 **Nombre de usuario**  
 Si está usando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , proporcione un nombre de usuario para usarlo cuando inicie sesión en el servidor.  
  
 **Contraseña**  
 Si está usando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , proporcione una contraseña.  
  
### <a name="location--dtsx-file"></a>Ubicación = archivo DTSX  
 **Nombre de archivo**  
 Proporcione la ruta de acceso a un paquete, o bien haga clic en el botón Examinar **(…)** y busque el paquete.  
  
## <a name="see-also"></a>Consulte también  
 [Tarea Cola de mensajes](message-queue-task.md)  
  
  
