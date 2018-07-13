---
title: 'Tarea 12: Adición de transformación columna derivada para agregar columnas necesarias en MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 98ccb271-04da-4126-9729-67e9a479aaef
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6d1bb94b040aee5ba1db6870edc71e3153a3c7a4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37165716"
---
# <a name="task-12-adding-derived-column-transform-to-add-columns-required-by-mds"></a>Tarea 12: agregar la transformación Columna derivada para agregar las columnas necesarias en MDS
  En esta tarea, agregará la transformación Columna derivada al flujo de datos. Agregar dos columnas derivadas, **ImportType** y **BatchTag**, a los registros pasados a esta transformación. Debe agregar estas columnas antes de cargar los datos en las tablas de ensayo en MDS. Son dos columnas necesarias para las tablas de ensayo en MDS. Consulte [tablas de ensayo de miembros hoja](http://msdn.microsoft.com/library/ee633854.aspx) para obtener más detalles.  
  
1.  Arrastrar y colocar **transformación columna derivada** desde **común** sección la **cuadro de herramientas de SSIS** a la **de flujo de datos** ficha.  
  
2.  Haga clic en **columna derivada** transformar en el **de flujo de datos** ficha y haga clic en **cambiar el nombre**. Tipo **agregar columnas necesarias en MDS** y presione **ENTRAR**.  
  
3.  Conectar **filtrar duplicados** a **agregar columnas necesarias en MDS** mediante el conector azul. Debería ver el **selección de entrada y salida** cuadro de diálogo.  
  
4.  En el **selección de entrada y salida** cuadro de diálogo, seleccione **registros únicos**y haga clic en **Aceptar**.  
  
     ![Cuadro de diálogo de selección de salida de entrada](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-01.jpg "salida cuadro de diálogo de selección de entrada")  
  
5.  Haga clic en **SSIS** en la barra de menú y haga clic en **Variables**.  
  
6.  En el **Variables** ventana, haga clic en **agregar Variable** en la barra de herramientas.  
  
     ![Ventana de Variables SSIS](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-02.jpg "ventana de Variables SSIS")  
  
7.  Tipo **ImportType** para el **nombre** y **2** para el **valor**. Debe especificar el valor 2 porque desea agregar dos miembros nuevos a una entidad en MDS. Para obtener más información acerca de este parámetro, vea [tabla de ensayo de miembros hoja](http://msdn.microsoft.com/library/ee633854.aspx).  
  
8.  Haga clic en **agregar Variable** nuevo botón de barra de herramientas.  
  
9. Tipo **BatchTag** para el **nombre**, seleccione **cadena** para el **tipo de datos**, y **EIMBatch** para el **Valor**. **BatchTag** es simplemente un nombre único para el lote que se va a enviar a MDS.  
  
10. En el **de flujo de datos** , haga doble clic **agregar columnas necesarias en MDS**.  
  
11. En el **Editor de transformación columna derivada** cuadro de diálogo el **cuadro de lista en el panel inferior**, tipo **ImportType** para el **nombre de columna derivada**.  
  
12. Expanda **Variables y parámetros** en el panel superior izquierdo, arrastrar y colocar **User:: importtype** a la **expresión** columna.  
  
     ![Derivado de Editor de transformación columna](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-03.jpg "derivados de Editor de transformación de columna")  
  
13. Tipo **BatchTag** en la siguiente fila de la **nombre de columna derivada**.  
  
14. Arrastrar y colocar **User:: batchtag** desde **Variables y parámetros** a la **expresión** columna.  
  
15. Haga clic en **Aceptar** para cerrar el **transformación columna derivada** cuadro de diálogo.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 13: Agregar el destino de OLE DB para escribir datos en la tabla de ensayo de MDS](../../2014/tutorials/task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table.md)  
  
  
