---
title: 'Tarea 4: Configurar reglas de dominio | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3a7162ba-cf2f-481f-830d-bb6a02823827
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 89e0027b3bf1748fb68a8b6922c45572a7b41bb7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109123"
---
# <a name="task-4-setting-domain-rules"></a>Tarea 4: configurar reglas de dominio
  En esta tarea, crear una regla para la **correo electrónico de contacto** dominio para comprobar si la dirección de correo electrónico termina con **@adventure-works.com**. Vea el tema [Crear una regla de dominio](http://msdn.microsoft.com/library/hh510397.aspx) para obtener más detalles sobre la página.  
  
1.  Haga clic en **Correo electrónico de contacto** en la lista **Dominio**.  
  
2.  Cambie a la pestaña **Reglas de dominio** en el panel derecho.  
  
     ![Agregue un nuevo botón de barra de herramientas de regla de dominio](../../2014/tutorials/media/et-settingdomainrules-01.jpg "agregar un nuevo botón de barra de herramientas de regla de dominio")  
  
3.  En el panel derecho, haga clic en el botón **Agregar una nueva regla de dominio** de la barra de herramientas (vea la imagen) para agregar una regla.  
  
4.  Escriba **Validación de correo electrónico** como **Nombre de regla** y presione **ENTRAR**. La casilla **Activa** debe estar activada de forma predeterminada. Este control le permite desactivar una regla temporalmente.  
  
5.  En el panel **Generar una regla** , haga clic en la **flecha abajo**y seleccione **El valor termina por**.  
  
6.  Tipo de **@adventure-works.com** en el cuadro de texto y presione **ficha**. Puede agregar más condiciones si hace clic en el botón **Agregar una nueva condición a la cláusula seleccionada** de la barra de herramientas del panel **Generar una regla** .  
  
     ![Regla de validación de correo electrónico](../../2014/tutorials/media/et-settingdomainrules-02.jpg "regla de validación de correo electrónico")  
  
7.  Haga clic en el botón **Ejecutar la regla de dominio seleccionada en los datos de prueba** de la barra de herramientas del panel derecho para probar la regla con datos de ejemplo.  
  
     ![Ejecutar la regla de dominio en el botón de barra de herramientas de datos de prueba](../../2014/tutorials/media/et-settingdomainrules-03.jpg "ejecutar la regla de dominio en el botón de barra de herramientas de datos de prueba")  
  
8.  En el cuadro de diálogo **Probar regla de dominio** , haga clic en el botón **Agrega un nuevo término de prueba para la regla de dominio** de la barra de herramientas.  
  
     ![Probar cuadro de diálogo regla de dominio](../../2014/tutorials/media/et-settingdomainrules-04.jpg "Probar cuadro de diálogo regla de dominio")  
  
9. Tipo de **frank7@adventure-works.com** (un valor válido) en la **correo electrónico de contacto** columna.  
  
10. Repita los dos pasos anteriores para agregar **joe2@adventure-work.com** (un valor no válido y no tienen ninguna del ').  
  
11. Haga clic en el último botón (**Probar la regla de dominio en todos los términos**) de la barra de herramientas para probar los datos de entrada con la regla.  
  
     ![Probar la regla de dominio en el botón de barra de herramientas de todos los términos](../../2014/tutorials/media/et-settingdomainrules-05.jpg "probar la regla de dominio en el botón de barra de herramientas de todos los términos")  
  
12. Observe que la primera entrada se muestra como un elemento válido y el segundo como un elemento no válido.  
  
     ![Probar los resultados de la regla de dominio](../../2014/tutorials/media/et-settingdomainrules-06.jpg "probar los resultados de la regla de dominio")  
  
13. Haga clic en **Cerrar** para cerrar el cuadro de diálogo **Probar regla de dominio** .  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 5: Configurar basadas en términos relaciones](../../2014/tutorials/task-5-setting-term-based-relationships.md)  
  
  