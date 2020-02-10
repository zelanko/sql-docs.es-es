---
title: 'Tarea 4 (opcional): combinar, buscar coincidencias y publicar un conjunto de datos nuevo | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13a13f03-b307-4555-8e33-6d98c459d994
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2d27a5bcd87ffd84b33de229d955dc9494846a72
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489271"
---
# <a name="task-4-optional-combining-matching-and-publishing-new-set-of-data"></a>Tarea 4 (opcional): combinar, buscar coincidencias y publicar un conjunto de datos nuevo
  Con el tiempo, le interesará agregar más datos al repositorio MDS. Antes de agregar datos, puede ser útil comparar los nuevos datos con los datos que ya se administran en MDS, para asegurarse de que no se agregan datos duplicados o inexactos. En el complemento Master Data Services para Excel, puede combinar datos de dos hojas de cálculo y comparar los datos para identificar y quitar duplicados antes de publicar los datos en MDS. La característica de búsqueda de coincidencias del complemento MDS para Excel emplea la funcionalidad de coincidencia de DQS para identificar coincidencias en los datos. En esta tarea, combinará datos de dos hojas de cálculo en una y después buscará coincidencias para identificar y quitar duplicados antes de publicar los datos en MDS. Vea [coincidencia de calidad de datos en los temas complemento MDS para Excel](https://msdn.microsoft.com/library/hh548681.aspx) y [combinar datos](https://msdn.microsoft.com/library/hh548680.aspx) para obtener más detalles.  
  
1.  Inicie una nueva instancia de **Excel**. Haga clic en **Inicio**, seleccione **Ejecutar**, escriba **Excel**y haga clic en **Aceptar**.  
  
2.  Cambie a la pestaña **datos maestros** haciendo clic en **datos maestros** en la barra de menús.  
  
3.  Haga clic en **conectar** en la cinta de opciones del grupo **conectar y cargar** para conectarse al **servidor MDS**. Ha configurado esta conexión anteriormente en esta lección.  
  
     ![Excel - Botón Mostrar explorador de la pestaña Datos maestros](../../2014/tutorials/media/et-combinematchandpublishnewsod-01.jpg "Excel - Botón Mostrar explorador de la pestaña Datos maestros")  
  
4.  Debería ver el panel de **Explorador de datos maestro** a la derecha. Si no ve el Explorador de datos maestro, haga clic en el botón **Mostrar explorador** de la cinta de opciones.  
  
5.  En la ventana de **Explorador de datos maestra** , seleccione **proveedores** en la lista desplegable del **modelo**. Debería ver que el modelo tiene una entidad: **Supplier**.  
  
     ![Excel - Ventana Explorador de datos maestros](../../2014/tutorials/media/et-combinematchandpublishnewsod-02.jpg "Excel - Ventana Explorador de datos maestros")  
  
6.  Haga doble clic en **proveedor** en la lista de entidades para cargar los miembros de la entidad en la hoja de cálculo de Excel.  
  
7.  Haga clic en **Sheet2** en la parte inferior para cambiar a la pestaña **hoja2** . Si no ve **Sheet2**, agregue una nueva hoja de cálculo.  
  
8.  Abra el archivo **Suppliers. xls** (el archivo de entrada original incluido en los archivos del tutorial) y copie todas las filas (tres) de la hoja de cálculo **CombineAndCleanse** en **Sheet2**.  
  
9. Vuelva a la hoja de **proveedores** en el **libro 1: Microsoft Excel** (no la **lista de proveedores limpiados y coincidentes** ) que está conectado a **MDS**.  
  
10. Haga clic en **Datos maestros** en la barra de menús.  
  
11. Haga clic en **combinar datos** en la cinta de opciones. Verá el cuadro de diálogo **combinar datos** .  
  
12. En el cuadro de diálogo **combinar datos** , haga clic en el botón situado junto al cuadro de texto **rango que se va a combinar con los datos MDS** , tal como se muestra en la siguiente imagen.  
  
     ![Excel - Cuadro de diálogo Combinar datos](../../2014/tutorials/media/et-combinematchandpublishnewsod-03.jpg "Excel - Cuadro de diálogo Combinar datos")  
  
13. Ahora debe ver el cuadro de diálogo reducido. Ahora, haga clic en **Sheet2** para cambiar a la pestaña **hoja2** que tiene los nuevos datos de proveedor con 4 filas (incluida una fila de encabezado).  
  
14. En la **hoja2**, seleccione **todas las filas, incluida la fila de encabezado** (aunque parezca que ya están seleccionadas). Debería ver que el **intervalo que se va a combinar con los datos de MDS** se actualiza automáticamente.  
  
     ![Excel - Cuadro de diálogo Combinar datos - Minimizado](../../2014/tutorials/media/et-combinematchandpublishnewsod-04.jpg "Excel - Cuadro de diálogo Combinar datos - Minimizado")  
  
15. Vuelva a la pestaña **proveedores** sin cerrar el cuadro de diálogo **combinar datos** .  
  
16. Haga clic en el **botón** situado junto al **cuadro de texto**. Ahora debe ver que el cuadro de diálogo se ha expandido. Debería ver que todas las asignaciones entre las columnas de la **entidad** MDS del **proveedor** a las columnas de **Excel** se rellenan automáticamente.  
  
     ![Excel - Cuadro de diálogo Combinar datos cumplimentado con datos](../../2014/tutorials/media/et-combinematchandpublishnewsod-05.jpg "Excel - Cuadro de diálogo Combinar datos cumplimentado con datos")  
  
17. Asegúrese de que la columna de entidad **código** esté asignada a la columna **IdProveedor** de la hoja de cálculo y la columna de la entidad **código postal** esté asignada a la columna **código postal** de la hoja de cálculo.  
  
18. En el cuadro de diálogo **combinar datos** , haga clic en **combinar**.  
  
19. Confirme que se han agregado tres filas de datos al final de la hoja de cálculo y que están codificadas por colores.  
  
     ![Excel - Nuevos elementos después de la combinación](../../2014/tutorials/media/et-combinematchandpublishnewsod-06.jpg "Excel - Nuevos elementos después de la combinación")  
  
20. Haga clic en **datos matemáticos** en la cinta de opciones para identificar duplicados. Esta característica emplea la funcionalidad de coincidencia de DQS.  
  
21. En el cuadro de diálogo **coincidencia de datos** , seleccione **proveedores** para la base de **conocimiento de DQS**.  
  
     ![Excel - Cuadro de diálogo Coincidir datos](../../2014/tutorials/media/et-combinematchandpublishnewsod-07.jpg "Excel - Cuadro de diálogo Coincidir datos")  
  
22. Asigne columnas de la hoja de cálculo a dominios como se muestra en la tabla siguiente.  
  
    |Columna de la hoja de cálculo|Domain|  
    |----------------------|------------|  
    |Code (cargó Id. de proveedor como código de la entidad Proveedor en MDS)|Id. de proveedor|  
    |Name (cargó Nombre de proveedor como nombre de la entidad Proveedor en MDS)|Nombre del proveedor|  
    |ContactEmailAddress|Correo electrónico de contacto|  
  
23. Seleccione **requisito previo** para la asignación de columna de **código** .  
  
24. Escriba **70%** como el **peso** del **nombre del proveedor** y el **30%** como el **peso** del **correo electrónico de contacto** , tal como se muestra en la imagen.  
  
25. Haga clic en **OK**.  
  
26. El proceso de coincidencia debe identificar un duplicado para el proveedor con **código: S1**.  
  
     ![Excel - Resultados de coincidencias](../../2014/tutorials/media/et-combinematchandpublishnewsod-08.jpg "Excel - Resultados de coincidencias")  
  
27. Seleccione la **fila duplicada (naranja)**, haga clic con el botón secundario y haga clic en **eliminar** para eliminar la fila.  
  
28. Elimine la columna de **CLUSTER_ID** porque ya no la necesita.  
  
29. Haga clic en **publicar** para publicar los otros dos registros nuevos con los **códigos S66** y **S57** en MDS.  
  
30. En el cuadro de diálogo **publicar y anotar** , agregue una **anotación**y haga clic en **publicar**.  
  
31. Cambie a la **aplicación Web de Master Data Manager**.  
  
32. En la Página principal, asegúrese de que se ha seleccionado **proveedores** para el **modelo**y haga clic en **Explorador**. Si ya tiene el **Explorador** abierto, actualice el explorador de Internet.  
  
33. **Ordene** la lista por **código** y busque los registros con **S57** y **S66** como códigos. También puede usar el botón **filtro** de la barra de herramientas para buscar un registro específico en la lista.  
  
34. Ahora, cierre **libro1: ventana de Microsoft Excel** sin guardar el archivo.  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 5: crear un atributo basado en dominio desde Excel](../../2014/tutorials/task-5-creating-a-domain-based-attribute-from-excel.md)  
  
  
