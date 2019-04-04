---
title: Virtualización de datos externos en SQL Server 2019 CTP 2.0 | Microsoft Docs
description: En esta página se detallan los pasos para usar al Asistente para crear tablas externas para un archivo CSV
author: Abiola
ms.author: aboke
ms.reviewer: jroth
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: polybase
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: dae0692bafd8c4de295a914c9da0ead5c6e3980b
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512962"
---
# <a name="use-the-external-table-wizard-with-csv-files"></a>Uso del Asistente para tablas externas con archivos CSV

SQL Server 2019 también permite virtualizar los datos desde un archivo CSV en HDFS.  Este proceso permite que los datos permanezcan en su ubicación original, pero puede **virtualizarlos** en una instancia de SQL Server para que se puedan consultar como cualquier otra tabla de SQL Server. Esta característica minimizará la necesidad de procesos ETL. Esto es posible gracias a los conectores de PolyBase. Para más información sobre la virtualización de datos, vea el documento de [introducción a PolyBase](polybase-guide.md).

## <a name="prerequisite"></a>Requisito previo

A partir de CTP 2.4, el grupo de datos y los orígenes de datos externos del grupo de almacenamiento ya no se crean de forma predeterminada en el clúster de macrodatos. Antes de usar el asistente, cree el origen de datos externo predeterminado **SqlStoragePool** en la base de datos de destino con la siguiente consulta Transact-SQL. Primero asegúrese de cambiar el contexto de la consulta a la base de datos de destino.

```sql
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
  BEGIN
    IF SERVERPROPERTY('ProductLevel') = 'CTP2.3'
      CREATE EXTERNAL DATA SOURCE SqlStoragePool
      WITH (LOCATION = 'sqlhdfs://service-mssql-controller:8080');
    ELSE IF SERVERPROPERTY('ProductLevel') = 'CTP2.4'
      CREATE EXTERNAL DATA SOURCE SqlStoragePool
      WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
  END
```

## <a name="launch-the-external-table-wizard"></a>Inicio del Asistente para tablas externas

Conéctese a la raíz de HDFS mediante la dirección IP. Expanda los elementos del Explorador de objetos. Después, seleccione uno de los archivos CSV del que quiera virtualizar los datos en una instancia existente de SQL Server. Haga clic con el botón derecho en la base de datos y seleccione **Create External Table From CSV File** (Crear tabla externa a partir del archivo CSV) en el menú contextual. También puede crear tablas externas a partir de archivos CSV desde una carpeta de HDFS si los archivos de la carpeta siguen el mismo esquema. Esto permitiría la virtualización de los datos en un nivel de carpeta sin necesidad de procesar archivos individuales y obtener un conjunto de resultados combinados de los datos combinados. Esta acción inicia el Asistente para virtualizar datos. También puede iniciar el Asistente para virtualizar datos desde la paleta de comandos escribiendo Ctrl+Mayús+P (en Windows) y Cmd+Mayús+P (en Mac).

![Asistente para virtualizar datos](media/data-virtualization/csv-virtualize-data-wizard.png)

## <a name="connect-to-a-sql-server-master-instance"></a>Conexión a una instancia principal de SQL Server

Aquí se puede especificar a qué instancia principal de SQL se conectará con la información de IP, puerto y credenciales. Se puede acceder a las conexiones guardadas anteriormente a través del cuadro de lista desplegable **Conexiones activas de SQL Server**. 
> [!NOTE]
>Si usa una conexión guardada, se bloquearán los demás campos.


![Selección de un origen de datos](media/data-virtualization/csv-connect-to-master.png)

Haga clic en Siguiente para continuar al paso siguiente del asistente, en el que se establece la clave maestra de base de datos.

## <a name="select-destination-database"></a>Selección de la base de datos de destino

En este paso, elegirá la base de datos de destino en la que quiere virtualizar los datos. El campo de lista desplegable contendrá todas las bases de datos aceptables en la instancia principal de SQL especificada en la pantalla anterior. Aquí también se puede asignar un nombre a la tabla externa nueva y ver el esquema que va a usar.

![Creación de la clave maestra de una base de datos](media/data-virtualization/csv-select-destination.png)


## <a name="preview-data"></a>Vista previa de los datos

En esta ventana, podrá ver una vista previa de las primeras 50 filas del archivo CSV para la validación.

Cuando haya terminado de visualizar la vista previa, haga clic en "Siguiente" para continuar.

![Credenciales del origen de datos externo](media/data-virtualization/csv-preview-data.png)

## <a name="modify-columns"></a>Modificación de columnas

En la ventana siguiente, podrá modificar las columnas de la tabla externa que se va a crear. Se puede modificar el nombre de columna, cambiar el tipo de datos y permitir filas que acepten valores NULL. 

![Credenciales del origen de datos externo](media/data-virtualization/csv-modify-columns.png)


## <a name="summary"></a>Resumen

Este paso proporciona un resumen de las selecciones. Proporciona la instancia principal de SQL e información de la tabla externa propuesta. En este paso, verá la opción **"Generar Script"**, que creará en T-SQL los scripts con la sintaxis para crear el origen de datos externo, o bien **Crear**, que creará el objeto de origen de datos externo.

![Pantalla de resumen](media/data-virtualization/csv-virtualize-data-summary.png)

Si hace clic en "Crear", podrá ver la tabla externa creada en la base de datos de destino.

![Orígenes de datos externos](media/data-virtualization/csv-external-data-sources.png)

Si hace clic en **Generar Script**, verá la consulta Transact-SQL que se genera para crear el objeto de origen de datos externo.

![Generar script](media/data-virtualization/csv-generated-script.png)

> [!NOTE]
> Generar script solo debería verse en la última página del asistente. Actualmente, se muestra en todas las páginas.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos de SQL Server y los escenarios relacionados, consulte [What is SQL Server Big Data Cluster?](../../big-data-cluster/big-data-cluster-overview.md) (¿Qué son los clústeres de macrodatos de SQL Server?)
