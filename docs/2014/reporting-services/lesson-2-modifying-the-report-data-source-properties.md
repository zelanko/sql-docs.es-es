---
title: 'Lección 2: Propiedades del origen de modificación de los datos de informe | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: c962b0ff-ce8a-4742-8262-dc730901afcf
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7f7f1df9e5b5ee885af3e7a0fe462faeafd2d6b7
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56026426"
---
# <a name="lesson-2-modifying-the-report-data-source-properties"></a>Lección 2: Modificar las propiedades del origen de datos de informe
  En esta lección, usará el Administrador de informes para seleccionar un informe que se entregará a los destinatarios. La suscripción controlada por datos que va a definir distribuirá el informe **Sales Order** creado en el tutorial [Crear un informe de tabla básico &#40;Tutorial de SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md). En los pasos siguientes, modificará la información de conexión del origen de datos que el informe utiliza para obtener los datos. Solo los informes que usan **credenciales almacenadas** para obtener acceso a un origen de datos del informe se pueden distribuir a través de una suscripción controlada por datos. Las credenciales almacenadas son necesarias para el procesamiento desatendido de informes.  
  
 También modificará el conjunto de datos y el informe para usar un parámetro que filtrar el informe en `[Order]` de modo que la suscripción pueda dar como resultado diferentes instancias del informe para pedidos concretos y formatos de representación.  
  
 **En este tema:**  
  
-   [Para modificar las propiedades del origen de datos](#bkmk_modify_datasource)  
  
-   [Para modificar AdventureWorksDataset](#bkmk_modify_dataset)  
  
-   [Para agregar un parámetro de informe y volver a publicar el informe](#bkmk_add_reportparameter)  
  
-   [Para volver a implementar el informe](#bkmk_redeploy)  
  
##  <a name="bkmk_modify_datasource"></a> Para modificar las propiedades del origen de datos  
  
1.  Iniciar [el Administrador de informes &#40;modo nativo de SSRS&#41; ](../../2014/reporting-services/report-manager-ssrs-native-mode.md) con privilegios de administrador, por ejemplo, haga clic en el icono para Internet Explorer y haga clic en **ejecutar como administrador**.  
  
2.  Busque la carpeta que contiene el informe **Sales Orders** y, en el menú contextual del informe, haga clic en **Administrar**.  
  
     ![Abra el menú contextual del informe y seleccione Administrar](../../2014/tutorials/media/ssrs-tutorial-datadriven-manage-report.gif "abra el menú contextual del informe y seleccione Administrar")  
  
3.  Haga clic en la pestaña **Orígenes de datos** .  
  
4.  Como **Tipo de conexión**, seleccione **Microsoft SQL Server**.  
  
5.  La cadena de conexión del origen de datos personalizada será la siguiente y se supone que la base de datos de ejemplo está en un servidor de bases de datos local:  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2012  
    ```  
  
6.  Haga clic en **Credenciales almacenadas de forma segura en el servidor de informes**.  
  
7.  Escriba su nombre de usuario (utilizando el formato *dominio\usuario*) y la contraseña. Si no dispone de permisos para tener acceso a la base de datos [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] , especifique un inicio de sesión que disponga de ellos.  
  
8.  Haga clic en **Usar como credenciales de Windows para la conexión al origen de datos**y, a continuación, en **Aceptar**. Si no usa ninguna cuenta de dominio (por ejemplo, si usa un inicio de sesión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ), no active esta casilla.  
  
9. Haga clic en **Probar conexión** para comprobar que puede conectarse al origen de datos.  
  
10. Haga clic en **Aplicar**.  
  
11. Visualice el informe para comprobar que se ejecuta con las credenciales que ha especificado. Para ver el informe, haga clic en la pestaña **Ver** . Tenga en cuenta que, una vez abierto el informe, debe seleccionar un nombre de empleado y, después, hacer clic en **Ver informe** para ver el informe.  
  
##  <a name="bkmk_modify_dataset"></a> Para modificar AdventureWorksDataset  
  
1.  Abra el informe Sales Orders en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]  
  
2.  Haga clic con el botón derecho en el conjunto de datos `AdventureWorksDataset` y haga clic en **Propiedades del conjunto de datos**.  
  
3.  Agregue la instrucción `WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)` antes que la instrucción `Group By` . La sintaxis de la consulta completa es la siguiente:  
  
    ```  
    SELECT soh.OrderDate AS Date, soh.SalesOrderNumber AS [Order], pps.Name AS Subcat, pp.Name AS Product, SUM(sd.OrderQty) AS Qty, SUM(sd.LineTotal)  AS LineTotal  
    FROM Sales.SalesPerson AS sp INNER JOIN  
      Sales.SalesOrderHeader AS soh ON sp.BusinessEntityID = soh.SalesPersonID INNER JOIN  
       Sales.SalesOrderDetail AS sd ON sd.SalesOrderID = soh.SalesOrderID INNER JOIN  
       Production.Product AS pp ON sd.ProductID = pp.ProductID  
    INNER JOIN  
       Production.ProductSubcategory AS pps ON pp.ProductSubcategoryID = pps.ProductSubcategoryID   
    INNER JOIN  
        Production.ProductCategory AS ppc ON ppc.ProductCategoryID = pps.ProductCategoryID  
  
    WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)  
  
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name, soh.SalesPersonID  
    HAVING (ppc.Name = 'Clothing')  
    ```  
  
4.  Haga clic en **Aceptar**.  
  
##  <a name="bkmk_add_reportparameter"></a> Para agregar un parámetro de informe y volver a publicar el informe  
  
1.  En el panel **Datos de informe** , haga clic en **Nuevo** y, a continuación, haga clic en **Parámetro**.  
  
2.  En **Nombre**, escriba `OrderNumber`.  
  
3.  En **Inicio**, escriba `OrderNumber`.  
  
4.  Seleccione **Permitir valor en blanco**.  
  
5.  Seleccione **Permitir valor NULL**.  
  
6.  Haga clic en **Aceptar**. El parámetro se agregará a la carpeta **Panel Datos de informe** y tendrá una apariencia similar a la de la imagen siguiente:  
  
     ![El nuevo parámetro se agrega al panel datos de informe](../../2014/tutorials/media/ssrs-tutorial-datadriven-parameter.gif "el nuevo parámetro se agrega al panel datos de informe")  
  
7.  Haga clic en la pestaña **Vista previa** para ejecutar el informe. Observe el cuadro de entrada del parámetro en la parte superior del informe. Puede elegir entre lo siguiente:  
  
    -   Haga clic en Ver informe para ver el informe completo sin usar un parámetro.  
  
    -   Cancelar la selección de la opción Null y escribir un número de pedido, por ejemplo so71949, para ver solo el único pedido del informe.  
  
         ![Visor de informes con área de parámetros visible](../../2014/tutorials/media/ssrs-tutorial-datadriven-reportviewer-parameter.gif "Visor de informes con área de parámetros visible")  
  
8.  Volver a implementar el informe de modo que la configuración de la suscripción de la lección siguiente pueda usar los cambios efectuados en esta lección. Para obtener más información sobre las propiedades del proyecto usado en el tutorial de la tabla, vea la sección ' Para publicar el informe en el servidor de informes (opcional)' de [lección 6: Agregar grupos y totales &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md).  
  
##  <a name="bkmk_redeploy"></a> Para volver a implementar el informe  
  
1.  Volver a implementar el informe de modo que la configuración de la suscripción de la lección siguiente pueda usar los cambios efectuados en esta lección. Para obtener más información sobre las propiedades del proyecto usado en el tutorial de la tabla, vea la sección ' Para publicar el informe en el servidor de informes (opcional)' de [lección 6: Agregar grupos y totales &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md).  
  
2.  En la barra de herramientas, haga clic en **Generar** y, a continuación, haga clic en **Tutorial de implementación**.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Ha configurado correctamente el informe para obtener datos utilizando credenciales almacenadas. A continuación, especifica la suscripción usando las páginas de suscripción controlada por datos en el Administrador de informes. Consulte [lección 3: Definir una suscripción controlada por datos](../reporting-services/lesson-3-defining-a-data-driven-subscription.md).  
  
## <a name="see-also"></a>Vea también  
 [Administrar orígenes de datos de informe](report-data/manage-report-data-sources.md)   
 [Especificar información de credenciales y conexión para los orígenes de datos de informes](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Crear una suscripción controlada por datos &#40;Tutorial de SSRS&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Crear un informe de tabla básico &#40;Tutorial de SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  
  
