---
title: 'Tarea 3: importar valores de dominio desde un archivo de Excel | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 242e8309-1195-495b-9cd5-aa127748c185
ms.author: lle
author: lrtoyou1223
ms.openlocfilehash: 36c34be6d994c543eb17f8c923fcf62c0fdd53d4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78177275"
---
# <a name="task-3-importing-domain-values-from-an-excel-file"></a>Tarea 3: Importación de valores de dominio desde un archivo de Excel

  En esta tarea, importará valores para el dominio **Estado** desde una hoja de cálculo de un archivo de Excel.

1.  Haga clic en el dominio **Estado** en la lista **Dominio**.

2.  Asegúrese de que la pestaña **Valores del dominio** esté activa en el panel derecho.

3.  En el panel derecho, en la barra de herramientas, haga clic en la **flecha abajo** situada junto al botón **Importar valores** y, a continuación, haga clic en **Importar valores válidos desde Excel**.

     ![Importar valores válidos del menú Excel](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-01.jpg "Importar valores válidos del menú Excel")

4.  Haga clic en **Examinar**, seleccione **Suppliers.xls**y haga clic en **Abrir**.

5.  Seleccione **StatesToImport$** en **Hoja de cálculo**.

     ![Cuadro de diálogo Importar valores de dominio](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-02.jpg "Cuadro de diálogo Importar valores de dominio")

6.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Importar valores del dominio** . Debe ver todos los nombres de los estados que importó en la lista. Observe que la opción **Mostrar solo nuevo** está seleccionada automáticamente después de la importación. Al importar valores y no ve los valores anteriores en la lista, es porque esta opción se habilita automáticamente después de la importación. Para ver todos los valores, desactive la casilla. Si importa de nuevo el mismo conjunto de valores, no se importa ninguno de los valores porque ya existen en el dominio.

     ![Mostrar solamente nueva casilla en valores de dominio](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-03.jpg "Mostrar solamente nueva casilla en valores de dominio")

## <a name="next-step"></a>siguiente paso
 [Tarea 4: Configuración de reglas de dominio](../../2014/tutorials/task-4-setting-domain-rules.md)


