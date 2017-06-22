---
title: 'Actualizado: los documentos de bases de datos relacionales | Documentos de Microsoft'
description: "Mostrar fragmentos de contenido actualizado para recientemente modificadas en documentación, bases de datos relacionales."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 05/23/2017
ms.author: genemi
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: 3ab051a6fd00670139bb1089dcd3f4af76b9ecef
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Las nuevas y recientemente actualizado: los documentos de bases de datos relacionales



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su [Docs.Microsoft.com](http://docs.microsoft.com/) sitio Web de documentación. Este artículo muestra extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

En este artículo es generado por un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto, o como marcado del artículo de origen. Nunca las imágenes se muestran aquí.

Actualizaciones recientes se notifican para el siguiente intervalo de fechas y el asunto:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **2017-05-01** &nbsp; - a - &nbsp; **2017-05-23**
- *Área de asunto:* &nbsp; **bases de datos relacionales**.




&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

Esta sección muestra los extractos de las actualizaciones que se recopilan de los artículos que han presentado recientemente una actualización a gran escala.

Los extractos que se muestran aquí aparecen separados de su contexto semántica correcta. Además, en ocasiones, un extracto se separa de la sintaxis de markdown importante que rodea en el artículo real. Por lo tanto, estos extractos son para obtener instrucciones generales solo. Los extractos de sólo le permiten saber si sus intereses garantizan dedicar tiempo a haga clic en y visite el artículo real.

Por estas y otras razones, no se copie el código de estos fragmentos y no toma como verdaderos exacta cualquier fragmento de texto. En su lugar, visite el artículo real.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-create-a-graph-database-and-run-some-pattern-matching-queries-using-t-sqlgraphssql-graph-samplemd"></a>1. &nbsp;[Crear una base de datos del gráfico y ejecutar algunas consultas mediante T-SQL de coincidencia de patrones](graphs/sql-graph-sample.md)

*Updated: 2017-05-04* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 68.  ms.author= "shkale".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ff467bf5fcf13592c796836def36e16e34f8cc31 99fcf0399006de16d0ac7cc9057564d307cb981b -->


```
INSERT INTO Person VALUES (1,'John');
INSERT INTO Person VALUES (2,'Mary');
INSERT INTO Person VALUES (3,'Alice');
INSERT INTO Person VALUES (4,'Jacob');
INSERT INTO Person VALUES (5,'Julie');

INSERT INTO Restaurant VALUES (1,'Taco Dell','Bellevue');
INSERT INTO Restaurant VALUES (2,'Ginger and Spice','Seattle');
INSERT INTO Restaurant VALUES (3,'Noodle Land', 'Redmond');

INSERT INTO City VALUES (1,'Bellevue','wa');
INSERT INTO City VALUES (2,'Seattle','wa');
INSERT INTO City VALUES (3,'Redmond','wa');

-- Insert into edge table. While inserting into an edge table, 
-- you need to provide the $node_id from $from_id and $to_id columns.
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 1), 
       (SELECT $node_id FROM Restaurant WHERE id = 1),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 2), 
      (SELECT $node_id FROM Restaurant WHERE id = 2),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 3), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 4), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 5), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);

INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 1),
      (SELECT $node_id FROM City WHERE id = 1));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 2),
      (SELECT $node_id FROM City WHERE id = 2));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 3),
      (SELECT $node_id FROM City WHERE id = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 4),
      (SELECT $node_id FROM City WHERE id = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 5),
      (SELECT $node_id FROM City WHERE id = 1));

INSERT INTO locatedIn VALUES ((SELECT $node_id FROM Restaurant WHERE id = 1),
      (SELECT $node_id FROM City WHERE id =1));
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sysfngetauditfile-transact-sqlsystem-functionssys-fn-get-audit-file-transact-sqlmd"></a>2. &nbsp; [sys.fn_get_audit_file (Transact-SQL)](system-functions/sys-fn-get-audit-file-transact-sql.md)

*Updated: 2017-05-16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1) | [Next](#TitleNum_3))

<!-- Source markdown line 145.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 046fa92ad1b7e6bb7a956493ca06cf72d45b5285 fbf55361da90663835d7e107fda697c358e0e061 -->



- **Azure SQL Database**

  En este ejemplo se lee un archivo denominado `ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel`.  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default);
  GO  
  ```  

  Este ejemplo se leen todos los registros de los servidores que comienzan por de auditoría `Sh`.  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```





&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-manage-retention-of-historical-data-in-system-versioned-temporal-tablestablesmanage-retention-of-historical-data-in-system-versioned-temporal-tablesmd"></a>3. &nbsp;[Administrar la retención de datos históricos en las tablas temporales con versión del sistema](tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)

*Updated: 2017-05-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_2))

<!-- Source markdown line 425.  ms.author= "carlrab".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ee69beb6a46913934d4a322f5d95343cc86f2ec4 94da98fec4ab16636a4581c16eb4456e2d1ff66b -->



**Usando el enfoque de directiva de retención de historial Temporal**

> **Nota:** mediante la directiva de retención de historial Temporal método se aplica a [! INCLUDE [sqldbesa--.. /.. /includes/sqldbesa-MD.MD]) y SQL Server 2017 desde CTP 1.3.  

Tiempo de retención de historial temporal puede ser configurado en el nivel de tabla individual, lo que permite a los usuarios crear antigüedad flexible directivas. Aplicar la retención temporal es simple: requiere un solo parámetro establecerse durante el cambio de esquema o de creación de tabla.

Después de definir la directiva de retención, la base de datos de SQL Azure inicia comprobar periódicamente si hay filas históricos que son aptas para la limpieza automática de los datos. Identificación de las filas coincidentes y su eliminación de la tabla de historial se producen de forma transparente, en la tarea en segundo plano programada y ejecutada por el sistema. Se comprueba la condición de edad para las filas de la tabla de historial en función de la columna que representa el final del período de SYSTEM_TIME. Si el período de retención, por ejemplo, se establece en seis meses, filas aptas para la limpieza de la tabla cumplen la condición siguiente:
```
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
```
En el ejemplo anterior, se supone que ValidTo columna corresponde al final del período de SYSTEM_TIME.
**¿Cómo configurar la directiva de retención?**

Antes de configurar la directiva de retención para una tabla temporal, compruebe primero si la retención de historial temporal está habilitada en el nivel de base de datos:
```
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
```
Marca la base de datos **is_temporal_history_retention_enabled** se establece en ON de forma predeterminada, pero los usuarios pueden cambiar con la instrucción ALTER DATABASE. Automáticamente se establece en OFF después de punto en la operación de restauración de tiempo. Para habilitar la limpieza de la retención de historial temporal para la base de datos, ejecute la instrucción siguiente:
```
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
```
Directiva de retención se configura durante la creación de una tabla especificando el valor para el parámetro HISTORY_RETENTION_PERIOD:
```
CREATE TABLE dbo.WebsiteUserInfo
```





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Compact lista de artículos que se actualizó recientemente

Esta lista compact proporciona vínculos a todos los artículos actualizados que se enumeran en la sección anterior.

1. [Crear una base de datos del gráfico y ejecutar algunas consultas mediante T-SQL de coincidencia de patrones](#TitleNum_1)
2. [Sys.fn_get_audit_file (Transact-SQL)](#TitleNum_2)
3. [Administración de la retención de datos históricos en las tablas temporales con control de versiones del sistema](#TitleNum_3)


<a name="sisters2"/>

&nbsp;

## <a name="sister-articles"></a>Hermana artículos

Esta sección enumeran artículos muy similar para los artículos actualizados recientemente en otras áreas temáticas, dentro del mismo repositorio de GitHub.


&nbsp;

[Microsoft /**pr de documentos de sql** ](https://github.com/microsoftdocs/sql-docs-pr/) repositorio en GitHub.com:

- [Actualizado recientemente: **Microsoft SQL Server y bases de datos relacionales** documentos](/sql/relational-databases/relational-databases-new-updated-sql-docs-pr)
- [Actualizado recientemente: **Microsoft SQL Server** documentos](/sql/sql-server/sql-server-new-updated-sql-docs-pr)
- [Actualizado recientemente: **Transact-SQL en SQL Server** documentos](/sql/t-sql/t-sql-new-updated-sql-docs-pr)


&nbsp;

<!--
[Microsoft/**azure-docs**](https://github.com/microsoft/azure-docs/) repository on GitHub.com:

- [Sisters list for **azure-docs** repo](https://docs.microsoft.com/azure/sql-server-new-updated-azure-docs/#sisters2)
-->

&nbsp;



