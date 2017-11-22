---
title: "(Asignación de tipos) de la configuración del proyecto (DB2ToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: cf426c69-6a8e-4d19-951d-6661d5ae2562
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 267d3e30f61539da24ed22d54c4355945da21999
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="project-settings-type-mapping-db2tosql"></a>(Asignación de tipos) de la configuración del proyecto (DB2ToSQL)
La página de asignación de tipo de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA convierte los tipos de datos de DB2 en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos.  
  
La página de asignación de tipo está disponible en la **configuración del proyecto** y **la configuración predeterminada del proyecto** cuadros de diálogo.  
  
-   Para especificar la configuración para todos los proyectos futuros de SSMA, en la **herramientas** menú haga clic en **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para el que se requiere para puede ver o cambiar de configuración **versión de destino de migración** de lista desplegable y, a continuación, haga clic en **Type Mapping** en la parte inferior del panel izquierdo.  
  
-   Para especificar la configuración para el proyecto actual, en la **herramientas** menú haga clic en **configuración del proyecto**y, a continuación, haga clic en **Type Mapping** en la parte inferior del panel izquierdo.  
  
Para especificar opciones para el objeto actual o la clase de objetos, use la **Type Mapping** pestaña en la ventana principal de SSMA.  
  
## <a name="options"></a>Opciones  
La tabla siguiente muestra la **Type Mapping** ficha Opciones:  
  
**Tipo de origen**  
El tipo de datos de DB2 asignado.  
  
**Tipo de destino**  
El destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de datos para el tipo de datos de DB2 especificado.  
  
Consulte las tablas en la sección siguiente para el valor predeterminado SSMA para asignaciones de tipos de DB2.  
  
**Agregar**  
Haga clic para agregar un tipo de datos a la lista de asignación.  
  
**Editar**  
Haga clic para editar el tipo de datos seleccionado en la lista de asignación.  
  
**Quitar**  
Haga clic para quitar la asignación de tipos de datos seleccionados de la lista de asignación.  
  
**Restablecer valores predeterminados**  
Haga clic para restablecer la lista de asignación de tipo para los valores predeterminados SSMA.  
  
## <a name="default-type-mappings"></a>Asignaciones de tipos predeterminadas  
En SSMA para DB2, puede establecer las asignaciones de tipos personalizados para los argumentos, las columnas, variables locales y valores devueltos. La asignación predeterminada para los argumentos y tipos de valor devuelto es casi idéntica.  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>Tipo de argumento predeterminado y devolver la asignación de tipos de valor  
En la tabla siguiente contiene la asignación de tipo de datos predeterminada para los argumentos y valores devueltos.  
  
|DB2 Tipo de datos|Predeterminado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de datos|  
|-----------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_integer|int|  
|blob|varbinary(max)|  
|boolean|bit|  
|char|varchar(max)|  
|char varying|varchar(max)|  
|character|varchar(max)|  
|character varying|varchar(max)|  
|CLOB|varchar(max)|  
|date|datetime2 [0]|  
|dec|DEC [38] [0]|  
|decimal|float [53]|  
|precisión doble|float [53]|  
|float|float [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|long raw|varbinary(max)|  
|long raw [\*... 8000]<sup>*</sup>|varbinary [*]|  
|long raw [8001..\*]<sup>*</sup>|varbinary(max)|  
|Car.|nvarchar(max)|  
|variación car.|nvarchar(max)|  
|caracteres no nacionales|nvarchar(max)|  
|national character varying de<sup>**</sup>|nvarchar(max)|  
|national character varying de<sup>*</sup>|nvarchar(max)|  
|nchar|nvarchar(max)|  
|NCLOB|nvarchar(max)|  
|number|float [53]|  
|numeric|float [53]|  
|NVARCHAR2|nvarchar(max)|  
|pls_integer|int|  
|raw|varbinary(max)|  
|real|float [53]|  
|ROWID|uniqueidentifier|  
|Signtype|smallint|  
|smallint|smallint|  
|string|varchar(max)|  
|timestamp|datetime2|  
|marca de tiempo con la zona horaria local|datetimeoffset|  
|marca de tiempo con la zona horaria|datetimeoffset|  
|Urowid|uniqueidentifier|  
|varchar|varchar(max)|  
|VARCHAR2|varchar(max)|  
|Tipo XML|xml|  
  
<sup>*</sup>Se aplica para devolver el valor de tipo asignación solo.  
  
<sup>**</sup>Se aplica al argumento de tipo asignación solo.  
  
### <a name="default-column-type-mapping"></a>Asignación de tipos de columna predeterminados  
En la tabla siguiente contiene la asignación de tipo de valor predeterminado para las columnas.  
  
|DB2 Tipo de datos|Predeterminado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de datos|  
|-----------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|blob|varbinary(max)|  
|char|char|  
|char varying [*.. \*]|varchar [*]|  
|Char [*.. \*]|Char [*]|  
|character|char|  
|carácter variable [*.. \*]|varchar [*]|  
|caracteres [*.. \*]|Char [*]|  
|CLOB|varchar(max)|  
|date|datetime2 [0]|  
|dec|DEC [38] [0]|  
|DEC [*.. \*]|DEC [*] [0]|  
|DEC [*.. \*][\*.. \*]|dec[*][\*]|  
|decimal|decimal [38] [0]|  
|decimal [*.. \*]|decimal [*] [0]|  
|decimal [*.. \*][\*.. \*]|decimal [*] [\*]|  
|precisión doble|float [53]|  
|float|float [53]|  
|float [*.. 53]|float [*]|  
|float [54.. *]|float [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|long raw|varbinary(max)|  
|long raw [*.. 8000]|varbinary [*]|  
|long raw [8001.. *]|varbinary(max)|  
|Long varchar|varchar(max)|  
|tiempo [*.. 8000]|varchar [*]|  
|tiempo [8001.. *]|varchar(max)|  
|Car.|nchar|  
|variación car [*.. \*]|nvarchar [*]|  
|National char [*.. \*]|nchar [*]|  
|caracteres no nacionales|nchar|  
|national character varying de [*.. \*]|nvarchar [*]|  
|caracteres no nacionales [*.. \*]|nchar [*]|  
|nchar|nchar|  
|nchar [*]|nchar [*]|  
|NCLOB|nvarchar(max)|  
|number|float [53]|  
|número [*.. \*]|numérico [*]|  
|número [*.. \*][\*.. \*]|numérico [*] [\*]|  
|numeric|numeric|  
|numérico [*.. \*]|numérico [*]|  
|numérico [*.. \*][\*.. \*]|numérico [*] [\*]|  
|NVARCHAR2 [*.. \*]|nvarchar [*]|  
|sin formato [*.. \*]|varbinary [*]|  
|real|float [53]|  
|ROWID|uniqueidentifier|  
|smallint|smallint|  
|timestamp|datetime2|  
|marca de tiempo con la zona horaria local|datetimeoffset|  
|marca de tiempo con la zona horaria local [*.. \*]|DateTimeOffset [*]|  
|marca de tiempo con la zona horaria|datetimeoffset|  
|marca de tiempo con la zona horaria [*.. \*]|DateTimeOffset [*]|  
|marca de tiempo [*.. \*]|datetime2 [*]|  
|Urowid|uniqueidentifier|  
|urowid [*.. \*]|uniqueidentifier|  
|varchar [*.. \*]|varchar [*]|  
|VARCHAR2 [*.. \*]|varchar [*]|  
|Tipo XML|xml|  
  
### <a name="default-local-variable-type-mapping"></a>Asignación de tipo de Variable Local de forma predeterminada  
En la tabla siguiente contiene la asignación de tipo de valor predeterminado para las variables locales.  
  
|DB2 Tipo de datos|Predeterminado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipo de datos|  
|-----------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_interger|int|  
|BLOB|varbinary(max)|  
|Boolean|bit|  
|Char|char|  
|char varying [*.. 8000]|varchar [*]|  
|char varying [8001.. *]|varchar(max)|  
|Char [*.. 8000]|Char [*]|  
|Char [8001.. *]|varchar(max)|  
|Carácter|char|  
|carácter variable [*.. 8000]|varchar [*]|  
|carácter variable [8001.. *]|varchar(max)|  
|caracteres [*.. 8000]|Char [*]|  
|caracteres [8001.. *]|varchar(max)|  
|CLOB|varchar(max)|  
|date|datetime2 [0]|  
|dec|DEC [38] [0]|  
|DEC [*.. \*]|DEC [*] [0]|  
|DEC [*.. \*][\*.. \*]|dec[*][\*]|  
|decimal|decimal [38] [0]|  
|decimal [*.. \*]|decimal [*] [0]|  
|decimal [*.. \*][\*.. \*]|decimal [*] [\*]|  
|precisión doble|float [53]|  
|Float|float [53]|  
|float [*.. 53]|float [*]|  
|float [54.. *]|float [53]|  
|int|int|  
|Integer|int|  
|entero [*.. \*]|numérico [*] [0]|  
|Long|varchar(max)|  
|long raw|varbinary(max)|  
|long raw [*.. 8000]|varbinary [*]|  
|long raw [8001.. *]|varbinary(max)|  
|Car.|nchar|  
|variación car [*.. 4000]|nvarchar [*]|  
|variación car [4001.. *]|nvarchar(max)|  
|National char [*.. 4000]|nchar [*]|  
|National char [4001.. *]|nvarchar(max)|  
|caracteres no nacionales|nchar|  
|caracteres no nacionales [*.. 4000]|nvarchar [*]|  
|caracteres no nacionales [4001.. *]|nvarchar(max)|  
|national character varying de [*.. 4000]|nvarchar [*]|  
|national character varying de [4001.. *]|nvarchar(max)|  
|Nchar|nchar|  
|nchar [*.. 4000]|nchar [*]|  
|nchar [4001.. *]|nvarchar(max)|  
|nchar varying [*.. 4000]|nvarchar [*]|  
|nchar varying [4001.. *]|nvarchar(max)|  
|NCLOB|nvarchar(max)|  
|Number|float [53]|  
|número [*.. \*]|numérico [*]|  
|número [*.. \*][\*.. \*]|numérico [*] [\*]|  
|Numérico|numérico [38] [0]|  
|numérico [*.. \*]|numérico [*]|  
|numérico [*.. \*][\*.. \*]|numérico [*] [\*]|  
|NVARCHAR2 [*.. 4000]|nvarchar [*]|  
|NVARCHAR2 [4001.. *]|nvarchar(max)|  
|pls_integer|int|  
|sin formato [*.. 8000]|varbinary [*]|  
|sin formato [8001.. *]|varbinary(max)|  
|Real|float [53]|  
|ROWID|uniqueidentifier|  
|Signtype|smallint|  
|Smallint|smallint|  
|cadena [*.. 8000]|varchar [*]|  
|cadena [8001.. *]|varchar(max)|  
|timestamp|datetime2|  
|marca de tiempo con la zona horaria local|datetimeoffset|  
|marca de tiempo con la zona horaria|datetimeoffset|  
|marca de tiempo con la zona horaria local [*.. \*]|DateTimeOffset [*]|  
|marca de tiempo con la zona horaria [*.. \*]|DateTimeOffset [*]|  
|marca de tiempo [*.. \*]|datetime2 [*]|  
|Urowid|uniqueidentifier|  
|urowid [*.. \*]|uniqueidentifier|  
|varchar [*.. 8000]|varchar [*]|  
|varchar [8001.. *]|varchar(max)|  
|VARCHAR2 [*.. 8000]|varchar [*]|  
|VARCHAR2 [8001.. *]|varcha(max)|  
|Tipo XML|xml|  
  
## <a name="see-also"></a>Vea también  
[Referencia de la interfaz de usuario &#40; DB2ToSQL &#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
