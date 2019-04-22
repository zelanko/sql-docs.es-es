---
title: Consultar datos externos en Oracle
titleSuffix: SQL Server big data clusters
description: Este tutorial muestra cómo consultar datos de Oracle desde un clúster de macrodatos de 2019 de SQL Server (versión preliminar). Crear una tabla externa a través de los datos de Oracle y, a continuación, ejecutar una consulta.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/12/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 139c5dd5ade04c3d1a71412060f823d492843ecb
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58859986"
---
# <a name="tutorial-query-oracle-from-a-sql-server-big-data-cluster"></a>Tutorial: Consultas de Oracle desde un clúster de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este tutorial muestra cómo consultar datos de Oracle desde un clúster de macrodatos de SQL Server 2019. Para ejecutar este tutorial, necesita tener acceso a un servidor de Oracle. Si no tiene acceso, en este tutorial puede dar una idea de cómo funciona la virtualización de datos para orígenes de datos externos en el clúster de macrodatos de SQL Server.

En este tutorial, obtendrá información sobre cómo:

> [!div class="checklist"]
> * Crear una tabla externa para los datos en una base de datos de Oracle externa.
> * Únase a estos datos con datos de gran valor en la instancia maestra.

> [!TIP]
> Si lo prefiere, puede descargar y ejecutar un script para los comandos en este tutorial. Para obtener instrucciones, consulte el [ejemplos de datos de virtualización](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization) en GitHub.

## <a id="prereqs"></a> Requisitos previos

- [Herramientas de datos de gran tamaño](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
- [Cargar datos de ejemplo en el clúster de macrodatos](tutorial-load-sample-data.md)

## <a name="create-an-oracle-table"></a>Crear una tabla de Oracle

Los pasos siguientes crean una tabla de ejemplo denominada `INVENTORY` en Oracle.

1. Conectarse a una instancia de Oracle y la base de datos que desea usar para este tutorial.

1. Ejecute la siguiente instrucción para crear el `INVENTORY` tabla:

   ```sql
    CREATE TABLE "INVENTORY"
    (
        "INV_DATE" NUMBER(10,0) NOT NULL,
        "INV_ITEM" NUMBER(10,0) NOT NULL,
        "INV_WAREHOUSE" NUMBER(10,0) NOT NULL,
        "INV_QUANTITY_ON_HAND" NUMBER(10,0)
    );

    CREATE INDEX INV_ITEM ON HR.INVENTORY(INV_ITEM);
    ```

1. Importar el contenido de la **inventory.csv** archivo en esta tabla. Este archivo se creó con los scripts de creación de ejemplo en el [requisitos previos](#prereqs) sección.

## <a name="create-an-external-data-source"></a>Crear un origen de datos externos

El primer paso es crear un origen de datos externos que puede tener acceso al servidor de Oracle.

1. En Azure Data Studio, conéctese a la instancia principal de SQL Server del clúster de macrodatos. Para obtener más información, consulte [conectar a la instancia principal de SQL Server](connect-to-big-data-cluster.md#master).

1. Haga doble clic en la conexión en el **servidores** ventana para mostrar el panel del servidor para la instancia principal de SQL Server. Seleccione **nueva consulta**.

   ![Consulta de la instancia principal de SQL Server](./media/tutorial-query-oracle/sql-server-master-instance-query.png)

1. Ejecute el siguiente comando de Transact-SQL para cambiar el contexto para el **ventas** base de datos en la instancia maestra.

   ```sql
   USE Sales
   GO
   ```

1. Crear una credencial con ámbito de base de datos para conectarse al servidor de Oracle. Proporcione las credenciales adecuadas para su servidor de Oracle en la siguiente instrucción.

   ```sql
   CREATE DATABASE SCOPED CREDENTIAL [OracleCredential]
   WITH IDENTITY = '<oracle_user,nvarchar(100),SYSTEM>', SECRET = '<oracle_user_password,nvarchar(100),manager>';
   ```

1. Crear un origen de datos externo que apunta al servidor de Oracle.

   ```sql
   CREATE EXTERNAL DATA SOURCE [OracleSalesSrvr]
   WITH (LOCATION = 'oracle://<oracle_server,nvarchar(100)>',CREDENTIAL = [OracleCredential]);
   ```

## <a name="create-an-external-table"></a>Crear una tabla externa

A continuación, cree una tabla externa denominada **iventory_ora** a través de la `INVENTORY` tabla en el servidor de Oracle.

```sql
CREATE EXTERNAL TABLE [inventory_ora]
    ([inv_date] DECIMAL(10,0) NOT NULL, [inv_item] DECIMAL(10,0) NOT NULL,
    [inv_warehouse] DECIMAL(10,0) NOT NULL, [inv_quantity_on_hand] DECIMAL(10,0))
WITH (DATA_SOURCE=[OracleSalesSrvr],
        LOCATION='<oracle_service_name,nvarchar(30),xe>.<oracle_schema,nvarchar(128),HR>.<oracle_table,nvarchar(128),INVENTORY>');
```

> [!NOTE]
> Los nombres de tabla y los nombres de columna utilizarán ANSI SQL identificador entre comillas al realizar una consulta en Oracle. Como resultado, los nombres distinguen mayúsculas de minúsculas. Es importante especificar el nombre de la definición de tabla externa que coincida con mayúsculas y minúsculas de los nombres de tabla y columna en los metadatos de Oracle.

## <a name="query-the-data"></a>Consultar los datos

Ejecute la siguiente consulta para combinar los datos el `iventory_ora` tabla externa con las tablas locales `Sales` base de datos.

```sql
SELECT TOP(100) w.w_warehouse_name, i.inv_item, SUM(i.inv_quantity_on_hand) as total_quantity
  FROM [inventory_ora] as i
  JOIN item as it
    ON it.i_item_sk = i.inv_item
  JOIN warehouse as w
    ON w.w_warehouse_sk = i.inv_warehouse
 WHERE it.i_category = 'Books' and i.inv_item BETWEEN 1 and 18000 --> get items within specific range
 GROUP BY w.w_warehouse_name, i.inv_item;
```

## <a name="clean-up"></a>Limpiar

Use el siguiente comando para quitar los objetos de base de datos creados en este tutorial.

```sql
DROP EXTERNAL TABLE [inventory_ora];
DROP EXTERNAL DATA SOURCE [OracleSalesSrvr] ;
DROP DATABASE SCOPED CREDENTIAL [OracleCredential];
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre cómo introducir datos en el grupo de datos:
> [!div class="nextstepaction"]
> [Cargar datos en el grupo de datos](tutorial-data-pool-ingest-sql.md)
