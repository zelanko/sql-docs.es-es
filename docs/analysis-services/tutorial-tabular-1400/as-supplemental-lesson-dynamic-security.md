---
title: 'Analysis Services lección complementaria del tutorial: Seguridad dinámica | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 8496868bc3b5b6ee42ac4f222724e859797662a4
ms.sourcegitcommit: a6949111461eda0cc9a71689f86b517de3c5d4c1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2019
ms.locfileid: "67263340"
---
# <a name="supplemental-lesson---dynamic-security"></a>Lección complementaria: Seguridad dinámica

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección complementaria, creará un rol adicional que implementa la seguridad dinámica. La seguridad dinámica proporciona seguridad de nivel de fila basada en el nombre de usuario o el identificador de inicio de sesión del usuario que ha iniciado sesión actualmente. 
  
Para implementar seguridad dinámica, agregar una tabla al modelo que contiene los nombres de usuario de los usuarios que pueden conectarse al modelo y examinar los datos y objetos del modelo. El modelo que crea con este tutorial está en el contexto de Adventure Works; Sin embargo, para completar esta lección, debe agregar una tabla que contiene los usuarios de su propio dominio. No necesita las contraseñas para los nombres de usuario que se agregan. Para crear una tabla EmployeeSecurity con una pequeña muestra de los usuarios de su propio dominio, utilice la función de pegar pegar datos de empleados desde una hoja de cálculo de Excel. En un escenario real, la tabla que contiene los nombres de usuario normalmente sería una tabla de una base de datos real como origen de datos; Por ejemplo, una tabla DimEmployee real.  
  
Para implementar seguridad dinámica, se usan dos funciones DAX: [Función USERNAME (DAX)](/dax/username-function-dax) y [función LOOKUPVALUE (DAX)](/dax/lookupvalue-function-dax). Estas funciones, aplicadas en una fórmula de filtro de columna, se definen en un nuevo rol. Mediante el uso de la función LOOKUPVALUE, la fórmula especifica un valor de la tabla EmployeeSecurity. La fórmula, a continuación, pasa a que el valor a la función USERNAME, que especifica el nombre de usuario de la sesión del usuario pertenece a este rol. El usuario, a continuación, puede examinar solo los datos especificados por los filtros de fila del rol. En este escenario, puede especificar que los empleados de ventas solo podrán examinar los datos de ventas por Internet para los territorios de ventas en los que son miembros.  
  
Las tareas que son únicas de este escenario de modelo tabular de Adventure Works, pero que no se aplicarían necesariamente en un escenario real, se identifican como tales. Cada tarea incluye información adicional que describe el propósito de la tarea.  
  
Tiempo estimado para completar esta lección: **30 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

En este artículo de la lección complementaria forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas de esta lección complementaria, debe haber completado todas las lecciones anteriores.  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>Agregar la tabla dimSalesTerritory al proyecto de modelo tabular AW Internet Sales  

Para implementar seguridad dinámica en este escenario de Adventure Works, debe agregar dos tablas adicionales al modelo. La primera tabla que agregará es DimSalesTerritory (como Sales Territory) desde la misma base de datos AdventureWorksDW. Más adelante se aplican un filtro de fila a la tabla SalesTerritory que define los datos concretos, que puede examinar el usuario con sesión iniciada.  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>Para agregar la tabla dimSalesTerritory  
  
1.  En el Explorador de modelos tabulares > **orígenes de datos**, haga clic en la conexión y, a continuación, haga clic en **importar nuevas tablas**.  

    Si aparece el cuadro de diálogo de credenciales de suplantación, escriba las credenciales de suplantación que usó en la lección 2: Agregar datos.
  
2.  En el navegador, seleccione el **DimSalesTerritory** de tabla y, a continuación, haga clic en **Aceptar**.    
  
3.  En el Editor de consultas, haga clic en el **DimSalesTerritory** de consulta y, a continuación, quite **SalesTerritoryAlternateKey** columna.  
  
7.  Haga clic en **Importar**.  
  
    La nueva tabla se agrega al área de trabajo del modelo. Objetos y datos de la tabla de origen DimSalesTerritory se importan, a continuación, en el modelo Tabular de AW Internet Sales.  
  
9. Después de la tabla se haya importado correctamente, haga clic en **cerrar**.  

## <a name="add-a-table-with-user-name-data"></a>Agregar una tabla con datos de nombre de usuario  

La tabla DimEmployee de la base de datos de ejemplo AdventureWorksDW contiene usuarios del dominio AdventureWorks. Los nombres de usuario no existen en su propio entorno. Debe crear una tabla en el modelo que contenga una pequeña muestra (al menos tres) de usuarios reales de su organización. A continuación, agregue estos usuarios como miembros al nuevo rol. No necesita las contraseñas de los nombres de usuario de ejemplo, pero necesita nombres de usuario de Windows reales de su propio dominio.  
  
#### <a name="to-add-an-employeesecurity-table"></a>Para agregar una tabla EmployeeSecurity  
  
1.  Abra Microsoft Excel para crear una hoja de cálculo.  
  
2.  Copie la siguiente tabla, incluida la fila de encabezado, y péguela en la hoja de cálculo.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Reemplace el nombre, apellidos y dominio\nombre de usuario con los nombres e identificadores de inicio de sesión de tres usuarios de su organización. Coloque el mismo usuario en las dos primeras filas de EmployeeId 1, que muestra este usuario pertenece a más de un territorio de ventas. Deje los campos EmployeeId y SalesTerritoryId tal como están.  
  
4.  Guarde la hoja de cálculo como **SampleEmployee**.  
  
5.  En la hoja de cálculo, seleccione todas las celdas con datos de empleados, incluidos los encabezados, a continuación, haga clic en los datos seleccionados y, a continuación, haga clic en **copia**.  
  
6.  En SSDT, haga clic en el **editar** menú y, a continuación, haga clic en **pegar**.  
  
    Si pegar está atenuada, haga clic en cualquier columna de cualquier tabla en la ventana del Diseñador de modelos e inténtelo de nuevo.  
  
7.  En el **vista previa de pegado** cuadro de diálogo **nombre de la tabla**, tipo **EmployeeSecurity**.  
  
8.  En **atos a pegar**, compruebe que los datos incluyen todos los datos de usuario y los encabezados de la hoja de cálculo SampleEmployee.  
  
9. Compruebe que esté seleccionada la opción **Usar primera fila como encabezados de columna** y haga clic en **Aceptar**.  
  
    Se crea una nueva tabla denominada "employeesecurity" con datos de empleados copiados de la hoja de cálculo SampleEmployee.  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>Crear relaciones entre tablas FactInternetSales, DimGeography y DimSalesTerritory  

La tabla FactInternetSales, DimGeography y DimSalesTerritory todas contienen una columna común SalesTerritoryId. La columna SalesTerritoryId de la tabla DimSalesTerritory contiene valores con un identificador distinto para cada territorio de ventas.  
  
#### <a name="to-create-relationships-between-the-factinternetsales-dimgeography-and-the-dimsalesterritory-table"></a>Para crear relaciones entre los FactInternetSales, DimGeography y dimsalesterritory  
  
1.  En la vista de diagrama, en el **DimGeography** de tabla, haga clic y mantenga presionado el **SalesTerritoryId** columna, a continuación, arrastre el cursor hasta la **SalesTerritoryId** columna en el **DimSalesTerritory** de tabla y suéltelo.  
  
2.  En el **FactInternetSales** de tabla, haga clic y mantenga presionado el **SalesTerritoryId** columna, a continuación, arrastre el cursor hasta la **SalesTerritoryId** columna en el **DimSalesTerritory** de tabla y suéltelo.  
  
    Observe la propiedad Active de esta relación es False, lo que significa que está inactiva. La tabla FactInternetSales ya tiene otra relación activa.  
  
## <a name="hide-the-employeesecurity-table-from-client-applications"></a>Ocultar la tabla EmployeeSecurity de las aplicaciones cliente  

En esta tarea, ocultar la tabla EmployeeSecurity evitando que aparezca en la lista de campos de la aplicación cliente. Tenga en cuenta que ocultar una tabla no significa protegerla. Los usuarios todavía pueden consultar datos de la tabla EmployeeSecurity si saben cómo. Para proteger los datos de tabla EmployeeSecurity evitando que los usuarios puedan consultar sus datos, aplicar un filtro en una tarea posterior.  
  
#### <a name="to-hide-the-employeesecurity-table-from-client-applications"></a>Para ocultar la tabla EmployeeSecurity de las aplicaciones cliente  
  
-   En el diseñador de modelos en la vista de diagrama, haga clic con el botón derecho en el encabezado de tabla **Empleado** y, después, haga clic en **Ocultar en herramientas de cliente**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Crear empleados de ventas por el rol de usuario de territorio  

En esta tarea, cree un rol de usuario. Este rol incluye un filtro de fila define qué filas de la tabla DimSalesTerritory son visibles para los usuarios. A continuación, se aplica el filtro en la dirección de la relación de uno a varios para todas las demás tablas relacionadas con DimSalesTerritory. También aplica un filtro que protege toda la tabla EmployeeSecurity que realice cualquier usuario que sea miembro del rol.  
  
> [!NOTE]  
> El rol de empleados de ventas por territorio que creará en esta lección solo permitirá a los miembros examinar (o consultar) los datos de ventas del territorio de ventas al que pertenezcan. Si agrega un usuario como miembro a los empleados de ventas por rol territorio que también existe como un miembro del rol creado en [lección 11: Crear Roles](../tutorial-tabular-1400/as-lesson-11-create-roles.md), obtendrá una combinación de permisos. Cuando un usuario es miembro de varios roles, los permisos y los filtros de fila definidos para cada uno de ellos son acumulativos. Es decir, el usuario tiene los mayores permisos determinados por la combinación de roles.  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>Para crear empleados de ventas por el rol de usuario de Territorio  
  
1.  En SSDT, haga clic en el **modelo** menú y, a continuación, haga clic en **Roles**.  
  
2.  En **Administrador de roles**, haga clic en **New**.  
  
    Se agrega a la lista un nuevo rol con el permiso Ninguno.  
  
3.  Haga clic en el nuevo rol y, a continuación, en el **nombre** columna, cambiar el nombre del rol a **empleados de ventas por territorio**.  
  
4.  En la columna **Permisos** , haga clic en la lista desplegable y, después, seleccione el permiso **Lectura** .  
  
5.  Haga clic en el **miembros** pestaña y, a continuación, haga clic en **agregar**.  
  
6.  En el **Seleccionar usuario o grupo** cuadro de diálogo **escriba lo nombres de objeto para seleccionar**, escriba el primer nombre de usuario de ejemplo que utilizó al crear la tabla EmployeeSecurity. Haga clic en **Comprobar nombres** para comprobar que el nombre de usuario es válido y haga clic en **Aceptar**.  
  
    Repita este paso, agregando los demás nombres de usuario de ejemplo que utilizó al crear la tabla EmployeeSecurity.  
  
7.  Haga clic en el **filtros de fila** ficha.  
  
8.  Para el **EmployeeSecurity** de tabla, en el **filtro DAX** columna, escriba la siguiente fórmula:  
  
    ```
      =FALSE()  
    ```
  
    Esta fórmula especifica que todas las columnas se resuelven en la condición booleana falsa. No hay columnas de la tabla EmployeeSecurity pueden consultarse por un miembro de los empleados de ventas por rol usuario territorio.  
  
9. Para el **DimSalesTerritory** de tabla, escriba la siguiente fórmula:  

    ```  
    ='DimSalesTerritory'[SalesTerritoryKey]=LOOKUPVALUE('EmployeeSecurity'[SalesTerritoryId], 
      'EmployeeSecurity'[LoginId], USERNAME(), 
      'EmployeeSecurity'[SalesTerritoryId], 'DimSalesTerritory'[SalesTerritoryKey]) 
    ```
  
    En esta fórmula, la función LOOKUPVALUE devuelve todos los valores de la columna DimEmployeeSecurity [SalesTerritoryId], donde el valor de EmployeeSecurity [LoginId] es el mismo que la sesión de nombre de usuario de Windows actual y EmployeeSecurity [SalesTerritoryId] es el igual que el de DimSalesTerritory [SalesTerritoryId].  
  
    El conjunto de identificadores devueltos por LOOKUPVALUE territorio de ventas, a continuación, se usa para restringir las filas que se muestra en la tabla DimSalesTerritory. Se muestran solo las filas donde la SalesTerritoryID para la fila está en el conjunto de identificadores devueltos por la función LOOKUPVALUE.  
  
10. En el Administrador de roles, haga clic en **Aceptar**.  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a>Probar los empleados de ventas por el rol de usuario de territorio  

En esta tarea, utilice la analizar en función de Excel en SSDT para probar la eficacia de los empleados de ventas por rol usuario territorio. Especifique uno de los nombres de usuario que agregó a la tabla EmployeeSecurity y como un miembro del rol. Este nombre de usuario, a continuación, se utiliza como el nombre de usuario efectivo en la conexión creada entre Excel y el modelo.  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>Para probar los empleados de ventas por el rol de usuario de territorio  
  
1.  En SSDT, haga clic en el **modelo** menú y, a continuación, haga clic en **analizar en Excel**.  
  
2.  En el cuadro de diálogo **Analizar en Excel** , en **Especifique el nombre de usuario o rol que se va a usar al conectarse al modelo**, seleccione **Otro usuario de Windows**y, después, haga clic en **Examinar**.  
  
3.  En el **Seleccionar usuario o grupo** cuadro de diálogo **escriba el nombre de objeto a seleccionar**, escriba un nombre de usuario que incluyó en la tabla EmployeeSecurity y, a continuación, haga clic en **comprobar nombres**.  
  
4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Seleccionar usuario o grupo** y, después, haga clic en **Aceptar** para cerrar el cuadro de diálogo **Analizar en Excel** .  
  
    Excel se abre con un nuevo libro. Automáticamente se crea una tabla dinámica. La lista PivotTable Fields incluye la mayoría de los campos de datos disponibles en el nuevo modelo.  
  
    Observe que la tabla EmployeeSecurity no está visible en la lista PivotTable Fields. Ocultó esta tabla de las herramientas de cliente en una tarea anterior.  
  
5.  En el **campos** lista **∑ Internet Sales** (medidas), seleccione el **InternetTotalSales** medida. La medida se celebra la **valores** campos.  
  
6.  Seleccione el **SalesTerritoryId** columna desde la **DimSalesTerritory** tabla. La columna se escribe en el **etiquetas de fila** campos.  
  
    Observe que las cifras de ventas por Internet solo aparecen para la región a la que pertenece el nombre de usuario efectivo que usó. Si selecciona otra columna, como la ciudad de la tabla DimGeography como campo de etiqueta de fila, se muestran solo las ciudades del territorio de ventas al que pertenece el usuario efectivo.  
    Este usuario no puede examinar ni consultar los datos de ventas de Internet de territorios distintos al que pertenecen. Esta restricción es porque el filtro de fila definido para la tabla DimSalesTerritory, empleados de ventas por rol de usuario del territorio, protege los datos de todos los datos relacionados con otros territorios de ventas.  
  
## <a name="see-also"></a>Vea también  

[función USERNAME (DAX)](/dax/username-function-dax)  
[función LOOKUPVALUE (DAX)](/dax/lookupvalue-function-dax)  
[Función CUSTOMDATA (DAX)](/dax/customdata-function-dax)  
