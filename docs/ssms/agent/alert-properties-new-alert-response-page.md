---
title: "Propiedades de alerta: Nueva alerta (página Respuesta) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.alert.response.f1
ms.assetid: 72daf008-f9ea-4077-b217-5048e7759d3e
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6a22ab0b483ff821408853b6b6c14d46047f0b39
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="alert-properties---new-alert-response-page"></a>Propiedades de alerta - Nueva alerta (página Respuesta)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use esta página para especificar el trabajo que quier ejecutar y obtener una lista de operadores a los que se notificará en respuesta a una alerta del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="options"></a>Opciones  
**Ejecutar trabajo**  
Habilita las opciones **Lista de trabajos**, **Nuevo trabajo** y **Ver trabajo** .  
  
**Nuevo trabajo**  
Abre el cuadro de diálogo **Nuevo trabajo** . Este botón no está disponible si la opción **Ejecutar trabajo** no está seleccionada.  
  
**Ver trabajo**  
Permite ver o modificar el trabajo seleccionado. Esta opción no está disponible si **Ejecutar trabajo** no está seleccionada.  
  
**Notificar a los operadores**  
Habilita los controles que le permiten agregar, quitar o cambiar operadores.  
  
**Lista de operadores**  
Enumera los operadores a los que se notificará cuando se produzca una alerta. Para especificar un método de notificación, seleccione la casilla **Correo electrónico**, **Buscapersonas**o **Net send** que aparece después del nombre del operador. Esta opción no está disponible si **Notificar a los operadores** no está seleccionada.  
  
**Correo electrónico**  
Utiliza el correo electrónico para notificar al operador.  
  
**Buscapersonas**  
Utiliza la dirección de correo electrónico del buscapersonas para notificar al operador.  
  
**Net send**  
Use **net send** para notificar al operador.  
  
**Nuevo operador**  
Muestra el cuadro de diálogo **Nuevo operador** , que se puede usar para crear un nuevo operador.  
  
**Ver operador**  
Muestra el cuadro de diálogo **Propiedades** para el operador seleccionado actualmente. Puede ver y modificar las propiedades del operador en el cuadro de diálogo **Propiedades del operador** .  
  
## <a name="see-also"></a>Vea también  
[Alertas](../../ssms/agent/alerts.md)  
[Create an Alert Using Severity Level](../../ssms/agent/create-an-alert-using-severity-level.md)  
[Alertas](../../ssms/agent/alerts.md)  
[Edit an Alert](../../ssms/agent/edit-an-alert.md)  
[Delete an Alert](../../ssms/agent/delete-an-alert.md)  
  
