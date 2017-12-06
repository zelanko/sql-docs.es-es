---
title: 'Actualizado: conectarse a los documentos de SQL Server | Documentos de Microsoft'
description: "Mostrar fragmentos de contenido actualizado para recientemente modificadas en documentación, para conectar con Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.workload: connect-to-sql
ms.openlocfilehash: cb0ac4b391559cfac072cff61c9f13b14fe7c952
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-connect-to-sql-server"></a>Nuevos y actualizados recientemente: conectarse a SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **2017-09-28** &nbsp; - a - &nbsp; **2017-12-02**
- *Área de asunto:* &nbsp; **conectar con SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Pantalla 1 del Asistente de origen de datos](odbc/windows/dsn-wizard-1.md)
2. [Pantalla 2 del Asistente de origen de datos](odbc/windows/dsn-wizard-2.md)
3. [Pantalla 3 del Asistente de origen de datos](odbc/windows/dsn-wizard-3.md)
4. [Pantalla 4 del Asistente de origen de datos](odbc/windows/dsn-wizard-4.md)
5. [Cuadro de diálogo de inicio de sesión SQL Server (ODBC)](odbc/windows/sql-server-login-dialog.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [PDOStatement::bindParam](#TitleNum_1)
2. [PDOStatement::bindValue](#TitleNum_2)
3. [sqlsrv_prepare](#TitleNum_3)
4. [sqlsrv_query](#TitleNum_4)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-pdostatementbindparamphppdostatement-bindparammd"></a>1. &nbsp;[Pdostatement:: Bindparam](php/pdostatement-bindparam.md)

*Actualizado: 2017-10-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([siguiente](#TitleNum_2))

<!-- Source markdown line 119.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2792d149331f5326f6914721c86687d545685488 e363544e2c6f73277b7f2ca05b9269a4139d1fac  (PR=3663  ,  Filename=pdostatement-bindparam.md  ,  Dirpath=docs\connect\php\  ,  MergeCommitSha40=e9caa51a68c2f03fb9f3a0354b5eab1eed43bdf1) -->



> [!NOTE]
> Se recomienda usar cadenas como entradas al enlazar los valores para un [columna decimal o numeric](https://docs.microsoft.com/en-us/sql/t-sql/data-types/decimal-and-numeric-transact-sql) para garantizar la precisión y la exactitud PHP limitó precisión para [números de punto flotante](http://php.net/manual/en/language.types.float.php).

**Ejemplo**

Este ejemplo de código muestra cómo enlazar un valor decimal como un parámetro de entrada.

```php
<?php
$database = "Test";
$server = "(local)";
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");

// Assume TestTable exists with a decimal field
$input = 9223372036854.80000;
$stmt = $conn->prepare("INSERT INTO TestTable (DecimalCol) VALUES (?)");
// by default it is PDO::PARAM_STR, rounding of a large input value may
// occur if PDO::PARAM_INT is specified
$stmt->bindParam(1, $input, PDO::PARAM_STR);
$stmt->execute();
```




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-pdostatementbindvaluephppdostatement-bindvaluemd"></a>2. &nbsp;[PDOStatement::bindValue](php/pdostatement-bindvalue.md)

*Actualizado: 2017-10-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [siguiente](#TitleNum_3))

<!-- Source markdown line 77.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c1d5ff4d5bfdbfbf1635cf14d71b4d583164075a 6cd5fc88860ae9ffca25ee15e8eeaeba29991fda  (PR=3663  ,  Filename=pdostatement-bindvalue.md  ,  Dirpath=docs\connect\php\  ,  MergeCommitSha40=e9caa51a68c2f03fb9f3a0354b5eab1eed43bdf1) -->



> [!NOTE]
> Se recomienda usar cadenas como entradas al enlazar los valores para un [columna decimal o numeric](https://docs.microsoft.com/en-us/sql/t-sql/data-types/decimal-and-numeric-transact-sql) para garantizar la precisión y la exactitud PHP limitó precisión para [números de punto flotante](http://php.net/manual/en/language.types.float.php).

**Ejemplo**

Este ejemplo de código muestra cómo enlazar un valor decimal como un parámetro de entrada.

```php
<?php
$database = "Test";
$server = "(local)";
$conn = new PDO("sqlsrv:server=$server ; Database = $database", "", "");

// Assume TestTable exists with a decimal field
$input = 9223372036854.80000;
$stmt = $conn->prepare("INSERT INTO TestTable (DecimalCol) VALUES (?)");
// by default it is PDO::PARAM_STR, rounding of a large input value may
// occur if PDO::PARAM_INT is specified
$stmt->bindValue(1, $input, PDO::PARAM_STR);
$stmt->execute();
```



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-sqlsrvpreparephpsqlsrv-preparemd"></a>3. &nbsp; [sqlsrv_prepare](php/sqlsrv-prepare.md)

*Actualizado: 2017-10-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2) | [siguiente](#TitleNum_4))

<!-- Source markdown line 219.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7811e459efec90ef79340375d5fb34364130466b 3d28b3d320dc7fe5df12300da5cb9579abf6839a  (PR=3663  ,  Filename=sqlsrv-prepare.md  ,  Dirpath=docs\connect\php\  ,  MergeCommitSha40=e9caa51a68c2f03fb9f3a0354b5eab1eed43bdf1) -->



> [!NOTE]
> Se recomienda usar cadenas como entradas al enlazar los valores para un [columna decimal o numeric](https://docs.microsoft.com/en-us/sql/t-sql/data-types/decimal-and-numeric-transact-sql) para garantizar la precisión y la exactitud PHP limitó precisión para [números de punto flotante](http://php.net/manual/en/language.types.float.php).

**Ejemplo**

Este ejemplo de código muestra cómo enlazar un valor decimal como un parámetro de entrada.

```php
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"YourTestDB");
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
    echo "Could not connect.\n";
    die(print_r(sqlsrv_errors(), true));
}

// Assume TestTable exists with a decimal field
$input = "9223372036854.80000";
$params = array($input);
$stmt = sqlsrv_prepare($conn, "INSERT INTO TestTable (DecimalCol) VALUES (?)", $params);
sqlsrv_execute($stmt);

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

?>
```



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-sqlsrvqueryphpsqlsrv-querymd"></a>4. &nbsp; [sqlsrv_query](php/sqlsrv-query.md)

*Actualizado: 2017-10-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_3))

<!-- Source markdown line 163.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 07a84878c07af0b6ad7e247337be5b4567ce03c3 127af26a8a054a45dda51d90f43f08652949ba18  (PR=3663  ,  Filename=sqlsrv-query.md  ,  Dirpath=docs\connect\php\  ,  MergeCommitSha40=e9caa51a68c2f03fb9f3a0354b5eab1eed43bdf1) -->



> [!NOTE]
> Se recomienda usar cadenas como entradas al enlazar los valores para un [columna decimal o numeric](https://docs.microsoft.com/en-us/sql/t-sql/data-types/decimal-and-numeric-transact-sql) para garantizar la precisión y la exactitud PHP limitó precisión para [números de punto flotante](http://php.net/manual/en/language.types.float.php).

**Ejemplo**

Este ejemplo de código muestra cómo enlazar un valor decimal como un parámetro de entrada.

```php
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"YourTestDB");
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
     echo "Could not connect.\n";
     die(print_r(sqlsrv_errors(), true));
}

// Assume TestTable exists with a decimal field
$input = "9223372036854.80000";
$params = array($input);
$stmt = sqlsrv_query($conn, "INSERT INTO TestTable (DecimalCol) VALUES (?)", $params);

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

?>
```








## <a name="similar-articles"></a>Artículos similares

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas temáticas con artículos nuevos o actualizados recientemente

- [Nuevos y actualizados (3 + 14): **Advanced Analytics para SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos + Actualizados (1+0): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos y actualizados (87 + 0): **Analytics Platform System para SQL** documentos](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos y actualizados (4 de 5 +): **conectar con SQL Server** documentos](../connect/new-updated-connect.md)
- [Nuevos y actualizados (0 + 1): **motor de base de datos de SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Nuevos y actualizados (2 + 2): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Nuevos y actualizados (10 + 9): **Linux para SQL** documentos](../linux/new-updated-linux.md)
- [Nuevos y actualizados (2 + 4): **bases de datos relacionales de SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Nuevos y actualizados (4 + 2): **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Nuevos y actualizados (0 + 1): **ejemplos para SQL** documentos](../sample/new-updated-sample.md)
- [Nuevos y actualizados (21 + 0): **Studio de operaciones SQL** documentos](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos y actualizados (5 + 1): **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Nuevos + Actualizados (0+1): documentos de **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Nuevos y actualizados (1 + 0): **SQL Server Migration Assistant (SSMA)** documentos](../ssma/new-updated-ssma.md)
- [Nuevos + Actualizados (0+1): documentos de **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Nuevos y actualizados (0 + 2): **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas temáticas sin artículos nuevos ni actualizados recientemente

- [Nuevos y actualizados (0 + 0): **datos migración Ayudante (DMA) para SQL** documentos](../dma/new-updated-dma.md)
- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Nuevos + actualizados (0+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)


