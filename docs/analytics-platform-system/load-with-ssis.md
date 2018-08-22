---
title: Carga con Integration Services - almacenamiento de datos paralelos | Microsoft Docs
description: Proporciona información de referencia e implementación para cargar datos en el almacenamiento de datos paralelos (PDW) mediante el uso de paquetes de SQL Server Integration Services (SSIS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f20220208aed16d745dbab5aecce64e6653ef350
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394570"
---
# <a name="load-data-with-integration-services-to-parallel-data-warehouse"></a>Carga de datos con Integration Services para almacenamiento de datos paralelos
Proporciona información de referencia e implementación para cargar datos en almacenamiento de datos paralelos de SQL Server mediante el uso de paquetes de SQL Server Integration Services (SSIS).  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](http://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx) on MSDN.  

-->
  
## <a name="Basics"></a>Conceptos básicos  
Integration Services es el componente de SQL Server de alto rendimiento extracción, transformación y carga (ETL) de datos y normalmente se usa para rellenar y actualizar un almacén de datos.  
  
El adaptador de destino PDW es un componente de Integration Services que le permite cargar datos en PDW utilizando paquetes dtsx de Integration Services. En un flujo de trabajo de paquete para ServerPDW SQL, puede cargar y combinar datos de varios orígenes y cargar datos en varios destinos. Las cargas se producen en paralelo, en un paquete y entre varios paquetes que se ejecutan simultáneamente, hasta un máximo de 10 cargas ejecutándose en paralelo en el mismo dispositivo.  
  
Además de las tareas descritas en este tema, puede utilizar otras características de Integration Services para filtrar, transformar, analizar y limpiar los datos antes de cargarlos en el almacén de datos. También puede mejorar el flujo de trabajo del paquete mediante la ejecución de instrucciones SQL, la ejecución de paquetes secundarios o el envío de correo.  
  
Para obtener documentación completa de Integration Services, consulte [SQL Server Integration Services](../integration-services/sql-server-integration-services.md).  
  
## <a name="HowToDeployPackage"></a>Métodos para ejecutar un paquete de Integration Services  
Use uno de estos métodos para ejecutar un paquete de Integration Services.  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>Ejecutar desde SQL Server 2008 R2 Business Intelligence Development Studio (BIDS)  
Para ejecutar el paquete desde dentro de BIDS, haga doble clic en el paquete y elija **Ejecutar paquete**.  
  
De forma predeterminada, BIDS ejecuta paquetes mediante los archivos binarios de 64 bits. Esto viene determinado por la **Run64BitRuntime** propiedad del paquete. Para establecer esta propiedad, vaya a **el Explorador de soluciones**, haga doble clic en el proyecto y elija **propiedades**. En el **páginas de propiedades de Integration Services**, vaya a **propiedades de configuración** y seleccione **depuración**. Verá el **Run64BitRuntime** propiedad bajo la **opciones de depuración**. Para usar los tiempos de ejecución de 32 bits, establezca esta opción en **False**. Para usar los tiempos de ejecución de 64 bits, establezca esta opción en **True**.  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>Ejecutar desde SQL Server datos de SQL Server 2012, herramientas  
Para ejecutar el paquete desde dentro de SQL Server Data Tools, haga doble clic en el paquete y elija **Ejecutar paquete**.  
  
### <a name="run-from-powershell"></a>Ejecución de PowerShell  
Para ejecutar el paquete de Windows PowerShell, utilizando el **dtexec** utilidad: `dtexec /FILE <packagePath>`  
  
Por ejemplo, `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
### <a name="run-from-a-windows-command-prompt"></a>Ejecución de Windows de un símbolo del sistema 
Para ejecutar el paquete desde un símbolo del sistema de Windows, utilizando el **dtexec** utilidad: `dtexec /FILE <packagePath>`  
  
Por ejemplo, `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="DataTypes"></a>Tipos de datos  
Al utilizar Integration Services para cargar datos desde un origen de datos a una base de datos de SQL Server PDW, los datos se asignan primero del origen de datos a tipos de datos de Integration Services. Esto permite que los datos de varios orígenes de datos se asignen a un conjunto común de tipos de datos.  
  
A continuación, se asignan los datos de Integration Services a tipos de datos de SQL Server PDW. Para cada tipo de datos PDW de SQL Server, en la tabla siguiente se enumera los tipos de datos de Integration Services que se pueden convertir al tipo de datos PDW de SQL Server.  
  
|Tipo de datos PDW|Tipos de datos de servicios de integración (s) que se asignan al tipo de datos PDW|  
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|  
|BIT|DT_BOOL|  
|bigint|DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4|  
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
  
**Compatibilidad limitada con la precisión del tipo de datos**  
  
PDW genera un error de validación si asigna una columna de entrada DT_NUMERIC o DT_DECIMAL que contiene un valor con una precisión mayor que 28.  
  
**Tipos de datos no admitido**  
  
PDW de SQL Server no admite los siguientes tipos de datos de Integration Services:  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
Para cargar las columnas que contienen datos de estos tipos en PDW de SQL Server, debe agregar una transformación de conversión de datos de nivel superior en el flujo de datos para convertir los datos a un tipo de datos compatible.  
  
## <a name="permissions"></a>Permisos  
Para ejecutar un paquete de carga de Integration Services, necesitará:  
  
-   Permiso de carga en la base de datos.  
  
-   Aplicable INSERT, UPDATE, los permisos de eliminación en la tabla de destino.  
  
-   Si se usa una base de datos de almacenamiento provisional, permiso para crear la base de datos de almacenamiento provisional. Esto es para crear una tabla temporal.  
  
-   Si no se usa ninguna base de datos de almacenamiento provisional, permiso para crear la base de datos de destino. Esto es para crear una tabla temporal.  
  
## <a name="GenRemarks"></a>Notas generales  
Cuando un paquete de Integration Services tiene varios destinos de PDW de SQL Server que se ejecuta y una de las conexiones se termina, Integration Services detiene la inserción de datos para todos los destinos de PDW de SQL Server.  
  
## <a name="Limits"></a>Limitaciones y restricciones  
Para un paquete de Integration Services, el número de destinos de PDW de SQL Server para el mismo origen de datos está limitado por el número máximo de cargas activas. Se preconfigura el máximo y no es configurable por el usuario. 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
Cada destino del paquete de Integration Services para el mismo origen de datos se considera como una carga cuando se ejecuta el paquete. Por ejemplo, suponga que el máximo de cargas activas es 10. El paquete no se ejecutará si se intenta abrir 11 o más destinos para el mismo origen de datos.  
  
Varios paquetes pueden ejecutarse simultáneamente siempre y cuando cada paquete no utilice más del máximo de cargas activas. Por ejemplo, si el máximo de cargas activas es 10, puede ejecutar simultáneamente dos paquetes que usen 10 destinos cada uno. Se ejecutará un paquete mientras otro espera en la cola de carga.  
  
Si el número de cargas en la cola de carga supera el máximo de cargas en cola, el paquete no se ejecutará. Por ejemplo, si el número máximo de cargas es 10 por dispositivo y el número máximo de cargas en cola es 40 por dispositivo, puede ejecutar simultáneamente cinco paquetes de Integration Services que cada abran 10 destinos. Si intenta ejecutar un sexto paquete, no se ejecutará.  

> [!IMPORTANT]
> Uso de un origen de datos OLE DB de SSIS con el adaptador de destino PDW, puede provocar daños en los datos si la tabla de origen contiene las columnas char y varchar con intercalaciones de SQL. Se recomienda usar un origen de ADO.NET si la tabla de origen contiene las columnas char o varchar con intercalaciones de SQL. 

  
## <a name="Locks"></a>Comportamiento de bloqueo  
Al cargar datos con Integration Services, SQL ServerPDW utiliza bloqueos de fila para actualizar datos en la tabla de destino. Esto significa que cada fila se bloquea para la lectura y escritura mientras se actualiza. Las filas de la tabla de destino no se bloquean mientras se cargan los datos en la tabla de ensayo.  
  
## <a name="Examples"></a>Ejemplos  
  
### <a name="Walkthrough"></a>A. Carga simple de archivo plano  
El siguiente tutorial muestra una carga de datos simple con Integration Services para cargar datos de archivo sin formato en un dispositivo PDW de SQL Server.  En este ejemplo se da por supuesto que ya se ha instalado Integration Services en el equipo cliente y el destino PDW de SQL Server se ha instalado, como se describió anteriormente.  
  
En este ejemplo se cargará en el `Orders` tabla, que tiene el siguiente DDL. El `Orders` tabla forma parte de la `LoadExampleDB` base de datos.  
  
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
  
En preparación para la carga, cree el archivo sin formato `exampleLoad.txt`, que contiene los datos de carga:  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
En primer lugar, cree un paquete de Integration Services mediante la realización de estos pasos:  
  
1.  En SQL Server Data Tools \(SSDT\), seleccione **archivo**, **New**y, a continuación, **proyecto**. Seleccione **proyecto de Integration Services** entre las opciones enumeradas. Nombre de este proyecto `ExampleLoad`y haga clic en **Aceptar**.  
  
2.  Haga clic en el **flujo de Control** pestaña y, a continuación, arrastre el **Data Flow Task** desde el **cuadro de herramientas** a la **flujo de Control** panel.  
  
3.  Haga clic en el **de flujo de datos** pestaña y, a continuación, arrastre **Flat File Source** desde el **cuadro de herramientas** a la **de flujo de datos** panel. Haga doble clic en el cuadro que acaba de crear para abrir el **Editor de origen de archivos planos**.  
  
4.  Haga clic en **Connection Manager** y, a continuación, haga clic en **New**.  
  
5.  En el **el nombre del Administrador de conexión** , escriba un nombre descriptivo para la conexión. En este ejemplo, `Example Load Flat File CM`.  
  
6.  Haga clic en **examinar** y seleccione el `ExampleLoad.txt` archivo desde el equipo local.  
  
7.  Puesto que el archivo sin formato contiene una fila con los nombres de columna, haga clic en el **los nombres de columna en la primera fila de datos** cuadro.  
  
8.  Haga clic en **columnas** en la columna izquierda y la versión preliminar se interpretaron correctamente los datos que se cargarán para asegurarse de que los nombres de columna y los datos.  
  
9. Haga clic en **avanzadas** en la columna izquierda. Haga clic en cada nombre de columna para revisar el tipo de datos que se ha asociado con los datos. Escriba los cambios en el cuadro de modo que los tipos de datos de los datos cargados será compatibles con los tipos de columna de destino.  
  
10. Haga clic en **Aceptar** para guardar el Administrador de conexiones.  
  
11. Haga clic en **Aceptar** para salir del **Editor de origen de archivos planos**.  
  
Especifique el destino del flujo de datos.  
  
1.  Arrastre el **destino PDW de SQL Server** desde el **cuadro de herramientas** a la **de flujo de datos** panel.  
  
2.  Haga doble clic en el cuadro que acaba de crear para cargar el **Editor de destino de SQL Server PDW**.  
  
3.  Haga clic en la flecha abajo junto a **Connection Manager**.  
  
4.  Seleccione **crear una nueva conexión**.  
  
5.  Rellene la información de la base de datos de destino, usuario, contraseña y servidor con información específica de su dispositivo. (Los ejemplos se muestran a continuación). A continuación, haga clic en **Aceptar**.  
  
    Para las conexiones InfiniBand, **nombre del servidor**: escriba < nombre del dispositivo >-SQLCTL01, 17001.  
  
    Para las conexiones Ethernet, **nombre del servidor**: escriba la dirección IP del clúster de nodo de Control, comas, el puerto 17001. Por ejemplo, 10.192.63.134,17001.  
  
    **Usuario:**`user1`  
  
    **Contraseña:**`password1`  
  
    **Base de datos de destino:**`LoadExampleDB`  
  
6.  Seleccione la tabla de destino: `Orders`.  
  
7.  Seleccione **Append** como el modo de carga y haga clic en **Aceptar**.  
  
Especificar el flujo de datos de origen al destino.  
  
1.  En el **de flujo de datos** panel, arrastre la flecha verde de la **Flat File Source** cuadro a la **destino PDW de SQL Server** cuadro.  
  
2.  Haga doble clic en el **destino PDW de SQL Server** cuadro poder ver el **Editor de destino de SQL Server PDW** nuevo. Debería ver los nombres de columna del archivo plano a la izquierda, bajo **columnas de entrada no asignadas**. Debería ver los nombres de columna de la tabla de destino a la derecha, bajo **columnas de destino no asignadas**. Asigne las columnas arrastrando o haga doble clic en los nombres de columna coincidentes en el **columnas de entrada no asignadas** y **columnas de destino no asignadas** listas para la **columnas asignadas**cuadro. Haga clic en **Aceptar** para guardar la configuración.  
  
3.  Guardar el paquete, haga clic en **guardar** en el **archivo** menú.  
  
Ejecute el paquete en el equipo de Integration Services.  
  
1.  En los servicios de integración**el Explorador de soluciones** (columna derecha), haga clic en `Package.dtsx` y seleccione **Execute**.  
  
2.  El paquete se ejecutará y se mostrará el progreso y los errores en el **progreso** panel. Use un cliente SQL para confirmar la carga, o supervisar la carga a través de la consola de administración de PDW de SQL Server.  
  
## <a name="see-also"></a>Vea también  
[Crear una tarea de secuencia de comandos que usa el adaptador de destino de SSIS PDW](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
[Diseño e implementación de paquetes (Integration Services)](http://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx)  
[Tutorial: Crear un paquete básico mediante un asistente](http://technet.microsoft.com/library/ms365330\(v=sql11\).aspx)  
[Introducción (Integration Services)](http://go.microsoft.com/fwlink/?LinkId=202412)  
[Ejemplo de generación dinámica de paquetes](http://go.microsoft.com/fwlink/?LinkId=202413)  
[Diseñar paquetes SSIS para el paralelismo (vídeo de SQL Server)](http://msdn.microsoft.com/library/dd795221.aspx)  
[Ejemplos de comunidad de Microsoft SQL Server: Servicios de integración](http://go.microsoft.com/fwlink/?LinkId=202415)  
[Mejorar las cargas incrementales con la captura de datos modificados](../integration-services/change-data-capture/change-data-capture-ssis.md)  
[Transformación Dimensión de variación lenta](../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)  
[Tarea Inserción masiva](../integration-services/control-flow/bulk-insert-task.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->
