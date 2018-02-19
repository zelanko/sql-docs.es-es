---
title: 'Actualizados: documentos de bases de datos relacionales | Microsoft Docs'
description: "Muestra fragmentos del contenido actualizado en la documentación de bases de datos relacionales que ha cambiado recientemente."
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: relational-databases
ms.date: 02/03/2018
ms.openlocfilehash: 38f9ee55137c54adddb07fbe9f3b74dd43d51a3a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Nuevos y actualizados recientemente: documentos de bases de datos relacionales



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; del **03-12-2017** &nbsp; al &nbsp; **03-02-2018**
- *Área temática:* &nbsp; **Bases de datos relacionales**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Almacenamiento de documentos JSON en SQL Server o SQL Database](json/store-json-documents-in-sql-tables.md)
2. [Evaluación de vulnerabilidad de SQL](security/sql-vulnerability-assessment.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Inicialización de archivos de base de datos](#TitleNum_1)
2. [Base de datos tempdb](#TitleNum_2)
3. [Datos JSON en SQL Server](#TitleNum_3)
4. [Lección 1: conectarse al motor de base de datos](#TitleNum_4)
5. [Administrar el tamaño del archivo de registro de transacciones](#TitleNum_5)
6. [bcp_bind](#TitleNum_6)
7. [Guía de diseño de índices de SQL Server](#TitleNum_7)
8. [sp_execute_external_script (Transact-SQL)](#TitleNum_8)
9. [Crear claves principales](#TitleNum_9)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-database-file-initializationdatabasesdatabase-instant-file-initializationmd"></a>1. &nbsp; [Inicialización de archivos de base de datos](databases/database-instant-file-initialization.md)

*Actualizado: 23-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Siguiente](#TitleNum_2))

<!-- Source markdown line 81.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c5f2aa53a8b43d4c43e0602cf945cb7c7028a27d 04c261c6588af1f53cda2fce3e9a86167c50b686  (PR=4702  ,  Filename=database-instant-file-initialization.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=3206a31870f8febab7d1718fa59fe0590d4d45db) -->



```
Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.
```

**Se aplica a:** SQL Server (a partir de SQL Server 2012 SP4, SQL Server 2014 SP2 y SQL Server 2016 hasta SQL Server 2017)

**Consideraciones de seguridad**

Al usar la inicialización instantánea de archivos (IFI), como el contenido del disco eliminado solo se sobrescribe cuando se escriben nuevos datos en los archivos, una entidad de seguridad no autorizada puede acceder al contenido eliminado hasta que algún otro dato se escriba en una área específica del archivo de datos. Mientras el archivo de la base de datos se adjunte a la instancia de SQL Server, este riesgo de divulgación de la información se reduce mediante la lista de control de acceso discrecional (DACL) del archivo. Con esta DACL, solamente la cuenta de servicio de SQL Server y el administrador local pueden acceder al archivo. Pero cuando el archivo está separado, un usuario o servicio que no tenga SE\_MANAGE\_VOLUME_NAME podrá acceder a él. Existe una consideración similar al crear una copia de seguridad de la base de datos: si el archivo de copia de seguridad no está protegido con una DACL adecuada, el contenido eliminado puede estar disponible para un usuario o servicio no autorizado.

Otra cosa que hay que tener en cuenta es que, cuando un archivo crece usando IFI, un administrador de SQL Server podría acceder a los contenidos de la página sin procesar y ver el contenido que se ha eliminado anteriormente.

Si los archivos de base de datos están hospedados en una red de área de almacenamiento, también es posible que esta presente siempre nuevas páginas inicializadas previamente y puede ser que configurar el sistema operativo para que vuelva a inicializar las páginas cree una sobrecarga innecesaria.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-tempdb-databasedatabasestempdb-databasemd"></a>2. &nbsp; [Base de datos tempdb](databases/tempdb-database.md)

*Actualizado: 17-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1) | [Siguiente](#TitleNum_3))

<!-- Source markdown line 100.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 337555ea28f4c3fdd6b78f1bfb4d62607a6bf92d 3257c92d6e2a88968fc44e5f6262c02cd0624635  (PR=0  ,  Filename=tempdb-database.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=45e6082acc29ba306525e7c08d2c22cc2b86eec3) -->



 Para obtener una descripción de estas opciones de la base de datos, vea [Opciones de ALTER DATABASE SET (Transact-SQL)](databases/../../t-sql/statements/alter-database-transact-sql-set-options.md).

**Base de datos tempdb en SQL Database**


|SLO|Tamaño de archivo de datos de tempdb máximo (MB)|Número de archivos de datos de tempdb|Tamaño máximo de datos de tempdb (MB)|
|---|---:|---:|---:|
|Básico|14 225|1|14 225|
|S0|14 225|1|14 225|
|S1|14 225|1|14 225|
|S2|14 225| 1|14 225|
|S3|32 768|1|32 768|
|S4|32 768|2|65,536|
|S6|32 768|3|98304|
|S7|32 768|6|196 608|
|S9|32 768|12|393 216|
|S12|32 768|12|393 216|
|P1|32 768|12|393 216|
|P2|32 768|12|393 216|
|P4|32 768|12|393 216|
|P6|32 768|12|393 216|
|P11|32 768|12|393 216|
|P15|32 768|12|393 216|
|Grupos elásticos premium (todas las configuraciones de DTU)|14 225|12|170 700|
|Grupos elásticos estándar (todas las configuraciones de DTU)|14 225|12|170 700|
|Grupos elásticos básicos (todas las configuraciones de DTU)|14 225|12|170 700|
||||




&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-json-data-in-sql-serverjsonjson-data-sql-servermd"></a>3. &nbsp; [Datos JSON en SQL Server](json/json-data-sql-server.md)

*Actualizado: 01-02-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_2) | [Siguiente](#TitleNum_4))

<!-- Source markdown line 233.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 62dd9c68d8cb72d6bf51b941a0731224514f0a7f 19e276637a463b412f2c29a84f9fb7d0b0f5fcc5  (PR=4783  ,  Filename=json-data-sql-server.md  ,  Dirpath=docs\relational-databases\json\  ,  MergeCommitSha40=73f18ae24a9a48234bf997ee9a2ef441bc4918b9) -->



-   [Load GeoJSON data into SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/loading-geojson-data-into-sql-server/) (Cargar datos GeoJSON en SQL Server 2016)

**Analizar datos JSON con consultas SQL**

Si tiene que filtrar o agregar datos JSON para elaborar informes, puede usar **OPENJSON** para transformar JSON en formato relacional. Luego puede usar las funciones integradas y Transact-SQL estándar para preparar los informes.

```
SELECT Tab.Id, SalesOrderJsonData.Customer, SalesOrderJsonData.Date
FROM   SalesOrderRecord AS Tab
          CROSS APPLY
     OPENJSON (Tab.json, N'$.Orders.OrdersArray')
           WITH (
              Number   varchar(200) N'$.Order.Number',
              Date     datetime     N'$.Order.Date',
              Customer varchar(200) N'$.AccountNumber',
              Quantity int          N'$.Item.Quantity'
           )
  AS SalesOrderJsonData
WHERE JSON_VALUE(Tab.json, '$.Status') = N'Closed'
ORDER BY JSON_VALUE(Tab.json, '$.Group'), Tab.DateModified
```



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-lesson-1-connecting-to-the-database-enginelesson-1-connecting-to-the-database-enginemd"></a>4. &nbsp; [Lección 1: Conexión al motor de base de datos](lesson-1-connecting-to-the-database-engine.md)

*Actualizado: 13-12-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_3) | [Siguiente](#TitleNum_5))

<!-- Source markdown line 79.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3c070935895450fd2ea054e2be9e1c48f7dc2b6c 0c386e3d47fb7f8f1e63b9301f0cafec2bc88ab0  (PR=4282  ,  Filename=lesson-1-connecting-to-the-database-engine.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=6e016a4ffd28b09456008f40ff88aef3d911c7ba) -->



2.  Seleccione **Motor de base de datos**.

    ![object-explorer](../relational-databases/media/object-explorer.png)

3.  En el cuadro **Nombre del servidor**, escriba el nombre de la instancia del motor de base de datos. Para la instancia predeterminada de SQL Server, el nombre de servidor es el nombre del equipo. Para una instancia con nombre de SQL Server, el nombre del servidor es *<nombre_equipo>***\\***<nombre_instancia>,* como **ACCTG_SRVR\SQLEXPRESS**. En la siguiente captura de pantalla se muestra la conexión a la instancia predeterminada (sin nombre) de SQL Server en un equipo denominado "PracticeComputer". El usuario que ha iniciado sesión en Windows es Mary del dominio Contoso. Al usar la autenticación de Windows, no puede cambiar el nombre de usuario.

    ![connect-to-server](../relational-databases/media/connect-to-server.png)

4.  Haga clic en **Conectar**.

> [!NOTE]
> En este tutorial se supone que no está familiarizado con SQL Server y no tiene problemas especiales para conectarse. Esto debería ser suficiente para la mayoría de las personas y hace que este tutorial sea simple. Para obtener pasos de solución de problemas detallados, consulte [Solucionar problemas de conexión al motor de base de datos de SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md).

**<a name="additional"></a>Autorizar conexiones adicionales**

Ahora que ya se ha conectado a SQL Server como administrador, una de las primeras tareas que debe realizar es autorizar a otros usuarios a conectarse. Para ello, cree un inicio de sesión y concédale autorización para obtener acceso a una base de datos como usuario. Los inicios de sesión pueden ser inicios de sesión con autenticación de Windows, que usan las credenciales de Windows, o bien inicios de sesión con autenticación de SQL Server, que almacenan la información de autenticación en SQL Server y son independientes de las credenciales de Windows. Utilice la autenticación de Windows siempre que sea posible.



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-manage-the-size-of-the-transaction-log-filelogsmanage-the-size-of-the-transaction-log-filemd"></a>5. &nbsp; [Administrar el tamaño del archivo de registro de transacciones](logs/manage-the-size-of-the-transaction-log-file.md)

*Actualizado: 17-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_4) | [Siguiente](#TitleNum_6))

<!-- Source markdown line 105.  ms.author= "jhubbard".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5847b31cf8f6003a380f0c8aaa289efdc55be678 84e45320d81db218cde17fbf8b9668a9ac3805a7  (PR=0  ,  Filename=manage-the-size-of-the-transaction-log-file.md  ,  Dirpath=docs\relational-databases\logs\  ,  MergeCommitSha40=45e6082acc29ba306525e7c08d2c22cc2b86eec3) -->



-   Un aumento de crecimiento pequeño puede generar demasiados [VLF](logs/../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) pequeños y puede reducir el rendimiento. Para determinar la distribución óptima de VLF para el tamaño de registro de transacciones actual de todas las bases de datos en una instancia determinada, así como los incrementos de tamaño necesarios para conseguir el tamaño requerido, consulte este [script](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs).

-   Un aumento de crecimiento grande puede generar demasiados [VLF](logs/../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) pequeños y grandes, y también puede afectar al rendimiento. Para determinar la distribución óptima de VLF para el tamaño de registro de transacciones actual de todas las bases de datos en una instancia determinada, así como los incrementos de tamaño necesarios para conseguir el tamaño requerido, consulte este [script](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs).

-   Incluso con el crecimiento automático habilitado, puede recibir un mensaje de que el registro de transacciones está lleno, si no puede crecer lo suficientemente rápido para satisfacer las necesidades de la consulta. Para obtener más información sobre cómo cambiar el aumento del crecimiento, vea [Opciones File y Filegroup de ALTER DATABASE &#40;Transact-SQL&#41;](logs/../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).

-   Aunque tenga varios archivos de registro en una base de datos, el rendimiento no mejorará, ya que los archivos de registro de transacciones no usan el [relleno proporcional](logs/../../relational-databases/pages-and-extents-architecture-guide.md#ProportionalFill), como los archivos de datos de un mismo grupo de archivos.

-   Puede configurar los archivos de registro para que se reduzcan automáticamente. Esto **no se recomienda** y la propiedad de base de datos **auto_shrink** está establecida en FALSE de manera predeterminada. Si **auto_shrink** está establecida en TRUE, el proceso de reducción automática solo reduce el tamaño de un archivo cuando más del 25 % de su espacio está sin usar.



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-bcpbindnative-client-odbc-extensions-bulk-copy-functionsbcp-bindmd"></a>6. &nbsp; [bcp_bind](native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)

*Actualizado: 30-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_5) | [Siguiente](#TitleNum_7))

<!-- Source markdown line 127.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d50791cef948ce8b3066438e317ab4d34d535258 e6f70559e7237cfc86dfc5746d218c08bec52af6  (PR=4762  ,  Filename=bcp-bind.md  ,  Dirpath=docs\relational-databases\native-client-odbc-extensions-bulk-copy-functions\  ,  MergeCommitSha40=60006e90d03fdb75b282bbc0dad3d40571bacacc) -->



 En esta tabla se muestran los tipos de datos enumerados válidos y los tipos de datos ODBC C correspondientes.

|eDataType|Tipo de C|
|-----------------------|------------|
|SQLTEXT|char *|
|SQLNTEXT|wchar_t *|
|SQLCHARACTER|char *|
|SQLBIGCHAR|char *|
|SQLVARCHAR|char *|
|SQLBIGVARCHAR|char *|
|SQLNCHAR|wchar_t *|
|SQLNVARCHAR|wchar_t *|
|SQLBINARY|unsigned char *|
|SQLBIGBINARY|unsigned char *|
|SQLVARBINARY|unsigned char *|
|SQLBIGVARBINARY|unsigned char *|
|SQLBIT|char|
|SQLBITN|char|
|SQLINT1|char|
|SQLINT2|short int|
|SQLINT4|INT|
|SQLINT8|_int64|
|SQLINTN|*cbIndicator*<br /> 1: SQLINT1<br /> 2: SQLINT2<br /> 4: SQLINT4<br /> 8: SQLINT8|
|SQLFLT4|FLOAT|
|SQLFLT8|FLOAT|
|SQLFLTN|*cbIndicator*<br /> 4: SQLFLT4<br /> 8: SQLFLT8|
|SQLDECIMALN|SQL_NUMERIC_STRUCT|
|SQLNUMERICN|SQL_NUMERIC_STRUCT|
|SQLMONEY|DBMONEY|
|SQLMONEY4|DBMONEY4|
|SQLMONEYN|*cbIndicator*<br /> 4: SQLMONEY4<br /> 8: SQLMONEY|
|SQLTIMEN|SQL_SS_TIME2_STRUCT|
|SQLDATEN|SQL_DATE_STRUCT|
|SQLDATETIM4|DBDATETIM4|
|SQLDATETIME|DBDATETIME|
|SQLDATETIMN|*cbIndicator*<br /> 4: SQLDATETIM4<br /> 8: SQLDATETIME|
|SQLDATETIME2N|SQL_TIMESTAMP_STRUCT|
|SQLDATETIMEOFFSETN|SQL_SS_TIMESTAMPOFFSET_STRUCT|
|SQLIMAGE|unsigned char *|
|SQLUDT|unsigned char *|
|SQLUNIQUEID|SQLGUID|
|SQLVARIANT|*Cualquier tipo de datos excepto:*<br />-   text<br />-   ntext<br />-   image<br />-   varchar(max)<br />-   varbinary(max)<br />-   nvarchar(max)<br />-   xml<br />-   timestamp|
|SQLXML|*Tipos de datos C admitidos:*<br />-   char*<br />-   wchar_t *<br />-   unsigned char *|



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-sql-server-index-design-guidesql-server-index-design-guidemd"></a>7. &nbsp; [Guía de diseño de índices de SQL Server](sql-server-index-design-guide.md)

*Actualizado: 02-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_6) | [Siguiente](#TitleNum_8))

<!-- Source markdown line 700.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bd09c9e66cd3cf5f3ebebe7ffa6e937978353169 8e5cbbf0063971676a8bafefba75aa5c7c28be61  (PR=0  ,  Filename=sql-server-index-design-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=74daee358fef75a25d75c69d971d08536c5bd2be) -->



A partir de SQL Server 2016, puede crear un **índice de almacén de columnas no agrupado actualizable en una tabla de almacén de filas**. El índice de columnas almacena una copia de los datos, por lo que necesita más almacenamiento. Sin embargo, los datos del índice de almacén de columnas se comprimen en un tamaño inferior al que requiere la tabla de almacén de filas.  Gracias a esto, se pueden ejecutar análisis en el índice de almacén de columnas y realizar transacciones en el índice de almacén de filas al mismo tiempo. El almacén de columnas se actualiza cuando cambian los datos de la tabla de almacén de filas, de modo que ambos índices trabajan con los mismos datos.

A partir de SQL Server 2016, puede tener **uno o varios índices de almacén de filas no agrupados en un índice de almacén de columnas**. Gracias a ello, podrá realizar búsquedas de tabla eficaces en el almacén de columnas subyacente. También habrá disponibles otras opciones. Por ejemplo, podrá aplicar una restricción de clave principal mediante una restricción UNIQUE en la tabla de almacén de filas. Puesto que un valor que no es único no se insertará en la tabla de almacén de filas, SQL Server no podrá insertar ese valor en el almacén de columnas.

**Consideraciones de rendimiento**


-   La definición del índice de almacén de columnas no agrupado admite el uso de una condición de filtrado. Para minimizar el impacto de rendimiento que tiene agregar un índice de almacén de columnas a una tabla OLTP, use una condición de filtrado para crear un índice de almacén de columnas no agrupado únicamente en los datos inactivos de la carga de trabajo operativa.

-   Las tablas en memoria pueden tener un índice de almacén de columnas. Puede crearlo cuando se genere la tabla o agregarlo en otro momento con [ALTER TABLE &#40;Transact-SQL&#41;](../t-sql/statements/alter-table-transact-sql.md). Antes de SQL Server 2016, solo las tablas basadas en disco podían contar con un índice de almacén de columnas.

Para obtener más información, consulte [Rendimiento de las consultas de índices de almacén de columnas](../relational-databases/indexes/columnstore-indexes-query-performance.md).

**Guía de diseño**


-   Una tabla de almacén de filas puede contar con un índice de almacén de columnas no agrupado actualizable. Antes de SQL Server 2014, el índice de almacén de columnas no agrupado era de solo lectura.



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-spexecuteexternalscript-transact-sqlsystem-stored-proceduressp-execute-external-script-transact-sqlmd"></a>8. &nbsp; [sp_execute_external_script (Transact-SQL)](system-stored-procedures/sp-execute-external-script-transact-sql.md)

*Actualizado: 23-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_7) | [Siguiente](#TitleNum_9))

<!-- Source markdown line 207.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0ee4d591ae9d9a5c015eec98aad9ccbb86268761 ac9b439c23ffae5fcc77639de6ff955763cf5844  (PR=4696  ,  Filename=sp-execute-external-script-transact-sql.md  ,  Dirpath=docs\relational-databases\system-stored-procedures\  ,  MergeCommitSha40=d7dcbcebbf416298f838a39dd5de6a46ca9f77aa) -->



Para generar un modelo similar mediante Python, tendría que cambiar el identificador de idioma de `@language=N'R'` a `@language = N'Python'`y realizar las modificaciones necesarias para el argumento `@script`. En caso contrario, todos los parámetros funcionan del mismo modo que para R.

**C. Creación de un modelo de Python y generar puntuaciones a partir de él**


En este ejemplo se muestra cómo usar sp\_execute\_external\_script para generar puntuaciones en un modelo simple de Python.

```
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

**Input query to generate the customer data**

DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders`

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

**Get data from input query**

customer_data = my_input_data

**Define the model**

n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

Los encabezados de columna usados en el código Python no se envían como resultados a SQL Server, así que use la instrucción WITH RESULTS para especificar los nombres de columna y los tipos de datos para SQL.

Para puntuar, también puede usar la función nativa [PREDICT](system-stored-procedures/../../t-sql/queries/predict-transact-sql.md), que es normalmente más rápida porque evita llamar al runtime de Python o R.




&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-create-primary-keystablescreate-primary-keysmd"></a>9. &nbsp; [Crear claves principales](tables/create-primary-keys.md)

*Actualización: 18-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_8))

<!-- Source markdown line 102.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d18b485f314cc005d624cab8a51650d3b8f55f89 9bd2e9453206e8940d30b0a01c43f9d8e1aed606  (PR=4652  ,  Filename=create-primary-keys.md  ,  Dirpath=docs\relational-databases\tables\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



**Crear una clave principal con un índice no agrupado en una tabla nueva**


1.  En el **Explorador de objetos**, conéctese a una instancia del motor de base de datos.

2.  En la barra de Estándar, haga clic en **Nueva consulta**.

3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En el ejemplo se crea una tabla y se define una clave principal en la columna `CustomerID` y un índice agrupado en `TransactionID`.

```
    USE AdventureWorks2012;
    GO
    CREATE TABLE Production.TransactionHistoryArchive1
    (
       CustomerID uniqueidentifier DEFAULT NEWSEQUENTIALID(),
       TransactionID int IDENTITY (1,1) NOT NULL,
       CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY NONCLUSTERED (uniqueidentifier)
    );
    GO

    -- Now add the clustered index
    CREATE CLUSTERED INDEX CIX_TransactionID ON Production.TransactionHistoryArchive1 (TransactionID);
    GO
```







## <a name="similar-articles-about-new-or-updated-articles"></a>Artículos similares sobre artículos nuevos o actualizados

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas temáticas *con* artículos nuevos o actualizados recientemente


- [Nuevos + actualizados (1+3): &nbsp;documentos de **Análisis avanzado para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos + actualizados (0+1): &nbsp;documentos de **Analytics Platform System para SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos + actualizados (0+1): &nbsp;documentos de **Conexión a SQL**](../connect/new-updated-connect.md)
- [Nuevos + actualizados (0+1): &nbsp;documentos del **Motor de base de datos de SQL**](../database-engine/new-updated-database-engine.md)
- [Nuevos + actualizados (12+1): **documentos de** Integration Services para SQL](../integration-services/new-updated-integration-services.md)
- [Nuevos + actualizados (6+2): &nbsp;documentos de **Linux para SQL**](../linux/new-updated-linux.md)
- [Nuevos + actualizados (15+0): **documentos de** PowerShell para SQL](../powershell/new-updated-powershell.md)
- [Nuevos + actualizados (2+9): &nbsp;documentos de **Bases de datos relacionales para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Nuevos + actualizados (1+0): &nbsp;documentos de **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Nuevos + actualizados (1+1): &nbsp;documentos de **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos + actualizados (1+1): &nbsp;documentos de **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Nuevos + actualizados (0+1): &nbsp;documentos de **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Nuevos + actualizados (1+2): &nbsp;documentos de **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Nuevos + actualizados (0+2): &nbsp;documentos de **Transact-SQL**](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Áreas temáticas que *no* tienen artículos nuevos o actualizados recientemente


- [Nuevos + Actualizados (0+0): documentos de **Data Migration Assistant (DMA) para SQL**](../dma/new-updated-dma.md)
- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos + actualizados (0+0): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **Ejemplos para SQL**](../sample/new-updated-sample.md)
- [Nuevos + Actualizados (0+0): documentos de **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Nuevos + actualizados (0+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)


