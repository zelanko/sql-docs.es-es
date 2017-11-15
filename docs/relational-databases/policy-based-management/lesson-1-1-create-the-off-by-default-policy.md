---
title: "Creación de la directiva Desactivado de forma predeterminada | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 98fde3c5-297c-4d95-981e-95700bbf5ccd
caps.latest.revision: "28"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 09e14b3302594f7829a72786dc1f13b42fcb2c51
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-1-1---create-the-off-by-default-policy"></a>Lección 1-1: Crear la directiva Desactivado de forma predeterminada
Esta tarea crea una condición denominada Correo desactivado que se basa en la faceta Configuración de área expuesta. A continuación, crea una directiva denominada Desactivado de forma predeterminada.  
  
### <a name="to-create-the-mail-off-condition"></a>Para crear la condición Correo desactivado  
  
1.  En el Explorador de objetos, expanda **Administración**, **Administración de directivas**y **Facetas**, haga clic con el botón derecho en **Configuración de área expuesta**y, después, haga clic en **Nueva condición**.  
  
2.  En el cuadro de diálogo **Crear nueva condición** , en el cuadro **Nombre** , escriba **Correo desactivado**.  
  
3.  En el cuadro **Faceta** , confirme que está seleccionada la faceta **Configuración de área expuesta** .  
  
4.  En el cuadro de diálogo **Expresión** , en el cuadro **Campo** , seleccione **@DatabaseMailEnabled**, en el cuadro **Operador** seleccione **=**y en **Valor** seleccione **False**.  
  
5.  En la página **Descripción** , escriba la descripción de la condición y luego haga clic en **Aceptar** para crear la condición.  
  
### <a name="to-create-the-off-by-default-policy"></a>Para crear la directiva Desactivado de forma predeterminada  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en **Configuración de área expuesta**y, después, haga clic en **Nueva directiva**.  
  
2.  En el cuadro de diálogo **Crear nueva directiva** , en el cuadro **Nombre** , escriba **Desactivado de forma predeterminada**.  
  
3.  Deje desactivada la casilla **Habilitado** . La casilla **Habilitado** se aplica a las directivas automatizadas y esta directiva se ejecutará a petición.  
  
4.  En la casilla **Condición de comprobación** , desplácese hacia abajo hasta el área **Configuración de área expuesta** y luego seleccione **Correo desactivado** como condición para comprobar.  
  
5.  El cuadro **Para destinos** estará en blanco porque se trata de una directiva con ámbito de servidor.  
  
6.  En la casilla **Modo de evaluación** , seleccione **A petición** .  
  
7.  En la casilla **Restricción de servidor** , seleccione **Ninguna**.  
  
8.  En la página **Descripción** , escriba la descripción de la directiva.  
  
9. Puede proporcionar un hipervínculo a una página web para las directivas en el área **Hipervínculo de ayuda adicional** . En el cuadro **Texto para mostrar** , escriba el texto que aparecerá para el hipervínculo.  
  
10. En el cuadro **Dirección** , escriba un hipervínculo a una página de Ayuda, por ejemplo, la página principal del departamento de IT de la compañía.  
  
11. Para confirmar la dirección y abrir la página web, haga clic en **Probar vínculo**.  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Configurar un servidor para ejecutar la directiva Desactivado de forma predeterminada](../../relational-databases/policy-based-management/lesson-1-2-configure-a-server-to-run-the-off-by-default-policy.md)  
  
  
  
