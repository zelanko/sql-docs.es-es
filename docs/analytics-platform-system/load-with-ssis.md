---
title: Carga con Integration Services
description: Proporciona información de referencia e implementación para cargar datos en el almacenamiento de datos paralelos (PDW) mediante paquetes de SQL Server Integration Services (SSIS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b0bcb5cfe1ec4111aaea7153f35bca084df62b76
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401016"
---
# <a name="load-data-with-integration-services-to-parallel-data-warehouse"></a>Carga de datos con Integration Services en el almacenamiento de datos paralelos
Proporciona información de referencia e implementación para cargar datos en SQL Server almacenamiento de datos paralelos mediante el uso de paquetes de SQL Server Integration Services (SSIS).  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx) on MSDN.  

-->
  
## <a name="Basics"></a>Conceptos básicos  
Integration Services es el componente de SQL Server para la extracción, transformación y carga de datos (ETL) de alto rendimiento, y se suele usar para rellenar y actualizar un almacenamiento de datos.  
  
El adaptador de destino de PDW es un componente de Integration Services que permite cargar datos en PDW mediante el uso de paquetes de Integration Services DTSX. En un flujo de trabajo de paquete de SQL ServerPDW, puede cargar y combinar datos de varios orígenes y cargar datos en varios destinos. Las cargas se producen en paralelo, en un paquete y entre varios paquetes que se ejecutan simultáneamente, hasta un máximo de 10 cargas ejecutándose en paralelo en el mismo dispositivo.  
  
Además de las tareas descritas en este tema, puede utilizar otras características de Integration Services para filtrar, transformar, analizar y limpiar los datos antes de cargarlos en el almacenamiento de datos. También puede mejorar el flujo de trabajo del paquete mediante la ejecución de instrucciones SQL, la ejecución de paquetes secundarios o el envío de correo.  
  
Para obtener la documentación completa de Integration Services, vea [SQL Server Integration Services](../integration-services/sql-server-integration-services.md).  
  
## <a name="HowToDeployPackage"></a>Métodos para ejecutar un paquete de Integration Services  
Use uno de estos métodos para ejecutar un paquete de Integration Services.  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>Ejecutar desde SQL Server 2008 R2 Business Intelligence Development Studio (BIDS)  
Para ejecutar el paquete desde BIDS, haga clic con el botón derecho en el paquete y elija **Ejecutar paquete**.  
  
De forma predeterminada, BIDS ejecuta paquetes mediante archivos binarios de 64 bits. Esto viene determinado por la propiedad del paquete **Run64BitRuntime** . Para establecer esta propiedad, vaya a **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y elija **propiedades**. En las **páginas de propiedades de Integration Services**, vaya a **propiedades de configuración** y seleccione **depuración**. Verá la propiedad **Run64BitRuntime** en las opciones de **depuración**. Para usar los tiempos de ejecución de 32 bits, establezca este valor en **false**. Para usar tiempos de ejecución de 64 bits, establézcalo en **true**.  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>Ejecute desde SQL Server 2012 SQL Server Data Tools  
Para ejecutar el paquete desde SQL Server Data Tools, haga clic con el botón derecho en el paquete y elija **Ejecutar paquete**.  
  
### <a name="run-from-powershell"></a>Ejecutar desde PowerShell  
Para ejecutar el paquete desde Windows PowerShell, con la utilidad **DTExec** :`dtexec /FILE <packagePath>`  
  
Por ejemplo: `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
### <a name="run-from-a-windows-command-prompt"></a>Ejecutar desde un símbolo del sistema de Windows 
Para ejecutar el paquete desde un símbolo del sistema de Windows, mediante la utilidad **DTExec** :`dtexec /FILE <packagePath>`  
  
Por ejemplo: `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="DataTypes"></a>Tipos de datos  
Cuando se usa Integration Services para cargar datos de un origen de datos en una base de datos de PDW de SQL Server, los datos se asignan primero de los datos de origen a los tipos de datos Integration Services. Esto permite que los datos de varios orígenes de datos se asignen a un conjunto común de tipos de datos.  
  
A continuación, los datos se asignan desde Integration Services a PDW de SQL Server tipos de datos. Para cada PDW de SQL Server tipo de datos, en la tabla siguiente se enumeran los tipos de datos de Integration Services que se pueden convertir al tipo de datos PDW de SQL Server.  
  
|Tipo de datos de PDW|Integration Services tipos de datos que se asignan al tipo de datos de PDW|  
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|  
|BIT|DT_BOOL|  
|BIGINT|DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4|  
|CHAR|DT_STR|  
|DATE|DT_DBDATE|  
|DATETIME|DT_DATE, DT_DBDATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2|  
|DATETIME2|DT_DATE, DT_DBDATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2|  
|DATETIMEOFFSET|DT_WSTR|  
|DECIMAL|DT_DECIMAL, DT_I1, DT_I2, DT_I4, DT_I4, DT_I8, DT_NUMERIC, DT_UI1, DT_UI2, DT_UI4, DT_UI8|  
|FLOAT|DT_R4, DT_R8|  
|INT|DT_I1, DTI2, DT_I4, DT_UI1, DT_UI2|  
|MONEY|DT_CY|  
|NCHAR|DT_WSTR|  
|NUMERIC|DT_DECIMAL, DT_I1, DT_I2, DT_I4, DT_I8, DT_NUMERIC, DT_UI1, DT_UI2, DT_UI4, DT_UI8|  
|NVARCHAR|DT_WSTR, DT_STR|  
|real|DT_R4|  
|SMALLDATETIME|DT_DBTIMESTAMP2|  
|SMALLINT|DT_I1, DT_I2, DT_UI1|  
|SMALLMONEY|DT_R4|  
|TIME|DT_WSTR|  
|TINYINT|DT_I1|  
|VARBINARY|DT_BYTES|  
|VARCHAR|DT_STR|  
  
**Compatibilidad limitada para la precisión del tipo de datos**  
  
PDW genera un error de validación si asigna un DT_NUMERIC o DT_DECIMAL columna de entrada que contiene un valor con una precisión mayor que 28.  
  
**Tipos de datos no compatibles**  
  
PDW de SQL Server no admite los siguientes tipos de datos Integration Services:  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
Para cargar en PDW de SQL Server las columnas que contienen datos de estos tipos, debe agregar una transformación de conversión de datos ascendente en el flujo de datos para convertir los datos en un tipo de datos compatible.  
  
## <a name="permissions"></a>Permisos  
Para ejecutar un paquete de carga de Integration Services, necesita:  
  
-   Permiso LOAD en la base de datos.  
  
-   Permisos de inserción, actualización y eliminación aplicables en la tabla de destino.  
  
-   Si se utiliza una base de datos de ensayo, cree el permiso en la base de datos de ensayo. Esto es para crear una tabla temporal.  
  
-   Si no se usa ninguna base de datos de almacenamiento provisional, cree el permiso en la base de datos de destino. Esto es para crear una tabla temporal.  
  
## <a name="GenRemarks"></a>Notas generales  
Cuando un paquete de Integration Services tiene varios destinos de PDW de SQL Server en ejecución y se termina una de las conexiones, Integration Services detiene la inserción de datos en todos los destinos de PDW de SQL Server.  
  
## <a name="Limits"></a>Limitaciones y restricciones  
En el caso de un paquete de Integration Services, el número de destinos de PDW de SQL Server para el mismo origen de datos está limitado por el número máximo de cargas activas. Se preconfigura el máximo y no es configurable por el usuario. 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
Cada destino de paquete Integration Services para el mismo origen de datos cuenta como una carga cuando el paquete se está ejecutando. Por ejemplo, suponga que el máximo de cargas activas es 10. El paquete no se ejecutará si se intenta abrir 11 o más destinos para el mismo origen de datos.  
  
Varios paquetes pueden ejecutarse simultáneamente siempre y cuando cada paquete no utilice más del máximo de cargas activas. Por ejemplo, si el máximo de cargas activas es 10, puede ejecutar simultáneamente dos paquetes que usen 10 destinos cada uno. Se ejecutará un paquete mientras otro espera en la cola de carga.  
  
Si el número de cargas en la cola de carga supera el máximo de cargas en cola, el paquete no se ejecutará. Por ejemplo, si el número máximo de cargas es de 10 por dispositivo y el número máximo de cargas en cola es 40 por dispositivo, puede ejecutar simultáneamente cinco Integration Services paquetes que tengan cada uno de los 10 destinos abiertos. Si intenta ejecutar un sexto paquete, no se ejecutará.  

> [!IMPORTANT]
> El uso de un origen de datos de OLE DB en SSIS con el adaptador de destino de PDW puede provocar daños en los datos si la tabla de origen contiene columnas CHAR y VARCHAR con intercalaciones de SQL. Se recomienda usar un origen de ADO.NET si la tabla de origen contiene columnas CHAR o VARCHAR con intercalaciones de SQL. 

  
## <a name="Locks"></a>Comportamiento de bloqueo  
Al cargar datos con Integration Services, SQL ServerPDW utiliza bloqueos de nivel de fila para actualizar los datos de la tabla de destino. Esto significa que cada fila se bloquea para la lectura y escritura mientras se actualiza. Las filas de la tabla de destino no se bloquean mientras se cargan los datos en la tabla de ensayo.  
  
## <a name="Examples"></a>Ejemplos  
  
### <a name="Walkthrough"></a>A. Carga sencilla desde un archivo plano  
En el siguiente tutorial se muestra una carga de datos simple mediante Integration Services para cargar datos de archivo sin formato en un dispositivo PDW de SQL Server.  En este ejemplo se da por supuesto que ya se ha instalado Integration Services en el equipo cliente y que se ha instalado el PDW de SQL Server destino, tal y como se ha descrito anteriormente.  
  
En este ejemplo, se cargará en `Orders` la tabla, que tiene el siguiente DDL. La `Orders` tabla forma parte de la `LoadExampleDB` base de datos.  
  
```sql  
CREATE TABLE LoadExampleDB.dbo.Orders (  
   id INT,  
   city varchar(25),  
   lastUpdateDate DATE,  
   orderDate DATE)  
;  
```  
  
Estos son los datos de carga:  
  
```  
id        city           lastUpdateDate     orderdate  
--------- -------------- ------------------ ----------  
1         Seattle        2010-05-01         2010-01-01  
2         Denver         2002-06-25         1999-01-02  
```  
  
Como preparación para la carga, cree el archivo `exampleLoad.txt`plano que contiene los datos de carga:  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
En primer lugar, cree un paquete de Integration Services realizando estos pasos:  
  
1.  En SQL Server Data Tools \(SSDT\), seleccione **archivo**, **nuevo**y **proyecto**. Seleccione **Integration Services proyecto** en las opciones que aparecen. Asigne a este `ExampleLoad`proyecto el nombre y haga clic en **Aceptar**.  
  
2.  Haga clic en la pestaña **flujo de control** y arrastre la **tarea flujo de datos** desde el cuadro de **herramientas** hasta el panel **flujo de control** .  
  
3.  Haga clic en la pestaña **flujo de datos** y, a continuación, arrastre **origen de archivo plano** desde el **cuadro de herramientas** hasta el panel **flujo de datos** . Haga doble clic en el cuadro que acaba de crear para abrir el **Editor de origen de archivos planos**.  
  
4.  Haga clic en **Administrador de conexiones** y, a continuación, en **nuevo**.  
  
5.  En el cuadro **nombre del administrador de conexiones** , escriba un nombre descriptivo para la conexión. En este ejemplo, `Example Load Flat File CM`.  
  
6.  Haga clic en **examinar** y `ExampleLoad.txt` Seleccione el archivo en el equipo local.  
  
7.  Puesto que el archivo sin formato contiene una fila con nombres de columna, haga clic en los **nombres de columna en el cuadro de la primera fila de datos** .  
  
8.  Haga clic en **columnas** en la columna izquierda y obtenga una vista previa de los datos que se cargarán para asegurarse de que los nombres de columna y los datos se interpretaron correctamente.  
  
9. Haga clic en **avanzadas** en la columna izquierda. Haga clic en cada nombre de columna para revisar el tipo de datos que se ha asociado con los datos. Escriba los cambios en el cuadro para que los tipos de datos de los datos cargados sean compatibles con los tipos de columna de destino.  
  
10. Haga clic en **Aceptar** para guardar el administrador de conexiones.  
  
11. Haga clic en **Aceptar** para salir del **Editor de origen de archivos planos**.  
  
Especifique el destino para el flujo de datos.  
  
1.  Arrastre el **PDW de SQL Server destino** desde el **cuadro de herramientas** hasta el panel **flujo de datos** .  
  
2.  Haga doble clic en el cuadro que acaba de crear para cargar el **PDW de SQL Server editor de destino**.  
  
3.  Haga clic en la flecha abajo junto a **Administrador de conexiones**.  
  
4.  Seleccione **crear una nueva conexión**.  
  
5.  Rellene la información del servidor, el usuario, la contraseña y la base de datos de destino con información específica del dispositivo. (Los ejemplos se muestran a continuación). A continuación, haga clic en **Aceptar**.  
  
    Para conexiones de InfiniBand, **nombre de servidor**: escriba <nombre de dispositivo>-SQLCTL01, 17001.  
  
    Para conexiones Ethernet, **nombre de servidor**: escriba la dirección IP del clúster de nodo de control, la coma, el puerto 17001. Por ejemplo, 10.192.63.134, 17001.  
  
    **Usuario**`user1`  
  
    **Contraseña**`password1`  
  
    **Base de datos de destino:**`LoadExampleDB`  
  
6.  Seleccione la tabla de destino `Orders`:.  
  
7.  Seleccione **anexar** como modo de carga y haga clic en **Aceptar**.  
  
Especifique el flujo de datos del origen al destino.  
  
1.  En el panel **flujo de datos** , arrastre la flecha verde desde el cuadro origen de **archivo plano** hasta el cuadro destino de la **PDW de SQL Server** .  
  
2.  Haga doble clic en el cuadro **destino de PDW de SQL Server** para que pueda ver de nuevo el editor de **destino de PDW de SQL Server** . Debería ver los nombres de columna del archivo plano a la izquierda, en **columnas de entrada no asignadas**. Debería ver los nombres de columna de la tabla de destino a la derecha, en **columnas de destino no asignadas**. Asigne las columnas arrastrando o haciendo doble clic en los nombres de columna coincidentes de las listas **columnas de entrada no asignadas** y **columnas de destino no asignadas** en el cuadro **columnas asignadas** . Haga clic en **Aceptar** para guardar la configuración.  
  
3.  Guarde el paquete haciendo clic en **Guardar** en el menú **archivo** .  
  
Ejecute el paquete en el equipo Integration Services.  
  
1.  En el**Explorador de soluciones** de Integration Services (columna derecha), haga clic `Package.dtsx` con el botón derecho y seleccione **Ejecutar**.  
  
2.  El paquete se ejecutará y el progreso más los errores se mostrarán en el panel **progreso** . Use un cliente SQL para confirmar la carga o supervise la carga a través de la consola de administración de PDW de SQL Server.  
  
## <a name="see-also"></a>Consulte también  
[Crear una tarea script que use el adaptador de destino PDW de SSIS](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
[Diseñar e implementar paquetes (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx)  
[Tutorial: Crear un paquete básico con un asistente](https://technet.microsoft.com/library/ms365330\(v=sql11\).aspx)  
[Introducción (Integration Services)](https://go.microsoft.com/fwlink/?LinkId=202412)  
[Ejemplo de generación de paquetes dinámicos](https://go.microsoft.com/fwlink/?LinkId=202413)  
[Diseñar paquetes SSIS para el paralelismo (vídeo de SQL Server)](https://msdn.microsoft.com/library/dd795221.aspx)  
[Ejemplos de la comunidad Microsoft SQL Server: Integration Services](https://go.microsoft.com/fwlink/?LinkId=202415)  
[Mejorar las cargas incrementales con la captura de datos modificados](../integration-services/change-data-capture/change-data-capture-ssis.md)  
[Dimensión de variación lenta, transformación](../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)  
[Inserción masiva, tarea](../integration-services/control-flow/bulk-insert-task.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->
