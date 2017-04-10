---
title: "Usar un destino de conjunto de registros | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "destino de conjunto de registros"
ms.assetid: a7b143dc-8008-404f-83b0-b45ffbca6029
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# Usar un destino de conjunto de registros
  El destino de conjunto de registros no guarda los datos en un origen de datos externo. En su lugar, el destino de conjunto de registros guarda los datos en memoria, en un conjunto de registros que se almacena en una variable de paquete [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] del tipo de datos **Objeto**. Una vez que el destino de conjunto de registros guarda los datos, normalmente se utiliza un contenedor de bucles Foreach con el enumerador de ADO para Foreach para procesar una fila del conjunto de registros cada vez. El enumerador de ADO para Foreach guarda el valor de cada columna de la fila actual en una variable de paquete independiente. A continuación, las tareas que se configuran en el contenedor de bucles Foreach leen esos valores de las variables y realizan alguna acción con ellos.  
  
 Puede utilizar el destino de conjunto de registros en muchos escenarios diferentes. A continuación se muestran algunos ejemplos:  
  
-   Puede usar una tarea Enviar correo y el lenguaje de expresiones [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para enviar un mensaje de correo personalizado por cada fila del conjunto de registros.  
  
-   Puede utilizar un componente de script configurado como origen en una tarea Flujo de datos para leer los valores de las columnas del flujo de datos. A continuación, puede utilizar transformaciones y destinos para transformar y guardar cada fila. En este ejemplo, la tarea Flujo de datos se ejecuta una vez por cada fila.  
  
 En las secciones siguientes se describe en primer lugar el proceso general de uso del destino de conjunto de registros y, a continuación, se muestra un ejemplo concreto acerca de cómo se utiliza el destino.  
  
## Pasos generales para utilizar un destino de conjunto de registros  
 El procedimiento siguiente resume los pasos que son necesarios para guardar los datos en un destino de conjunto de registros y utilizar, a continuación, el contenedor de bucles Foreach para procesar cada fila.  
  
#### Para guardar los datos en un destino de conjunto de registros y procesar cada fila utilizando el contenedor de bucles Foreach  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], cree o abra un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  Cree una variable que contendrá el conjunto de registros guardados en la memoria por el destino de conjunto de registros y establezca el tipo de la variable en **Object**.  
  
3.  Cree variables adicionales de los tipos adecuados para que contengan los valores de cada columna del conjunto de registros que desea utilizar.  
  
4.  Agregue y configure el administrador de conexiones requerido por el origen de datos que pretende utilizar en su flujo de datos.  
  
5.  Agregue una tarea Flujo de datos al paquete y en la pestaña Flujo de datos del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , configure los orígenes y las transformaciones que se van a utilizar para cargar y transformar los datos.  
  
6.  Agregue un destino de conjunto de registros al flujo de datos y asócielo con las transformaciones. En la propiedad **VariableName** del destino de conjunto de registros, escriba el nombre de la variable que creó para el conjunto de registros.  
  
7.  En la pestaña Flujo de control del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , agregue un contenedor de bucles Foreach y conecte este contenedor después de la tarea Flujo de datos. A continuación, abra el **Editor de bucles Foreach** para configurar el contenedor con los valores siguientes:  
  
    1.  En la página **Colección** , seleccione el enumerador ADO para Foreach. A continuación, en **Variable de origen de objeto ADO**, seleccione la variable que contiene el conjunto de registros.  
  
    2.  En la página **Asignaciones de variables**, asigne el índice de base cero de cada columna que quiera usar a la variable adecuada.  
  
         En cada iteración del bucle, el enumerador rellena estas variables con los valores de columna de la fila actual.  
  
8.  Dentro del contenedor de bucles Foreach, agregue y configure las tareas que va a utilizar para procesar una fila del conjunto cada vez al leer los valores de las variables.  
  
## Ejemplo de uso del destino de conjunto de registros  
 En el ejemplo siguiente, la tarea Flujo de datos carga información sobre los empleados de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] de la tabla Sales.SalesPerson en un destino de conjunto de registros. A continuación, un contenedor de bucles Foreach lee una fila de datos cada vez y llama a la tarea Enviar correo. La tarea Enviar correo utiliza expresiones para enviar un mensaje de correo electrónico personalizado a cada vendedor sobre el importe de su paga extraordinaria.  
  
#### Para crear el proyecto y configurar las variables  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], cree un nuevo proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  En el menú **SSIS** , seleccione **Variables**.  
  
3.  En la ventana **Variables** , cree las variables que contendrán el conjunto de registros y los valores de columna de la fila actual:  
  
    1.  Cree una variable con nombre **BonusRecordset**y establezca su tipo en **Object**.  
  
         La variable **BonusRecordset** contiene el conjunto de registros.  
  
    2.  Cree una variable con nombre **EmailAddress**y establezca su tipo en **String**.  
  
         La variable **EmailAddress** contiene la dirección de correo electrónico del vendedor.  
  
    3.  Cree una variable con nombre **FirstName**y establezca su tipo en **String**.  
  
         La variable **FirstName** contiene el nombre del vendedor.  
  
    4.  Cree una variable con nombre **Bonus**y establezca su tipo en **Double**.  
  
         La variable **Bonus** contiene el importe de la bonificación del vendedor.  
  
#### Para configurar los administradores de conexión  
  
1.  En el área de Administradores de conexiones del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , agregue y configure un nuevo administrador de conexiones OLE DB que se conecte a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
     El origen de OLE DB de la tarea Flujo de datos utilizará este administrador de conexiones para recuperar los datos.  
  
2.  En el área de Administradores de conexiones, agregue y configure un nuevo administrador de conexiones SMTP que se conecte a un servidor SMTP disponible.  
  
     La tarea Enviar correo incluida en el contenedor de bucles Foreach utilizará este administrador de conexiones para enviar correos electrónicos.  
  
#### Para configurar el flujo de datos y el destino de conjunto de registros  
  
1.  En la pestaña **Flujo de control** del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , agregue una tarea Flujo de datos a la superficie de diseño.  
  
2.  En la pestaña **Flujo de datos** tab, add an OLE DB source to the Flujo de datos task, and then open the **Editor de origen de OLE DB**.  
  
3.  En la página **Administrador de conexiones** del editor, configure el origen con los valores siguientes:  
  
    1.  En **Administrador de conexiones OLE DB**, seleccione el administrador de conexiones OLE DB que creó previamente.  
  
    2.  En **Modo de acceso a datos**, seleccione **Comando SQL**.  
  
    3.  En **Texto de comando SQL**, escriba la consulta siguiente:  
  
        ```  
        SELECT     Person.Contact.EmailAddress, Person.Contact.FirstName, CONVERT(float, Sales.SalesPerson.Bonus) AS Bonus  
        FROM         Sales.SalesPerson INNER JOIN  
                              Person.Contact ON Sales.SalesPerson.SalesPersonID = Person.Contact.ContactID  
        ```  
  
        > [!NOTE]  
        >  Tiene que convertir el valor **currency** de la columna Bonus en un valor **float** antes de poder cargar ese valor en una variable de paquete cuyo tipo sea **Double**.  
  
4.  En la pestaña **Flujo de datos** , agregue un destino de conjunto de registros y conecte el destino después del origen de OLE DB.  
  
5.  Abra el **Editor de destino de conjunto de registros**y configure el destino con los valores siguientes:  
  
    1.  En la pestaña **Propiedades de componente** , en la propiedad **VariableName** , seleccione **User::BonusRecordset**.  
  
    2.  En la pestaña **Columnas de entrada** , seleccione las tres columnas disponibles.  
  
#### Para configurar el contenedor de bucles Foreach y ejecutar el paquete  
  
1.  En la pestaña **Flujo de control** del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , agregue un contenedor de bucles Foreach y conecte el contenedor después de la tarea Flujo de datos.  
  
2.  Abra el **Editor de bucles Foreach**y configure el contenedor con los valores siguientes:  
  
    1.  En la página **Colección** , en **Enumerador**, seleccione **Enumerador de ADO para Foreach**y, en **Variable de origen de objeto ADO**, seleccione **User::BonusRecordset**.  
  
    2.  En la página **Asignaciones de variables** , asigne la variable **User::EmailAddress** al índice 0, **User::FirstName** al índice 1 y **User::Bonus** al índice 2.  
  
3.  En la pestaña **Flujo de control** , en el contenedor de bucles Foreach, agregue una tarea Enviar correo.  
  
4.  Abra el **Editor de la tarea Enviar correo**, y a continuación, en la página **Correo** , configure la tarea con los valores siguientes:  
  
    1.  En **SmtpConnection**, seleccione el administrador de conexiones SMTP que se configuró previamente.  
  
    2.  En **De**, escriba una dirección de correo electrónico adecuada.  
  
         Si utiliza su propia dirección de correo electrónico, podrá comprobar que el paquete se ejecuta correctamente. Recibirá las confirmaciones de los mensajes que no se pudieron entregar enviados por la tarea Enviar correo a los vendedores ficticios de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
    3.  En **Para**, escriba una dirección de correo electrónico predeterminada.  
  
         Este valor no se utilizará, pero se reemplazará en tiempo de ejecución por la dirección de correo electrónico de cada vendedor.  
  
    4.  En **Asunto**, escriba "Paga extraordinaria anual".  
  
    5.  En **MessageSourceType**, seleccione **Entrada directa**.  
  
5.  En la página **Expresiones** del **Editor de la tarea Enviar correo**, haga clic en el botón de puntos suspensivos (**…**) para abrir el **Editor de expresiones de propiedad**.  
  
6.  En el **Editor de expresiones de propiedad**, escriba la información siguiente:  
  
    1.  En **ToLine**, agregue la expresión siguiente:  
  
        ```  
        @[User::EmailAddress]  
        ```  
  
    2.  En la propiedad **MessageSource** , agregue la expresión siguiente:  
  
        ```  
        "Dear " +  @[User::FirstName] + ": The amount of your bonus for this year is $" +  (DT_WSTR, 12) @[User::Bonus] + ". Thank you!"  
        ```  
  
7.  Ejecute el paquete.  
  
     Si especificó un servidor SMTP válido y proporcionó su propia dirección de correo electrónico, recibirá las confirmaciones de los mensajes que no se pueden entregar que la tarea Enviar correo enviará a los vendedores ficticios de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
  