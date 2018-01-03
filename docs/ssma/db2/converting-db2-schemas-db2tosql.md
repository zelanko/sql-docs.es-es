---
title: Convertir esquemas de DB2 (DB2ToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 7947efc3-ca86-4ec5-87ce-7603059c75a0
caps.latest.revision: "9"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e3684380a10f371952b2461907bb36a7b13f1107
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="converting-db2-schemas-db2tosql"></a>Convertir esquemas de DB2 (DB2ToSQL)
Después de haberse conectado a DB2, conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], y el proyecto de conjunto y las opciones de asignación de datos, puede convertir los objetos de base de datos de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos de base de datos.  
  
## <a name="the-conversion-process"></a>El proceso de conversión  
Convertir objetos de base de datos toma las definiciones de objeto de DB2, se convierte en similar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos y, a continuación, se carga esta información en los metadatos SSMA. No se carga la información en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. A continuación, puede ver los objetos y sus propiedades mediante el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Explorador de metadatos.  
  
Durante la conversión, SSMA imprime mensajes de salida en el panel de resultados y mensajes de error en el panel de lista de errores. Use la información de salida y el error para determinar si tiene que modificar las bases de datos DB2 o el proceso de conversión para obtener los resultados de la conversión deseada.  
  
## <a name="setting-conversion-options"></a>Establecer las opciones de conversión  
Antes de convertir objetos, revise las opciones de conversión de proyecto en el **configuración del proyecto** cuadro de diálogo. Mediante este cuadro de diálogo, puede establecer cómo SSMA convierte las funciones y variables globales. Para obtener más información, vea [configuración del proyecto &#40; Conversión &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md).  
  
## <a name="conversion-results"></a>Resultados de la conversión  
La siguiente tabla muestra qué objetos de DB2 se convierten y resultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos:  
  
|Objetos de DB2|Objetos SQL Server resultantes|  
|-----------|----------------------------|  
|Tipos de datos|**SSMA asigna todos los tipos excepto los criterios enumerados a continuación:**<br /><br />CLOB: Algunas funciones nativas para trabajar con este tipo no son compatibles (por ejemplo, CLOB_EMPTY())<br /><br />BLOB: Algunas funciones nativas para trabajar con este tipo no son compatibles (por ejemplo, BLOB_EMPTY())<br /><br />DBLOB: Algunas funciones nativas para trabajar con este tipo no son compatibles (por ejemplo, DBLOB_EMPTY())|  
|Tipos definidos por el usuario|**SSMA asigna los siguientes definidos por el usuario:**<br /><br />Tipo distinto<br /><br />Tipo estructurado<br /><br />Tipos de datos de SQL PL: Nota: no se admiten el tipo de cursor débil.|  
|Registros especiales|**SSMA solo asigna registros que se muestran a continuación:**<br /><br />MARCA DE TIEMPO ACTUAL<br /><br />FECHA ACTUAL<br /><br />HORA ACTUAL<br /><br />ZONA HORARIA ACTUAL<br /><br />USUARIO ACTUAL<br /><br />SESSION_USER y usuario<br /><br />SYSTEM_USER<br /><br />CLIENT_APPLNAME ACTUAL<br /><br />CLIENT_WRKSTNNAME ACTUAL<br /><br />TIEMPO DE ESPERA DE BLOQUEO ACTUAL<br /><br />ESQUEMA ACTUAL<br /><br />SERVIDOR ACTUAL<br /><br />AISLAMIENTO ACTUAL<br /><br />Otros registros especiales no se asignan a semántica de SQL server.|  
|CREATE TABLE|**SSMA asigna CREATE TABLE con las siguientes excepciones:**<br /><br />Tablas de agrupación en clústeres (MDC) multidimensionales<br /><br />Tablas de intervalo de clúster (RCT)<br /><br />Tablas con particiones<br /><br />Tabla desasociada<br /><br />Cláusula de captura de datos<br /><br />Opción IMPLICITLY OCULTAS<br /><br />Opción volátil|  
|CREATE VIEW|SSMA asigna CREATE VIEW con 'WITH LOCAL CHECK OPTION', pero otras opciones no están asignadas a la semántica SQL server|  
|CREATE INDEX|**SSMA asigna CREATE INDEX con las siguientes excepciones:**<br /><br />Índice XML<br /><br />Opción BUSINESS_TIME sin se SUPERPONE<br /><br />Cláusula con particiones<br /><br />Opción especificación sólo<br /><br />Opción de uso de extender<br /><br />Opción MINPCTUSED<br /><br />Opción de división de página|  
|Desencadenadores|**SSMA asigna la semántica de desencadenador siguiente:**<br /><br />Después de / para los desencadenadores de cada fila<br /><br />Después de /FOR se desencadena cada instrucción<br /><br />ANTES de / para cada fila y, en lugar de / para cada fila desencadenadores|  
|Secuencias|Se asignan.|  
|Instrucción SELECT|**Mapas SSMA seleccione con las siguientes excepciones:**<br /><br />Cláusula de datos-cambio-referencia de tabla: hayan asignado parcialmente, pero las tablas FINAL no se admite<br /><br />Cláusula de referencia de tabla: hayan asignado parcialmente, pero solo--referencia de tabla, referencia de tabla externa, analyze_table-expression, tabla derivada de recopilación, xmltable-expression no se asignan a la semántica SQL server<br /><br />Cláusula de especificación de período: no asignado.<br /><br />Cláusula de controlador continuar: no se ha asignado.<br /><br />Cláusula de correlación con tipo: no asignado.<br /><br />Cláusula de resolución de acceso simultáneo – no asignado.|  
|Instrucción de valores|Se ha asignado.|  
|INSERT, instrucción|Se ha asignado.|  
|Instrucción UPDATE|S**SMA asigna actualización con las siguientes excepciones:**<br /><br />Cláusula, referencia de tabla: solo-tabla-referencia no está asignado a la semántica SQL server<br /><br />Cláusula período: no está asignada.|  
|Instrucción MERGE|**SSMA asigna mezcla con las siguientes excepciones:**<br /><br />Único frente a varias apariciones de cada cláusula: se asigna a la semántica SQL server limitados apariciones de cada cláusula<br /><br />Cláusula de señal: no se asigna a la semántica de SQL Server<br /><br />Mixto UPDATE y DELETE cláusulas: no se asigna a la semántica de SQL Server<br /><br />Cláusula de período: no se asigna a la semántica de SQL Server|  
|La instrucción DELETE|**ELIMINAR asignaciones SSMA con las siguientes excepciones:**<br /><br />Cláusula, referencia de tabla: solo-tabla-referencia no está asignado a la semántica SQL server<br /><br />Cláusula período: no se asigna a la semántica de SQL Server|  
|Nivel de aislamiento y el tipo de bloqueo|Se ha asignado.|  
|Procedimientos (SQL)|Se asignan.|  
|Procedimientos (externo)|Requieren una actualización manual.|  
|Procedimientos (originados)|No se asignan a la semántica de SQL Server.|  
|Instrucción de asignación|Se ha asignado.|  
|Instrucción de llamada para un procedimiento|Se ha asignado.|  
|Instrucción CASE|Se ha asignado.|  
|PARA la instrucción|Se ha asignado.|  
|GOTO, instrucción|Se ha asignado.|  
|Instrucción IF|Se ha asignado.|  
|Recorrer en ITERACIÓN instrucción|Se ha asignado.|  
|Deje la instrucción|Se ha asignado.|  
|Instrucción del bucle|Se ha asignado.|  
|Repita la instrucción|Se ha asignado.|  
|RESIGNAL instrucción|No se admiten condiciones. Los mensajes pueden ser opcionales.|  
|RETURN (instrucción)|Se ha asignado.|  
|Instrucción de señal|No se admiten condiciones. Los mensajes pueden ser opcionales.|  
|WHILE (instrucción)|Se ha asignado.|  
|GET (instrucción) diagnósticos|**SSMA asigna obtener diagnósticos con las siguientes excepciones:**<br /><br />ROW_COUNT: se ha asignado.<br /><br />DB2_RETURN_STATUS: se ha asignado.<br /><br />MESSAGE_TEXT: se ha asignado.<br /><br />DB2_SQL_NESTING_LEVEL - no se asigna a la semántica de SQL Server<br /><br />DB2_TOKEN_STRING - no se asigna a la semántica de SQL Server|  
|Cursores|**SSMA asigna los CURSORES con las siguientes excepciones:**<br /><br />Instrucción de CURSOR ALLOCATE - no se asigna a la semántica de SQL Server<br /><br />Declaración de asociar LOCALIZADORES: no se asigna a la semántica de SQL Server<br /><br />Instrucción DECLARE CURSOR - cláusula Returnability no está asignado a la semántica SQL server<br /><br />La instrucción FETCH – una asignación parcial. Solo se admiten variables como destino. DESCRIPTOR de SQLDA no está asignado a la semántica SQL server|  
|Variables|Se asignan.|  
|Excepciones, controladores y condiciones|**SSMA asigna "control de excepciones" con las siguientes excepciones:**<br /><br />SALIR de controladores: se asignan.<br /><br />Deshacer controladores: se asignan.<br /><br />CONTINUAR controladores: no se asignan.<br /><br />Condiciones - no se asigna a la semántica SQL server.|  
|SQL dinámico|No se ha asignado.|  
|Alias|Se asignan.|  
|Alias|Asignación parcial. Procesamiento manual es necesario para el objeto subyacente|  
|Sinónimos|Se asignan.|  
|Funciones estándares de DB2|SSMA asigna las funciones estándar de DB2 cuando una función equivalente está disponible en SQL Server:|  
|Autorización|No se ha asignado.|  
|Predicados|Se asignan.|  
|SELECT INTO, instrucción|No se ha asignado.|  
|Los valores en la instrucción|No se ha asignado.|  
|Control de transacciones|No se ha asignado.|  
  
## <a name="converting-db2-database-objects"></a>Convertir objetos de base de datos de DB2  
Para convertir objetos de base de datos de DB2, primero seleccione los objetos que se va a convertir y, a continuación, tener SSMA para realizar la conversión. Para ver los mensajes de salida durante la conversión, en la **vista** menú, seleccione **salida**.  
  
**Para convertir objetos de DB2 a sintaxis de SQL Server**  
  
1.  En el Explorador de metadatos de DB2, expanda el servidor DB2 y, a continuación, expanda **esquemas**.  
  
2.  Seleccione los objetos que se va a convertir:  
  
    -   Para convertir todos los esquemas, active la casilla situada junto a **esquemas**.  
  
    -   Para convertir u omitir una base de datos, active la casilla de verificación situada junto al nombre de esquema.  
  
    -   Para convertir u omitir una categoría de objetos, expanda un esquema y, a continuación, active o desactive la casilla situada junto a la categoría.  
  
    -   Para convertir u omitir los objetos individuales, expanda la carpeta de la categoría y, a continuación, active o desactive la casilla de verificación situada junto al objeto.  
  
3.  Para convertir todos los objetos seleccionados, haga clic en **esquemas** y seleccione **convertir esquema**.  
  
    También puede convertir los objetos individuales o las categorías de objetos con el botón secundario en el objeto o su carpeta principal y, a continuación, seleccione **convertir esquema**.  
  
## <a name="viewing-conversion-problems"></a>Ver los problemas de conversión  
No se pueden convertir algunos objetos de DB2. Puede determinar las tasas de éxito de conversión visualizando el informe de resumen de conversión.  
  
**Para ver un informe de resumen**  
  
1.  En el Explorador de metadatos de DB2, seleccione **esquemas**.  
  
2.  En el panel derecho, seleccione la **informe** ficha.  
  
    Este informe muestra el informe de resumen de evaluación para todos los objetos de base de datos que se han evaluado o convertir. También puede ver un informe de resumen para objetos individuales:  
  
    -   Para ver el informe de un esquema en particular, seleccione el esquema en el Explorador de metadatos de DB2.  
  
    -   Para ver el informe de un objeto individual, seleccione el objeto en el Explorador de metadatos de DB2. Objetos que tienen problemas de conversión tienen un icono rojo de error.  
  
Para los objetos que no se pudo conversión, puede ver la sintaxis que produjo el error de conversión.  
  
**Para ver los problemas de conversión individuales**  
  
1.  En el Explorador de metadatos de DB2, expanda **esquemas**.  
  
2.  Expanda el esquema que muestra un icono rojo de error.  
  
3.  En el esquema, expanda una carpeta que tenga un icono rojo de error.  
  
4.  Seleccione el objeto que tiene un icono rojo de error.  
  
5.  En el panel derecho, haga clic en el **informe** ficha.  
  
6.  En la parte superior de la **informe** ficha es una lista desplegable. Si la lista muestra **estadísticas**, cambie la selección a **origen**.  
  
    SSMA mostrará el código fuente y varios botones inmediatamente encima del código.  
  
7.  Haga clic en el **problema siguiente** botón. Se trata de un icono de error rojo con una flecha que apunta a la derecha.  
  
    SSMA resaltará el primer código de origen problemático que encuentra en el objeto actual.  
  
Para cada elemento que no se pudo convertir, deberá determinar qué desea hacer con ese objeto:  
  
-   Puede modificar el código fuente de procedimientos en el **SQL** ficha.  
  
-   Puede modificar el objeto en la base de datos de DB2 para quitar o revisar cargue código problemático. Para cargar el código actualizado en SSMA, tendrá que actualizar los metadatos. Para obtener más información, consulte [conectarse a base de datos DB2 &#40; DB2ToSQL &#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md).  
  
-   Puede excluir el objeto de la migración. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Explorador de metadatos y el Explorador de metadatos de DB2, desactive la casilla de verificación situada junto al elemento antes de cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y migrar los datos de DB2.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración consiste en [cargar los objetos convertidos en SQL Server](http://msdn.microsoft.com/en-us/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3).  
  
## <a name="see-also"></a>Vea también  
[Migrar datos de DB2 en SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
