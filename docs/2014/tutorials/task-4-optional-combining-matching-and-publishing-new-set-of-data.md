---
title: 'Tarea 4 (opcional): Combinar, coincidencia y publicar un nuevo conjunto de datos | Microsoft Docs'
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
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489271"
---
# <a name="task-4-optional-combining-matching-and-publishing-new-set-of-data"></a>Tarea 4 (opcional): Combinación, búsqueda de coincidencias y publicación de un conjunto de datos nuevo
  Con el tiempo, le interesará agregar más datos al repositorio MDS. Antes de agregar datos, puede ser útil comparar los nuevos datos a los datos que ya se administran en MDS, para asegurarse de que no se agregan datos duplicados o imprecisos. En el complemento Master Data Services para Excel, puede combinar datos de dos hojas de cálculo y comparar los datos para identificar y quitar duplicados antes de publicar los datos en MDS. La característica de búsqueda de coincidencias del complemento MDS para Excel emplea la funcionalidad de coincidencia de DQS para identificar coincidencias en los datos. En esta tarea, combinará datos de dos hojas de cálculo en una y después buscará coincidencias para identificar y quitar duplicados antes de publicar los datos en MDS. Consulte [coincidencia de calidad de datos en el complemento MDS para Excel](https://msdn.microsoft.com/library/hh548681.aspx) y [combinar datos](https://msdn.microsoft.com/library/hh548680.aspx) temas para obtener más detalles.  
  
1.  Inicie una nueva instancia de **Excel**. Haga clic en **iniciar**, apunte a **ejecutar**, tipo **Excel**y haga clic en **Aceptar**.  
  
2.  Cambie a la **datos maestros** haciendo clic en **datos maestros** en la barra de menús.  
  
3.  Haga clic en **Connect** en la cinta de opciones la **conectar y cargar** grupo para conectarse a la **servidor MDS**. Ha configurado esta conexión anteriormente en esta lección.  
  
     ![Excel - Mostrar botón Explorador de datos maestros](../../2014/tutorials/media/et-combinematchandpublishnewsod-01.jpg "Excel - Mostrar botón Explorador de datos maestros")  
  
4.  Debería ver el **Explorador de datos maestros** panel a la derecha. Si no ve el Explorador de datos maestros, haga clic en **Mostrar explorador** botón en la cinta de opciones.  
  
5.  En el **Explorador de datos maestros** ventana, seleccione **proveedores** en la lista desplegable para la **modelo**. Debería ver que el modelo tiene una entidad: **Proveedor**.  
  
     ![Excel - ventana del explorador de datos maestros](../../2014/tutorials/media/et-combinematchandpublishnewsod-02.jpg "Excel - ventana del explorador de datos maestros")  
  
6.  Haga doble clic en **proveedor** en la lista de entidades para cargar los miembros de entidad en la hoja de cálculo de Excel.  
  
7.  Haga clic en **Hoja2** en la parte inferior para cambiar a la **Hoja2** ficha. Si no ve **Hoja2**, agregue una nueva hoja de cálculo.  
  
8.  Abra **Suppliers.xls** (el archivo original entrada que se incluye en los archivos del tutorial) y copie todas las filas (tres) de la **CombineAndCleanse** hoja de cálculo para **Hoja2**.  
  
9. Vuelva a la **proveedor** hoja en el **1 libro: Microsoft Excel** (no el **Cleansed and Matched Supplier List** Excel) que está conectado a **MDS**.  
  
10. Haga clic en **Datos maestros** en la barra de menús.  
  
11. Haga clic en **combinar datos** en la cinta de opciones. Verá el **combinar datos** cuadro de diálogo.  
  
12. En el **combinar datos** diálogo cuadro, haga clic en el botón junto a **intervalo para combinar con los datos MDS** cuadro de texto, como se muestra en la siguiente imagen.  
  
     ![Excel - combinar datos cuadro de diálogo](../../2014/tutorials/media/et-combinematchandpublishnewsod-03.jpg "Excel: combinar datos cuadro de diálogo")  
  
13. Ahora debe ver el cuadro de diálogo reducido. Ahora, haga clic en **Hoja2** para cambiar a la **Hoja2** pestaña que tiene el nuevo proveedor de datos con 4 filas (incluida una fila de encabezado).  
  
14. En el **Hoja2**, seleccione **todas las filas incluida la fila de encabezado** (Aunque parezcan estar ya seleccionadas). Debería ver el **intervalo para combinar con los datos MDS** se actualiza automáticamente.  
  
     ![Excel - cuadro de diálogo de datos - minimizado de combinar](../../2014/tutorials/media/et-combinematchandpublishnewsod-04.jpg "Excel - combinar el cuadro de diálogo de datos - minimizado")  
  
15. Vuelva a la **proveedores** ficha sin cerrar la **combinar datos** cuadro de diálogo.  
  
16. Haga clic en el **botón** junto a la **cuadro de texto**. Ahora debe ver que el cuadro de diálogo se ha expandido. Debería ver todas las asignaciones entre columnas de la **proveedor** MDS **entidad** a **Excel** columnas se rellenan automáticamente.  
  
     ![Excel: combinar datos de cuadro de diálogo rellenado con datos](../../2014/tutorials/media/et-combinematchandpublishnewsod-05.jpg "Excel: combinar datos de cuadro de diálogo rellenado con datos")  
  
17. Asegúrese de que **código** columna de la entidad se asigna a la **SupplierID** columna en la hoja de cálculo y **código postal** columna de la entidad se asigna a la **código postal** columna en la hoja de cálculo.  
  
18. En el **combinar datos** cuadro de diálogo, haga clic en **combinar**.  
  
19. Confirme que se han agregado tres filas de datos al final de la hoja de cálculo y que están codificadas por colores.  
  
     ![Excel - nuevos elementos después de la combinación](../../2014/tutorials/media/et-combinematchandpublishnewsod-06.jpg "Excel - nuevos elementos después de la combinación")  
  
20. Haga clic en **matemáticas datos** en la cinta de opciones para identificar los duplicados. Esta característica emplea la funcionalidad de coincidencia de DQS.  
  
21. En el **coincidir datos** cuadro de diálogo, seleccione **proveedores** para **Base de conocimiento DQS**.  
  
     ![Excel - cuadro de diálogo coincidir datos](../../2014/tutorials/media/et-combinematchandpublishnewsod-07.jpg "Excel - cuadro de diálogo de datos de coincidencia")  
  
22. Asigne columnas de la hoja de cálculo a dominios como se muestra en la tabla siguiente.  
  
    |Columna de la hoja de cálculo|Dominio|  
    |----------------------|------------|  
    |Code (cargó Id. de proveedor como código de la entidad Proveedor en MDS)|Id. de proveedor|  
    |Name (cargó Nombre de proveedor como nombre de la entidad Proveedor en MDS)|Nombre de proveedor|  
    |ContactEmailAddress|Correo electrónico de contacto|  
  
23. Seleccione **requisitos previos** para el **código** asignación de columnas.  
  
24. Escriba **70%** como el **peso** para **Supplier Name** y **30%** como el **peso** para **Correo electrónico de contacto** tal como se muestra en la imagen.  
  
25. Haga clic en **Aceptar**.  
  
26. El proceso de coincidencia debe identificar un duplicado para el proveedor con **código: S1**.  
  
     ![Excel - resultados coincidentes](../../2014/tutorials/media/et-combinematchandpublishnewsod-08.jpg "Excel - resultados coincidentes")  
  
27. Seleccione el **fila duplicada (naranja)**, con el botón secundario y haga clic en **eliminar** para eliminar la fila.  
  
28. Eliminar el **CLUSTER_ID** columna Puesto que ya no es necesaria.  
  
29. Haga clic en **publicar** para publicar los otros dos nuevos registros con **códigos S66** y **S57** a MDS.  
  
30. En el **publicar y anotar** diálogo cuadro, agregue un **anotación**y haga clic en **publicar**.  
  
31. Cambie a la **aplicación Web de Master Data Manager**.  
  
32. En la página principal, asegúrese de que **proveedores** está seleccionada para la **modelo**y haga clic en **Explorer**. Si ya tiene la **Explorer** abierto, actualice el Explorador de internet.  
  
33. **Ordenación** la lista por **código** y busque los registros con **S57** y **S66** como códigos. También puede usar el **filtro** en la barra de herramientas para buscar un registro específico en la lista.  
  
34. Ahora, cierre **Book1 - Microsoft Excel** ventana sin guardar el archivo.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 5: Crear un atributo basado en dominio desde Excel](../../2014/tutorials/task-5-creating-a-domain-based-attribute-from-excel.md)  
  
  
