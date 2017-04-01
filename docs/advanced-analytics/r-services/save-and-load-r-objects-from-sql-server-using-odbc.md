---
title: "Guardar y cargar objetos de R desde SQL Server mediante ODBC | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 6ac2e971-6b4f-4c73-ba57-29c716abd057
caps.latest.revision: 8
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# Guardar y cargar objetos de R desde SQL Server mediante ODBC
SQL Server R Services puede almacenar objetos serializados de R en una tabla y luego cargar el objeto desde la tabla si es necesario, sin tener que volver a ejecutar el código R ni reciclar el modelo. Esta capacidad de guardar objetos de R en una base de datos es fundamental para escenarios como el reciclaje y el guardado de un modelo y su uso más adelante para puntuación o análisis. 

Para mejorar el rendimiento de este paso fundamental, el paquete **RevoScaleR** ahora incluye nuevas funciones de serialización y deserialización que mejoran considerablemente el rendimiento y almacenan el objeto de forma más compacta. Además, puede guardar objetos de R en SQL Server directamente desde un entorno de R si llama a estas nuevas funciones a través de una conexión ODBC con *RxOdbcData*.

## <a name="overview"></a>Información general

El paquete **RevoScaleR** ahora incluye nuevas funciones que facilitan la tarea de guardar objetos de R en SQL Server y luego leerlos desde la tabla de SQL Server. Estas funciones exigen que se establezca una conexión a SQL Server mediante el origen de datos *RxOdbcData*.

En general, las llamadas a la función se modelan según un almacén de valores de clave simple, en el que la clave es el nombre del objeto y el valor asociado a la clave es el objeto varbinary de R que se va a mover dentro o fuera de una tabla. 

- De forma predeterminada, cualquier objeto al que se llame desde R para moverlo a SQL Server se serializa y se comprime. 
- Por el contrario, cuando se carga un objeto desde una tabla de SQL Server para usarlo en el código R, el objeto se deserializa y se descomprime.
- Opcionalmente, puede especificar que no se serialice el objeto y puede elegir un nuevo algoritmo de compresión en lugar del predeterminado.


## <a name="new-functions"></a>Funciones nuevas

- `rxWriteObject` escribe un objeto de R en SQL Server mediante el origen de datos ODBC. 

- `rxReadObject` lee un objeto de R desde una base de datos de SQL Server mediante un origen de datos ODBC

- `rxDeleteObject` elimina un objeto de R de la base de datos de SQL Server especificada en el origen de datos ODBC. Si hay varios objetos que se identifican mediante la combinación de clave y versión, se eliminan todos.

- `rxListKeys` enumera todos los objetos disponibles como pares de clave y valor. Esto ayuda a determinar los nombres y las versiones de los objetos de R.

Para obtener ayuda detallada sobre la sintaxis de cada función, use la Ayuda de R. Habrá disponibles detalles en la [referencia de ScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) en MSDN en una fecha posterior.

## <a name="how-to-store-r-objects-in-sql-server-using-odbc"></a>Cómo almacenar objetos de R en SQL Server mediante ODBC

Este procedimiento muestra cómo usar las nuevas funciones para crear un modelo y guardarlo en SQL Server.

1. Configure la cadena de conexión de SQL Server.
   ```R
   conStr <- 'Driver={SQL Server};Server=localhost;Database=storedb;Trusted_Connection=true'
   ```
2. Cree un objeto de origen de datos *rxOdbcData* en R con la cadena de conexión.
   ```R
   ds <- RxOdbcData(table="robjects", connectionString=conStr)
   ```

3. Elimine la tabla si ya existe y no quiere realizar un seguimiento de las versiones anteriores de los objetos.

   ```R
   if(rxSqlServerTableExists(ds@table, ds@connectionString)) {
       rxSqlServerDropTable(ds@table, ds@connectionString)
       }
   ```
   
4. Defina una tabla que se pueda usar para almacenar objetos binarios.

   ```R
   ddl <- paste(" CREATE TABLE [", ds@table, "] 
      (","  [id] varchar(200) NOT NULL,
       "," [value] varbinary(max),
       "," CONSTRAINT unique_id UNIQUE (id))", 
       sep = "") 
   ```
5. Abra la conexión de ODBC para crear la tabla y, cuando haya finalizado la instrucción DDL, cierre la conexión.

   ```R
    rxOpen(ds, "w") 
    rxExecuteSQLDDL(ds, ddl) 
    rxClose(ds)
    ```
6. Genere los objetos de R que quiere almacenar.

   ```R
   infertLogit <- rxLogit(case ~ age + parity + education + spontaneous + induced, 
     data = infert)
   ```
6. Use el objeto *RxOdbcData* creado anteriormente para guardar el modelo en la base de datos.

   ```R
   rxWriteObject(ds, "logit.model", infertLogit)
   ```

## <a name="how-to-read-r-objects-from-sql-server-using-odbc"></a>Cómo leer objetos de R desde SQL Server mediante ODBC

Este procedimiento muestra cómo usar las nuevas funciones para cargar un modelo desde SQL Server.

1. Configure la cadena de conexión de SQL Server.

   ```R
   conStr2 <- 'Driver={SQL Server};Server=localhost;Database=storedb;Trusted_Connection=true'
   ```
2. Cree un objeto de origen de datos *rxOdbcData* en R con la cadena de conexión.

   ```R
   ds <- RxOdbcData(table="robjects", connectionString=conStr2)
   ```
3. Lea el modelo desde la tabla al especificar su nombre de objeto de R.

   ```R
    infertLogit2 <- rxReadObject(ds, "logit.model")
   ```

## <a name="see-also"></a>Vea también

[Características y tareas de R Services](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)
