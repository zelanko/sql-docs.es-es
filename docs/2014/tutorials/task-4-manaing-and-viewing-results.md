---
title: 'Tarea 4: administrar y ver los resultados | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ecc3ba7e-fecf-478f-8825-6e4764b00e99
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8b97b0129a7cc4ffa21b4a82ad0208a2c1890b27
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313644"
---
# <a name="task-4-manaing-and-viewing-results"></a>Tarea 4: administrar y ver los resultados
  En esta tarea, revisará los resultados de la limpieza asistida por PC y realizará la limpieza interactiva de los datos de proveedor. Vea [fase de limpieza interactiva](https://msdn.microsoft.com/library/hh213061.aspx#Interactive) para obtener más detalles.  
  
1.  Seleccione dominio de **correo electrónico de contacto** en la lista de dominios.  
  
2.  Cambie a la pestaña **no válido** en el panel derecho. Observe que dos direcciones de correo electrónico a las que les faltaba el carácter ' al final. Estos dos correos electrónicos que se han detectado que no son válidos por la regla de dominio que requiere que todas las direcciones de correo electrónico terminen con **\@Adventure-Works.com** (con ' es '). DQS emplea la regla de dominio durante la limpieza para determinar si una dirección de correo electrónico es válida o no. Esta pestaña muestra los valores de dominio que se marcaron como no válidos en la base de conocimiento o que no cumplieron una regla de dominio. En este caso, estos valores no cumplieron en la regla de dominio (Validación de correo electrónico).  
  
3.  En la columna **corregir a** , escriba la dirección de correo electrónico adecuada que termine con **\@Adventure-Works.com** (con ' es ').  
  
     ![Correcciones de las correcciones de reglas de validación de correo electrónico](../../2014/tutorials/media/et-managingandviewingresults-01.jpg "de la regla de validación de correo electrónico")  
  
4.  Haga clic en **aprobar** para ambos registros con el fin de aprobar ambos cambios. Al aprobar, los registros se mueven a la pestaña **corregido** . En lugar de aprobar cada elemento por separado, puede aprobar todos los cambios a la vez mediante el botón de la barra de herramientas **aprobar todos los términos** .  
  
5.  Cambie a la **nueva** pestaña en el panel derecho. Los valores de esta pestaña son aquellos para los que DQS no tiene todavía suficiente información en la base de conocimiento para determinar si son correctos o no. Por tanto, no puede cambiar ni sugerir cambios a los valores de dominio.  
  
6.  Revise los valores para confirmar que todos los mensajes de correo electrónico terminan con **\@Adventure-Works.com** y haga clic en **aprobar todos los términos** en la barra de herramientas. Los valores aprobados de esta pestaña se mueven a la pestaña **correcto** .  
  
7.  Seleccione el dominio de **país** en la lista de dominios.  
  
8.  Cambie a la pestaña **corregido** en el panel derecho y observe que el valor de **Estados Unidos** se corrige automáticamente en el **Estados Unidos** con ' de ' al final. Esta regla no es una regla que haya definido para el dominio **Country** , pero DQS es **83%** de confianza de que el valor correcto es **Estados Unidos**. El botón **aprobar** se selecciona automáticamente para todos los elementos **corregidos** . Puede invalidar este comportamiento y rechazar un cambio.  
  
9. Tenga en cuenta que **usa** se corrige para **Estados Unidos** porque son sinónimos y **Estados Unidos** es el valor inicial (preferido).  
  
     ![Correcciones basadas en](../../2014/tutorials/media/et-managingandviewingresults-02.jpg "correcciones de sinónimos basadas en sinónimos")  
  
10. Tenga en cuenta que el botón **aprobar** ya está seleccionado para estos valores corregidos. Este comportamiento es el predeterminado para los valores corregidos. Puede rechazar un cambio y, al hacerlo, el valor se desplaza a la pestaña **no válido** .  
  
11. Seleccione **nombre de proveedor** en la lista de dominios.  
  
12. Cambie a la pestaña **corregido** en el panel derecho.  
  
     Nombres de ![proveedores corregidos](../../2014/tutorials/media/et-managingandviewingresults-03.jpg "corregidos nombres de proveedor")  
  
    1.  Observe que **a. Datum Corp.** se ha corregido a **. Datum Corporation** y el **motivo** se establece en **relación basada en términos. A. Datum Corporation** es un valor de dominio conocido para DQS porque se detectó durante el proceso de detección de conocimiento. Por lo tanto, DQS es el **100% seguro** de esta corrección.  
  
    2.  Observe que **Lazy Country STOREX** se ha corregido a **Lazy Country Store**, el **nivel de confianza** está establecido en **100%** y el **motivo** está establecido en **valor de dominio**. Durante el proceso de detección de conocimiento, se establece **Lazy Country STOREX** como un error con **Lazy Country Store** como **corrección**, por lo que DQS está **100% seguro** de hacer esta corrección.  
  
    3.  DQS no está familiarizado con los demás valores de la lista, pero encontró las correcciones para estos valores mediante el **corrector ortográfico** y propone las correcciones correspondientes. DQS **no es 100%** seguro de estas correcciones, pero el nivel de confianza es superior al 80%, que es el nivel de umbral para la realización de correcciones, por lo que DQS propone las correcciones.  
  
13. Tenga en cuenta que la **aprobación** se habilita automáticamente para todos los valores. Puede invalidar el valor corregido o rechazar el cambio según corresponda. De forma predeterminada, se selecciona el botón **aprobar** para todos los valores de la pestaña **corregido** .  
  
14. Cambie a la pestaña **nuevo** .  
  
15. Observe que **Corp.** se ha corregido a **Corporation**, **Co.** se ha corregido a **Company**y **Inc.** se ha corregido a **Incorporated**. Por ejemplo, **ConsoliDate Inc.** se corrige para **consolidar el co incorporado** y el **Co consolidado.** se ha corregido a la **empresa consolidada**y **Frabrikam Corp.** se ha corregido a **Fabrikam Corporation**.  Puede ver que la **relación basada en términos** se menciona como el motivo. Para proponer estos cambios se usan las relaciones basadas en términos que definió durante la actividad de administración de dominios. Puede cambiar manualmente los valores **correctos a** .  
  
16. Desplácese por la lista para ver el **almacén de Hunxgry Coyote** con una línea ondulada roja. Haga clic con el botón derecho en él y haga clic en el **almacén de Coyote bloqueado** (sin "x"). La columna **corregir a** se debe rellenar automáticamente con el **almacén Coyote**. También puede escribir manualmente un valor en la columna Corregir a.  
  
17. Haga clic en **aprobar todos los términos** en la barra de herramientas. Los valores de dominio con el valor **correcto para** especificado se desplacen a la pestaña **corregida** y los nuevos valores sin valores **correctos asociados se** mueven a la pestaña **correcto** .  
  
18. Seleccione el dominio compuesto **validación de direcciones** en la lista de dominios.  
  
19. En el panel derecho, cambie a la pestaña **correcto** . Debería ver las direcciones que ha detectado que son correctas por el servicio de DQS de **comprobación de direcciones de datos Melissa** en **Azure Marketplace**.  
  
20. Cambie a la pestaña **corregido** .  
  
21. Observe que el **Estado** del registro que tiene **City** como los **Ángeles** está establecido en **CA** Now. Observe que en el campo **motivo** está **corregido por la regla "City-State Rule"** .  
  
     Ciudad: corrección de ![la regla de estado](../../2014/tutorials/media/et-managingandviewingresults-04.jpg "ciudad-corrección de la regla de estado")  
  
22. Tenga en cuenta que el botón de radio **aprobar** ya está seleccionado para este elemento en la lista. Este es el comportamiento predeterminado de los elementos de la pestaña **corregido** .  
  
23. Cambie a la pestaña **sugerido** . Revise los cambios que sugiere el servicio **Melissa Data-Address check** .  
  
24. **Haga clic en aprobar todos los términos** en el botón de la barra de herramientas y haga clic en **Aceptar** en el cuadro de mensaje de **confirmación** .  
  
     Botón de la barra de ![herramientas aprobar todos los términos]botón de la(../../2014/tutorials/media/et-managingandviewingresults-05.jpg "barra de herramientas aprobar todo término")  
  
25. Haga clic en **siguiente** para cambiar a la página **exportar** .  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 5: Exportar los resultados de la limpieza a un archivo de Excel](../../2014/tutorials/task-5-exporting-cleansing-results-to-an-excel-file.md)  
  
  
