---
title: Configuración del proyecto (asignación de tipo) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4bb8466e-2199-4f00-8513-b04e9586723d
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 449f1ecc2fbcc2f9e18ea24cb5bd42323bbf5ddc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62625889"
---
# <a name="project-settings-type-mapping-oracletosql"></a>Configuración del proyecto (asignación de tipo) (OracleToSQL)
La página de asignación de tipos de la **configuración del proyecto** cuadro de diálogo contiene la configuración que permiten personalizar cómo SSMA convierte tipos de datos de Oracle en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.  
  
Está disponible en la página de asignación de tipos de la **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo.  
  
-   Para especificar la configuración para todos los proyectos SSMA futuros, en el **herramientas** menú haga clic en **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para el que la configuración es necesaria para ver o cambiar de **Versión de destino de migración** lista desplegable y, a continuación, haga clic en **Type Mapping** en la parte inferior del panel izquierdo.  
  
-   Para especificar la configuración para el proyecto actual, en el **herramientas** menú haga clic en **configuración del proyecto**y, a continuación, haga clic en **Type Mapping** en la parte inferior del panel izquierdo.  
  
Para especificar la configuración para el objeto actual o la clase de objetos, utilice el **Type Mapping** pestaña en la ventana principal de SSMA.  
  
## <a name="options"></a>Opciones  
La tabla siguiente muestra la **Type Mapping** opciones de la pestaña:  
  
**Tipo de origen**  
El tipo de datos de Oracle asignado.  
  
**Tipo de destino**  
El destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos para el tipo de datos de Oracle especificado.  
  
Consulte las tablas en la sección siguiente para el valor predeterminado SSMA para asignaciones de tipos de Oracle.  
  
**Agregar**  
Haga clic para agregar un tipo de datos a la lista de asignación.  
  
**Editar**  
Haga clic para editar el tipo de datos seleccionado en la lista de asignación.  
  
**Quitar**  
Haga clic para quitar la asignación de tipos de datos seleccionados de la lista de asignación.  
  
**Valores predeterminados**  
Haga clic para restablecer la lista de asignación de tipo para los valores predeterminados SSMA.  
  
## <a name="default-type-mappings"></a>Asignaciones de tipos predeterminadas  
De SSMA para Oracle, puede establecer asignaciones de tipos personalizado para los argumentos, columnas, variables locales y los valores devueltos. La asignación predeterminada para los argumentos y tipos de valor devuelto es casi idéntica.  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>Tipo de argumento predeterminado y devolver la asignación de tipos de valor  
En la tabla siguiente contiene la asignación de tipo de datos predeterminada para los argumentos y valores devueltos.  
  
|Tipo de datos de Oracle|Default [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos|  
|--------------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|binary_integer|INT|  
|blob|varbinary(max)|  
|boolean|bit|  
|char|ntext|  
|char varying|ntext|  
|character|ntext|  
|character varying|ntext|  
|clob|ntext|  
|date|datetime2 [0]|  
|dec|dec[38][0]|  
|Decimal|float[53]|  
|doble precisión|float[53]|  
|FLOAT|float[53]|  
|INT|INT|  
|integer|INT|  
|long|ntext|  
|long raw|varbinary(max)|  
|long raw [\*... 8000]<sup>*</sup>|varbinary [*]|  
|long raw [8001..\*]<sup>*</sup>|varbinary(max)|  
|carácter nacional|nvarchar(max)|  
|variable de Car. nacional|nvarchar(max)|  
|carácter nacional|nvarchar(max)|  
|national character varying de<sup>**</sup>|nvarchar(max)|  
|national character varying de<sup>*</sup>|nvarchar(max)|  
|NCHAR|nvarchar(max)|  
|nclob|nvarchar(max)|  
|number|float[53]|  
|NUMERIC|float[53]|  
|nvarchar2|nvarchar(max)|  
|pls_integer|INT|  
|raw|varbinary(max)|  
|REAL|float[53]|  
|ROWID|UNIQUEIDENTIFIER|  
|signtype|SMALLINT|  
|SMALLINT|SMALLINT|  
|string|ntext|  
|TIMESTAMP|datetime2|  
|marca de tiempo con la zona horaria local|datetimeoffset|  
|marca de tiempo con la zona horaria|datetimeoffset|  
|urowid|UNIQUEIDENTIFIER|  
|varchar|ntext|  
|varchar2|ntext|  
|xmltype|xml|  
  
<sup>*</sup> Se aplica para devolver el valor de tipo asignación solo.  
  
<sup>**</sup> Se aplica al argumento de tipo asignación solo.  
  
### <a name="default-column-type-mapping"></a>Asignación de tipos de columna predeterminados  
En la tabla siguiente contiene la asignación de tipo de valor predeterminado para las columnas.  
  
|Tipo de datos de Oracle|Default [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos|  
|--------------------|-------------------------------------------------------------------------|  
|BFILE|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|blob|varbinary(max)|  
|char|char|  
|char varying [*.. \*]|varchar [*]|  
|Char [*.. \*]|Char [*]|  
|character|char|  
|variable de carácter [*.. \*]|varchar [*]|  
|character[*..\*]|Char [*]|  
|clob|ntext|  
|date|datetime2 [0]|  
|dec|dec[38][0]|  
|dec[*..\*]|DEC [*] [0]|  
|dec[*..\*][\*..\*]|DEC [*] [\*]|  
|Decimal|decimal[38][0]|  
|decimal[*..\*]|decimal[*][0]|  
|decimal [*.. \*][\*.. \*]|decimal [*] [\*]|  
|doble precisión|float[53]|  
|FLOAT|float[53]|  
|float [*.. 53]|float [*]|  
|float[54..*]|float[53]|  
|INT|INT|  
|integer|INT|  
|long|ntext|  
|long raw|varbinary(max)|  
|long raw [*.. 8000]|varbinary [*]|  
|long raw [8001.. *]|varbinary(max)|  
|long varchar|ntext|  
|long[*..8000]|varchar [*]|  
|long[8001..*]|ntext|  
|carácter nacional|NCHAR|  
|National char varying [*.. \*]|nvarchar [*]|  
|carácter nacional [*.. \*]|nchar [*]|  
|carácter nacional|NCHAR|  
|national character varying de [*.. \*]|nvarchar [*]|  
|carácter nacional [*.. \*]|nchar [*]|  
|NCHAR|NCHAR|  
|nchar [*]|nchar [*]|  
|nclob|nvarchar(max)|  
|number|float[53]|  
|number[*..\*]|numérico [*]|  
|number[*..\*][\*..\*]|numérico [*] [\*]|  
|NUMERIC|NUMERIC|  
|numeric[*..\*]|numérico [*]|  
|numeric[*..\*][\*..\*]|numérico [*] [\*]|  
|NVARCHAR2 [*.. \*]|nvarchar [*]|  
|sin formato [*.. \*]|varbinary [*]|  
|REAL|float[53]|  
|ROWID|UNIQUEIDENTIFIER|  
|SMALLINT|SMALLINT|  
|TIMESTAMP|datetime2|  
|marca de tiempo con la zona horaria local|datetimeoffset|  
|marca de tiempo con la zona horaria local [*.. \*]|DateTimeOffset [*]|  
|marca de tiempo con la zona horaria|datetimeoffset|  
|marca de tiempo con la zona horaria [*.. \*]|DateTimeOffset [*]|  
|timestamp[*..\*]|datetime2 [*]|  
|urowid|UNIQUEIDENTIFIER|  
|urowid[*..\*]|UNIQUEIDENTIFIER|  
|varchar[*..\*]|varchar [*]|  
|varchar2[*..\*]|varchar [*]|  
|Xmltype|xml|  
  
### <a name="default-local-variable-type-mapping"></a>Asignación de tipo de Variable Local predeterminada  
En la tabla siguiente contiene la asignación de tipo de valor predeterminado para las variables locales.  
  
|Tipo de datos de Oracle|Default [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos|  
|--------------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float[53]|  
|binary_float|float[53]|  
|binary_interger|INT|  
|Blob|varbinary(max)|  
|Boolean|bit|  
|Char|char|  
|char varying [*.. 8000]|varchar [*]|  
|char varying [8001.. *]|ntext|  
|char[*..8000]|Char [*]|  
|char[8001..*]|ntext|  
|Carácter|char|  
|variable de carácter [*.. 8000]|varchar [*]|  
|variable de carácter [8001.. *]|ntext|  
|character[*..8000]|Char [*]|  
|character[8001..*]|ntext|  
|clob|ntext|  
|date|datetime2 [0]|  
|dec|dec[38][0]|  
|dec[*..\*]|DEC [*] [0]|  
|dec[*..\*][\*..\*]|DEC [*] [\*]|  
|Decimal|decimal[38][0]|  
|decimal[*..\*]|decimal[*][0]|  
|decimal [*.. \*][\*.. \*]|decimal [*] [\*]|  
|doble precisión|float[53]|  
|float|float[53]|  
|float [*.. 53]|float [*]|  
|float[54..*]|float[53]|  
|int|INT|  
|Integer|INT|  
|integer[*..\*]|numérico [*] [0]|  
|Long|ntext|  
|long raw|varbinary(max)|  
|long raw [*.. 8000]|varbinary [*]|  
|long raw [8001.. *]|varbinary(max)|  
|carácter nacional|NCHAR|  
|National char varying [*.. 4000]|nvarchar [*]|  
|National char varying [4001.. *]|nvarchar(max)|  
|carácter nacional [*.. 4000]|nchar [*]|  
|carácter nacional [4001.. *]|nvarchar(max)|  
|carácter nacional|NCHAR|  
|carácter nacional [*.. 4000]|nvarchar [*]|  
|carácter nacional [4001.. *]|nvarchar(max)|  
|national character varying de [*.. 4000]|nvarchar [*]|  
|national character varying de [4001.. *]|nvarchar(max)|  
|Nchar|NCHAR|  
|nchar[*..4000]|nchar [*]|  
|nchar[4001..*]|nvarchar(max)|  
|nchar varying [*.. 4000]|nvarchar [*]|  
|nchar varying [4001.. *]|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|Number|float[53]|  
|number[*..\*]|numérico [*]|  
|number[*..\*][\*..\*]|numérico [*] [\*]|  
|Numérico|numeric[38][0]|  
|numeric[*..\*]|numérico [*]|  
|numeric[*..\*][\*..\*]|numérico [*] [\*]|  
|nvarchar2[*..4000]|nvarchar [*]|  
|nvarchar2[4001..*]|nvarchar(max)|  
|pls_integer|INT|  
|raw[*..8000]|varbinary [*]|  
|raw[8001..*]|varbinary(max)|  
|Real|float[53]|  
|Rowid|UNIQUEIDENTIFIER|  
|Signtype|SMALLINT|  
|Smallint|SMALLINT|  
|string[*..8000]|varchar [*]|  
|string[8001..*]|ntext|  
|TIMESTAMP|datetime2|  
|marca de tiempo con la zona horaria local|datetimeoffset|  
|marca de tiempo con la zona horaria|datetimeoffset|  
|marca de tiempo con la zona horaria local [*.. \*]|DateTimeOffset [*]|  
|marca de tiempo con la zona horaria [*.. \*]|DateTimeOffset [*]|  
|timestamp[*..\*]|datetime2 [*]|  
|urowid|UNIQUEIDENTIFIER|  
|urowid[*..\*]|UNIQUEIDENTIFIER|  
|varchar[*..8000]|varchar [*]|  
|varchar[8001..*]|ntext|  
|varchar2[*..8000]|varchar [*]|  
|varchar2[8001..*]|varcha(max)|  
|Xmltype|xml|  
  
## <a name="see-also"></a>Vea también  
[User Interface Reference &#40;OracleToSQL&#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
