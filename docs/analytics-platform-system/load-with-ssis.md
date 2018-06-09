---
title: Carga con Integration Services - almacenamiento de datos paralelos | Documentos de Microsoft
description: Proporciona información de referencia e implementación para cargar datos en el almacenamiento de datos paralelo (PDW) con los paquetes de SQL Server Integration Services (SSIS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 718a076822a4304e0ba951f3ca1903bb7c009e17
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34586067"
---
# <a name="load-data-with-integration-services-to-parallel-data-warehouse"></a>Carga los datos con Integration Services para almacenamiento de datos paralelos
Proporciona información de referencia e implementación para cargar datos en almacenamiento de datos paralelos de SQL Server mediante el uso de paquetes de SQL Server Integration Services (SSIS).  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](http://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx) on MSDN.  

-->
  
## <a name="Basics"></a>Conceptos básicos  
Integration Services es el componente de SQL Server de alto rendimiento extracción, transformación y carga (ETL) de datos y se utiliza normalmente para rellenar y actualizar un almacenamiento de datos.  
  
El adaptador de destino de PDW es un componente de servicios de integración que permite cargar datos en PDW con los paquetes de Integration Services dtsx. En un flujo de trabajo de paquete para ServerPDW de SQL, puede cargar y combinar datos de varios orígenes y cargar datos a varios destinos. Las cargas se producen en paralelo, en un paquete y entre varios paquetes que se ejecutan simultáneamente, hasta un máximo de 10 cargas ejecutándose en paralelo en el mismo dispositivo.  
  
Además de las tareas descritas en este tema, puede utilizar otras características de Integration Services para filtrar, transformar, analizar y limpiar los datos antes de cargarlos en el almacén de datos. También puede mejorar el flujo de trabajo del paquete mediante la ejecución de instrucciones SQL, la ejecución de paquetes secundarios o el envío de correo.  
  
Para obtener documentación completa de Integration Services, vea [SQL Server Integration Services](http://msdn.microsoft.com/library/ms141026(v=sql11).aspx).  
  
## <a name="HowToDeployPackage"></a>Métodos para ejecutar un paquete de Integration Services  
Utilice uno de estos métodos para ejecutar un paquete de Integration Services.  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>Ejecutar desde SQL Server 2008 R2 Business Intelligence Development Studio (BIDS)  
Para ejecutar el paquete desde dentro de BIDS, haga doble clic en el paquete y elija **Ejecutar paquete**.  
  
De forma predeterminada, BIDS ejecuta paquetes con archivos binarios de 64 bits. Esto viene determinado por la **Run64BitRuntime** propiedad del paquete. Para establecer esta propiedad, vaya a **el Explorador de soluciones**, haga doble clic en el proyecto y elija **propiedades**. En el **páginas de propiedades de servicios de integración**, vaya a **propiedades de configuración** y seleccione **depuración**. Verá el **Run64BitRuntime** propiedad en el **opciones de depuración**. Para utilizar tiempos de ejecución de 32 bits, establezca esta propiedad en **False**. Para utilizar tiempos de ejecución de 64 bits, establezca esta propiedad en **True**.  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>Ejecución de datos de SQL Server SQL Server 2012 herramientas  
Para ejecutar el paquete desde dentro de SQL Server Data Tools, haga doble clic en el paquete y elija **Ejecutar paquete**.  
  
### <a name="run-from-powershell"></a>Ejecución de PowerShell  
Para ejecutar el paquete de Windows PowerShell, utilizando la **dtexec** utilidad: `dtexec /FILE <packagePath>`  
  
Por ejemplo, `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
### <a name="run-from-a-windows-command-prompt"></a>Ejecución de Windows un símbolo del sistema 
Para ejecutar el paquete desde un símbolo del sistema de Windows, con el **dtexec** utilidad: `dtexec /FILE <packagePath>`  
  
Por ejemplo, `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="DataTypes"></a>Tipos de datos  
Al utilizar Integration Services para cargar datos desde un origen de datos a una base de datos de SQL Server PDW, se asignan primero los datos del origen de datos a tipos de datos de Integration Services. Esto permite que los datos de varios orígenes de datos se asignen a un conjunto común de tipos de datos.  
  
A continuación, se asignan los datos de Integration Services a tipos de datos de SQL Server PDW. Para cada tipo de datos de SQL Server PDW, la tabla siguiente enumeran los tipos de datos de Integration Services que se pueda convertir al tipo de datos de SQL Server PDW.  
  
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
  
**Compatibilidad limitada para la precisión del tipo de datos**  
  
PDW genera un error de validación si se asigna una columna de entrada DT_NUMERIC o DT_DECIMAL que contiene un valor con una precisión mayor que 28.  
  
**Tipos de datos no admitidos**  
  
PDW de SQL Server no admite los siguientes tipos de datos de Integration Services:  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
Para cargar las columnas que contienen datos de estos tipos en PDW de SQL Server, debe agregar una transformación de conversión de datos de nivel superior en el flujo de datos para convertir los datos a un tipo de datos compatible.  
  
## <a name="permissions"></a>Permisos  
Para ejecutar un paquete de carga de Integration Services, necesita:  
  
-   Permiso de carga en la base de datos.  
  
-   Aplicable INSERT, UPDATE, DELETE permisos en la tabla de destino.  
  
-   Si se usa una base de datos de almacenamiento provisional, el permiso Crear en la base de datos de almacenamiento provisional. Se trata de crear una tabla temporal.  
  
-   Si no se usa ninguna base de datos de almacenamiento provisional, el permiso Crear en la base de datos de destino. Se trata de crear una tabla temporal.  
  
## <a name="GenRemarks"></a>Observaciones generales  
Cuando un paquete de Integration Services tiene varios destinos de PDW de SQL Server que se ejecuta y una de las conexiones se termina, Integration Services detiene la inserción de datos a todos los destinos de SQL Server PDW.  
  
## <a name="Limits"></a>Limitaciones y restricciones  
Para un paquete de Integration Services, el número de destinos de PDW de SQL Server para el mismo origen de datos está limitado por el número máximo de cargas activas. Se preconfigura el máximo y no es configurable por el usuario. 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
Cada destino de paquete de Integration Services para el mismo origen de datos se considera como una carga mientras se ejecuta el paquete. Por ejemplo, suponga que el máximo de cargas activas es 10. El paquete no se ejecutará si se intenta abrir 11 o más destinos para el mismo origen de datos.  
  
Varios paquetes pueden ejecutarse simultáneamente siempre y cuando cada paquete no utilice más del máximo de cargas activas. Por ejemplo, si el máximo de cargas activas es 10, puede ejecutar simultáneamente dos paquetes que usen 10 destinos cada uno. Se ejecutará un paquete mientras otro espera en la cola de carga.  
  
Si el número de cargas en la cola de carga supera el máximo de cargas en cola, el paquete no se ejecutará. Por ejemplo, si el número máximo de cargas es 10 por dispositivo y el número máximo de cargas en cola es 40 por dispositivo, puede ejecutar simultáneamente cinco paquetes de Integration Services que cada uno de ellos abran 10 destinos. Si intenta ejecutar un sexto paquete, no se ejecutará.  

> [!IMPORTANT]
> Usa un origen de datos de OLE DB en SSIS con el adaptador de destino PDW, puede provocar daños en los datos si la tabla de origen contiene las columnas char y varchar con intercalaciones de SQL. Se recomienda utilizar un origen ADO.NET si la tabla de origen contiene las columnas char o varchar con intercalaciones de SQL. 

  
## <a name="Locks"></a>Comportamiento de bloqueo  
Cuando se cargan datos con Integration Services, SQL ServerPDW utiliza bloqueos de fila para actualizar datos en la tabla de destino. Esto significa que cada fila se bloquea para la lectura y escritura mientras se actualiza. Las filas de la tabla de destino no se bloquean mientras se cargan los datos en la tabla de ensayo.  
  
## <a name="Examples"></a>Ejemplos  
  
### <a name="Walkthrough"></a>A. Carga simple de archivo plano  
En el siguiente tutorial se muestra una carga de datos simple con Integration Services para cargar datos de archivo sin formato a un dispositivo PDW de SQL Server.  En este ejemplo se da por supuesto que Integration Services ya se ha instalado en el equipo cliente y el destino PDW de SQL Server se ha instalado, como se describió anteriormente.  
  
En este ejemplo se cargará en el `Orders` tabla, que tiene la siguiente instrucción DDL. El `Orders` tabla forme parte de la `LoadExampleDB` base de datos.  
  
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
  
En primer lugar, cree un paquete de Integration Services, realice estos pasos:  
  
1.  En SQL Server Data Tools \(SSDT\), seleccione **archivo**, **New**y, a continuación, **proyecto**. Seleccione **proyecto de Integration Services** entre las opciones enumeradas. Nombre de este proyecto `ExampleLoad`y haga clic en **Aceptar**.  
  
2.  Haga clic en el **flujo de Control** ficha y, a continuación, arrastre el **tarea flujo de datos** desde el **cuadro de herramientas** a la **flujo de Control** panel.  
  
3.  Haga clic en el **de flujo de datos** pestaña y, a continuación, arrastre **origen de archivo plano** desde el **cuadro de herramientas** a la **de flujo de datos** panel. Haga doble clic en el cuadro que acaba de crear para abrir el **Editor de origen de archivos planos**.  
  
4.  Haga clic en **Connection Manager** y, a continuación, haga clic en **nuevo**.  
  
5.  En el **el nombre del Administrador de conexión** cuadro, escriba un nombre descriptivo para la conexión. En este ejemplo, `Example Load Flat File CM`.  
  
6.  Haga clic en **examinar** y seleccione la `ExampleLoad.txt` archivo desde el equipo local.  
  
7.  Puesto que el archivo sin formato contiene una fila con los nombres de columna, haga clic en el **nombres de columna en la primera fila de datos** cuadro.  
  
8.  Haga clic en **columnas** en la columna izquierda y la vista previa se interpretaron correctamente los datos que se cargarán para asegurarse de que los nombres de columna y los datos.  
  
9. Haga clic en **avanzadas** en la columna izquierda. Haga clic en cada nombre de columna para revisar el tipo de datos que se ha asociado con los datos. Escriba los cambios en el cuadro de modo que los tipos de datos de los datos cargados será compatibles con los tipos de columna de destino.  
  
10. Haga clic en **Aceptar** para guardar el Administrador de conexiones.  
  
11. Haga clic en **Aceptar** para salir del **Editor de origen de archivos planos**.  
  
Especifique el destino del flujo de datos.  
  
1.  Arrastre el **destino PDW de SQL Server** desde el **cuadro de herramientas** a la **de flujo de datos** panel.  
  
2.  Haga doble clic en el cuadro que acaba de crear para cargar la **Editor de destino de SQL Server PDW**.  
  
3.  Haga clic en la flecha abajo junto a **Connection Manager**.  
  
4.  Seleccione **crear una nueva conexión**.  
  
5.  Rellene la información de la base de datos de servidor, usuario, contraseña y el destino con información específica de su dispositivo. (Los ejemplos se muestran a continuación). A continuación, haga clic en **Aceptar**.  
  
    Para las conexiones InfiniBand, **nombre del servidor**: escriba < nombre del dispositivo >-SQLCTL01, 17001.  
  
    Para las conexiones Ethernet, **nombre del servidor**: escriba la dirección IP del clúster de nodo de Control, la coma, el puerto 17001. Por ejemplo, 10.192.63.134,17001.  
  
    **Usuario:**`user1`  
  
    **Contraseña:**`password1`  
  
    **Base de datos de destino:**`LoadExampleDB`  
  
6.  Seleccione la tabla de destino: `Orders`.  
  
7.  Seleccione **anexado** como el modo de carga y haga clic en **Aceptar**.  
  
Especificar el flujo de datos de origen a destino.  
  
1.  En el **de flujo de datos** panel, arrastre la flecha verde de la **origen de archivo plano** cuadro a la **destino PDW de SQL Server** cuadro.  
  
2.  Haga doble clic en el **destino PDW de SQL Server** cuadro para que ver el **Editor de destino de SQL Server PDW** nuevo. Debería ver los nombres de columna del archivo plano de la izquierda, bajo **columnas de entrada no asignadas**. Debería ver los nombres de columna de la tabla de destino a la derecha, en **columnas de destino no asignadas**. Asigne las columnas arrastrando o haciendo doble clic en los nombres de columna coincidentes en el **columnas de entrada no asignadas** y **columnas de destino no asignadas** listas para el **columnas asignadas**cuadro. Haga clic en **Aceptar** para guardar la configuración.  
  
3.  Guardar el paquete, haga clic en **guardar** en el **archivo** menú.  
  
Ejecute el paquete en el equipo de servicios de integración.  
  
1.  En los servicios de integración**el Explorador de soluciones** (columna derecha), haga clic en `Package.dtsx` y seleccione **Execute**.  
  
2.  El paquete se ejecutará y el progreso y los errores se mostrarán en el **progreso** panel. Utilice a un cliente SQL para confirmar la carga, o supervisar la carga a través de la consola de administración de SQL Server PDW.  
  
## <a name="see-also"></a>Vea también  
[Crear una tarea de secuencia de comandos que usa el adaptador de destino de SSIS PDW](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](http://msdn.microsoft.com/library/ms141026\(v=sql11\).aspx)  
[Diseñar e implementar paquetes (Integration Services)](http://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx)  
[Tutorial: Crear un paquete básico mediante un asistente](http://technet.microsoft.com/library/ms365330\(v=sql11\).aspx)  
[Introducción (Integration Services)](http://go.microsoft.com/fwlink/?LinkId=202412)  
[Ejemplo para generar el paquete dinámico](http://go.microsoft.com/fwlink/?LinkId=202413)  
[Diseñar paquetes SSIS para el paralelismo (vídeo de SQL Server)](http://msdn.microsoft.com/library/dd795221.aspx)  
[Microsoft SQL Server Community ejemplos: Servicios de integración](http://go.microsoft.com/fwlink/?LinkId=202415)  
[Mejorar las cargas incrementales con la captura de datos modificados](http://msdn.microsoft.com/library/bb895315\(v=sql11\).aspx)  
[Transformación Dimensión de variación lenta](http://msdn.microsoft.com/library/ms141715\(v=sql11\).aspx)  
[Tarea Inserción masiva](http://msdn.microsoft.com/library/ms141239\(v=sql11\).aspx)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->
