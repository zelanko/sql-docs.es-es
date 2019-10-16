---
title: 'Tarea 4: establecer reglas de dominio | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3a7162ba-cf2f-481f-830d-bb6a02823827
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: dd59bf315e90bd52ba1388d27c533ab4a3136d3c
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381742"
---
# <a name="task-4-setting-domain-rules"></a>Tarea 4: configurar reglas de dominio
  En esta tarea, creará una regla para el dominio de **correo electrónico de contacto** para comprobar si la dirección de correo electrónico termina con **@no__t 2adventure-Works.com**. Vea el tema [Crear una regla de dominio](https://msdn.microsoft.com/library/hh510397.aspx) para obtener más detalles sobre la página.  
  
1.  Haga clic en **Correo electrónico de contacto** en la lista **Dominio**.  
  
2.  Cambie a la pestaña **Reglas de dominio** en el panel derecho.  
  
     ![Botón de la barra de herramientas agregar nueva regla de dominio](../../2014/tutorials/media/et-settingdomainrules-01.jpg "Botón de la barra de herramientas agregar nueva regla de dominio")  
  
3.  En el panel derecho, haga clic en el botón **Agregar una nueva regla de dominio** de la barra de herramientas (vea la imagen) para agregar una regla.  
  
4.  Escriba **Validación de correo electrónico** como **Nombre de regla** y presione **ENTRAR**. La casilla **Activa** debe estar activada de forma predeterminada. Este control le permite desactivar una regla temporalmente.  
  
5.  En el panel **Generar una regla** , haga clic en la **flecha abajo**y seleccione **El valor termina por**.  
  
6.  Escriba **\@adventure-Works.com** en el cuadro de texto y presione **Tab**. Puede agregar más condiciones si hace clic en el botón **Agregar una nueva condición a la cláusula seleccionada** de la barra de herramientas del panel **Generar una regla** .  
  
     ![Regla de validación de correo electrónico](../../2014/tutorials/media/et-settingdomainrules-02.jpg "Regla de validación de correo electrónico")  
  
7.  Haga clic en el botón **Ejecutar la regla de dominio seleccionada en los datos de prueba** de la barra de herramientas del panel derecho para probar la regla con datos de ejemplo.  
  
     ![Botón de la barra de herramientas ejecutar la regla de dominio en los datos de prueba](../../2014/tutorials/media/et-settingdomainrules-03.jpg "Botón de la barra de herramientas ejecutar la regla de dominio en los datos de prueba")  
  
8.  En el cuadro de diálogo **Probar regla de dominio** , haga clic en el botón **Agrega un nuevo término de prueba para la regla de dominio** de la barra de herramientas.  
  
     ![Cuadro de diálogo probar regla de dominio](../../2014/tutorials/media/et-settingdomainrules-04.jpg "Cuadro de diálogo probar regla de dominio")  
  
9. Escriba **frank7\@adventure-works.com** (un valor válido) en la columna **correo electrónico de contacto** .  
  
10. Repita los dos pasos anteriores para agregar **joe2\@adventure-work.com** (un valor no válido sin ') '.  
  
11. Haga clic en el último botón (**Probar la regla de dominio en todos los términos**) de la barra de herramientas para probar los datos de entrada con la regla.  
  
     ![Botón de la barra de herramientas probar la regla de dominio en todos los términos](../../2014/tutorials/media/et-settingdomainrules-05.jpg "Botón de la barra de herramientas probar la regla de dominio en todos los términos")  
  
12. Observe que la primera entrada se muestra como un elemento válido y el segundo como un elemento no válido.  
  
     ![Resultados de la regla de dominio de prueba](../../2014/tutorials/media/et-settingdomainrules-06.jpg "Resultados de la regla de dominio de prueba")  
  
13. Haga clic en **Cerrar** para cerrar el cuadro de diálogo **Probar regla de dominio** .  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 5: Configurar relaciones basadas en términos](../../2014/tutorials/task-5-setting-term-based-relationships.md)  
  
  
