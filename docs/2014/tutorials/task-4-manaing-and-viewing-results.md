---
title: 'Tarea 4: Administrar y ver resultados | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: ecc3ba7e-fecf-478f-8825-6e4764b00e99
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c298daa69c57c7771787c181cc0087927ff83f68
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48163505"
---
# <a name="task-4-manaing-and-viewing-results"></a>Tarea 4: administrar y ver los resultados
  En esta tarea, revisará los resultados de la limpieza asistida por PC y realizará la limpieza interactiva de los datos de proveedor. Consulte [fase de limpieza interactiva](http://msdn.microsoft.com/library/hh213061.aspx#Interactive) para obtener más detalles.  
  
1.  Seleccione **correo electrónico de contacto** dominio en la lista de dominios.  
  
2.  Cambie a la **válido** ficha en el panel derecho. Observe que en dos direcciones de correo electrónico faltaba el carácter 's' al final. Estos dos correos electrónicos que se han encontrado no es válido por la regla de dominio que requiere que todas las direcciones de correo electrónico terminen con **@adventure-works.com** (del '). DQS emplea la regla de dominio durante la limpieza para determinar si una dirección de correo electrónico es válida o no. Esta pestaña muestra los valores de dominio que se marcaron como no válidos en la base de conocimiento o que no cumplieron una regla de dominio. En este caso, estos valores no cumplieron en la regla de dominio (Validación de correo electrónico).  
  
3.  En el **corregir a** columna, escriba el correo electrónico adecuado de direcciones que finalicen con **@adventure-works.com** (del ').  
  
     ![Correcciones de la regla de validación de correo electrónico](../../2014/tutorials/media/et-managingandviewingresults-01.jpg "correcciones de la regla de validación de correo electrónico")  
  
4.  Haga clic en **aprobar** para ambos registros aprobar ambos cambios. Cuando apruebe, mover los registros a la **corregido** ficha. En lugar de aprobar cada elemento por separado, puede aprobar todos los cambios a la vez mediante la **aprobar todos los términos** botón de barra de herramientas.  
  
5.  Cambie a la **New** ficha en el panel derecho. Los valores de esta pestaña son aquellos para los que DQS no tiene todavía suficiente información en la base de conocimiento para determinar si son correctos o no. Por tanto, no puede cambiar ni sugerir cambios a los valores de dominio.  
  
6.  Revise los valores para confirmar que todos los correos electrónicos acaban **@adventure-works.com** y haga clic en **aprobar todos los términos** en la barra de herramientas. Los valores aprobados de esta pestaña se mueven a la **correcto** ficha.  
  
7.  Seleccione el **país** dominio en la lista de dominios.  
  
8.  Cambie a la **corregido** pestaña en el panel derecho y observe que **United State** se corrige automáticamente el valor para el **Estados Unidos** del "al final. Esta regla no es una regla que se ha definido para el **país** dominio, pero DQS está **83%** seguro de que el valor correcto es **Estados Unidos**. El **aprobar** botón se selecciona automáticamente para todos los **corregido** elementos. Puede invalidar este comportamiento y rechazar un cambio.  
  
9. Tenga en cuenta que **EE.UU.** se ha corregido a **Estados Unidos** porque son sinónimos y **Estados Unidos** es el valor inicial (preferido).  
  
     ![Correcciones basadas en sinónimos](../../2014/tutorials/media/et-managingandviewingresults-02.jpg "correcciones basadas en sinónimos")  
  
10. Tenga en cuenta que el **aprobar** ya está seleccionado el botón para estos valores corregidos. Este comportamiento es el predeterminado para los valores corregidos. Puede rechazar un cambio y al hacerlo, el valor se desplaza a la **válido** ficha.  
  
11. Seleccione **Supplier Name** en la lista de dominios.  
  
12. Cambie a la **corregido** ficha en el panel derecho.  
  
     ![Nombres de proveedores corregidos](../../2014/tutorials/media/et-managingandviewingresults-03.jpg "nombres de proveedores corregidos")  
  
    1.  Tenga en cuenta que **A. Datum Corp.** se ha corregido a **A. Datum Corporation** y **motivo** está establecido en **relación basada en términos. A. datum Corporation** es un valor de dominio conocido para DQS porque se detectó durante el proceso de detección de conocimiento. Por lo tanto, DQS es **100% seguro** sobre esta corrección.  
  
    2.  Tenga en cuenta que **Lazy Country Storex** se ha corregido a **Lazy Country Store**, **un nivel de confianza** está establecido en **100%** y el  **Motivo** está establecido en **valor de dominio**. Durante el proceso de detección de conocimiento, establecer **Lazy Country Storex** como un error con **Lazy Country Store** como el **corrección**, por lo que DQS es **100% seguro** sobre esta corrección.  
  
    3.  DQS no está familiarizado con los otros valores en la lista, pero encontró correcciones para estos valores con el **corrector ortográfico** y propone las correcciones correspondientes. DQS es **no al 100%** inspira estas correcciones, pero el nivel de confianza es superior al 80%, que es el nivel de umbral para hacer correcciones, por lo que DQS propone las correcciones.  
  
13. Tenga en cuenta que el **aprobar** se habilita automáticamente para todos los valores. Puede invalidar el valor corregido o rechazar el cambio según corresponda. De forma predeterminada el **aprobar** botón está seleccionado para todos los valores en el **corregido** ficha.  
  
14. Cambie a la **New** ficha.  
  
15. Tenga en cuenta que **Corp.** se ha corregido a **Corporation**, **Co.** se ha corregido a **empresa**, y **Inc.** se ha corregido a **Incorporated**. Por ejemplo, **Consolidate Inc.** se ha corregido a **Consolidate Incorporated** y **Consolidated Co.** se ha corregido a **Consolidated Company**, y **Frabrikam Corp.** se ha corregido a **Fabrikam Corporation**.  Puede ver que **relación basada en términos** se menciona el motivo. Para proponer estos cambios se usan las relaciones basadas en términos que definió durante la actividad de administración de dominios. Puede cambiar el **corregir a** manualmente aquí los valores.  
  
16. Desplácese por la lista para ver **Hunxgry Coyote Store** con una línea ondulada roja. Haga doble clic en él y haga clic en **Hungy Coyote Store** (con ningún ' x'). El **corregir a** columna debe rellenarse automáticamente con **Hungry Coyote Store**. También puede escribir manualmente un valor en la columna Corregir a.  
  
17. Haga clic en **aprobar todos los términos** desde la barra de herramientas. Los valores de dominio con el **corregir a** mover el valor especificado para el **corregido** ficha y los nuevos valores no asociados **corregir a** los valores que se mueven a la  **Correcto** ficha.  
  
18. Seleccione el **validación de direcciones** dominio compuesto en la lista de dominios.  
  
19. En el panel derecho, cambie a la **correcto** ficha. Debería ver las direcciones que se encuentran correctas el **Melissa Data – Address Check** DQS de servicio en la **Azure Marketplace**.  
  
20. Cambie a la **corregido** ficha.  
  
21. Tenga en cuenta que **estado** para el registro que tiene **Ciudad** como **Los Ángeles** está establecido en **CA** ahora. Observe que en el **motivo** campo es que **corregido por la regla 'Regla ciudad-estado'**.  
  
     ![Corrección de regla ciudad-estado](../../2014/tutorials/media/et-managingandviewingresults-04.jpg "corrección a la regla Ciudad-Estado")  
  
22. Tenga en cuenta que el **aprobar** ya está seleccionado el botón de radio para este elemento en la lista. Este es el comportamiento predeterminado para los elementos en el **corregido** ficha.  
  
23. Cambie a la **sugerido** ficha. Revise los cambios sugeridos por la **Melissa Data – Address Check** service.  
  
24. **Haga clic en aprobar todos los términos** en el botón de barra de herramientas y haga clic en **Aceptar** en el **confirmación** cuadro de mensaje.  
  
     ![Botón de barra de herramientas de todos los términos aprobar](../../2014/tutorials/media/et-managingandviewingresults-05.jpg "aprobar el botón de barra de herramientas de todos los términos")  
  
25. Haga clic en **siguiente** para cambiar a la **exportar** página.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 5: Exportar los resultados de la limpieza a un archivo de Excel](../../2014/tutorials/task-5-exporting-cleansing-results-to-an-excel-file.md)  
  
  
