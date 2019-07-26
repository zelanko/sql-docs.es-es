---
title: Guardar y cargar objetos de R desde SQL Server mediante ODBC
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 46c25083133677b382b33480ac5674f1786a7bf8
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469923"
---
# <a name="save-and-load-r-objects-from-sql-server-using-odbc"></a>Guardar y cargar objetos de R desde SQL Server mediante ODBC
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server R Services puede almacenar objetos serializados de R en una tabla y luego cargar el objeto desde la tabla si es necesario, sin tener que volver a ejecutar el código R ni reciclar el modelo. Esta capacidad de guardar objetos de R en una base de datos es fundamental para escenarios como el reciclaje y el guardado de un modelo y su uso más adelante para puntuación o análisis.

Para mejorar el rendimiento de este paso fundamental, el paquete **RevoScaleR** ahora incluye nuevas funciones de serialización y deserialización que mejoran considerablemente el rendimiento y almacenan el objeto de forma más compacta. En este artículo se describen estas funciones y cómo usarlas.

## <a name="overview"></a>Información general

El paquete **RevoScaleR** ahora incluye nuevas funciones que facilitan la tarea de guardar objetos de R en SQL Server y luego leerlos desde la tabla de SQL Server. En general, cada llamada de función utiliza un almacén de valores de clave simple, en el que la clave es el nombre del objeto y el valor asociado a la clave es el objeto varbinary R que se va a colocar dentro o fuera de una tabla.

Para guardar objetos de R en SQL Server directamente desde un entorno de R, debe hacer lo siguiente:

+ estableció una conexión a SQL Server mediante el origen de datos *RxOdbcData* .
+ Llamar a las nuevas funciones a través de la conexión ODBC
+ Opcionalmente, puede especificar que no se serialice el objeto. A continuación, elija un nuevo algoritmo de compresión que se usará en lugar del algoritmo de compresión predeterminado.

De forma predeterminada, cualquier objeto al que se llame desde R para moverlo a SQL Server se serializa y se comprime. Por el contrario, cuando se carga un objeto desde una tabla de SQL Server para usarlo en el código R, el objeto se deserializa y se descomprime.

## <a name="list-of-new-functions"></a>Lista de nuevas funciones

- `rxWriteObject` escribe un objeto de R en SQL Server mediante el origen de datos ODBC.

- `rxReadObject` lee un objeto de R desde una base de datos de SQL Server mediante un origen de datos ODBC

- `rxDeleteObject` elimina un objeto de R de la base de datos de SQL Server especificada en el origen de datos ODBC. Si hay varios objetos que se identifican mediante la combinación de clave y versión, se eliminan todos.

- `rxListKeys` enumera todos los objetos disponibles como pares de clave y valor. Esto ayuda a determinar los nombres y las versiones de los objetos de R.

Para obtener ayuda detallada sobre la sintaxis de cada función, use la Ayuda de R. Los detalles también están disponibles en la [referencia de ScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler).

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
