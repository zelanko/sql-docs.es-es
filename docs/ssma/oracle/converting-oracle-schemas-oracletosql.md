---
title: Convertir esquemas de Oracle (OracleToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Conversion Results
ms.assetid: e021182d-31da-443d-b110-937f5db27272
caps.latest.revision: 14
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 50294e2048a3fb494e683cfdb20b5eecd8662ca4
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="converting-oracle-schemas-oracletosql"></a>Convertir esquemas de Oracle (OracleToSQL)
Después de haberse conectado a Oracle, conectado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], y el proyecto de conjunto y las opciones de asignación de datos, puede convertir objetos de base de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos de base de datos.  
  
## <a name="the-conversion-process"></a>El proceso de conversión  
Convertir objetos de base de datos toma las definiciones de objeto de Oracle, se convierte en similar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos y, a continuación, se carga esta información en los metadatos SSMA. No se carga la información en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. A continuación, puede ver los objetos y sus propiedades mediante el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Explorador de metadatos.  
  
Durante la conversión, SSMA imprime mensajes de salida en el panel de resultados y mensajes de error en el panel de lista de errores. Use la información de salida y el error para determinar si tiene que modificar las bases de datos de Oracle o el proceso de conversión para obtener los resultados de la conversión deseada.  
  
## <a name="setting-conversion-options"></a>Establecer las opciones de conversión  
Antes de convertir objetos, revise las opciones de conversión de proyecto en el **configuración del proyecto** cuadro de diálogo. Mediante este cuadro de diálogo, puede establecer cómo SSMA convierte las funciones y variables globales. Para obtener más información, vea [configuración del proyecto &#40; Conversión &#41; &#40; OracleToSQL &#41; ](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
## <a name="conversion-results"></a>Resultados de la conversión  
La siguiente tabla muestra qué objetos de Oracle se convierten y resultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos:  
  
|||  
|-|-|  
|Objetos de Oracle|Objetos SQL Server resultantes|  
|Funciones|Si la función se puede convertir directamente a [!INCLUDE[tsql](../../includes/tsql_md.md)], SSMA crea una función.<br /><br />En algunos casos, la función debe convertirse en un procedimiento almacenado. En este caso, SSMA crea un procedimiento almacenado y una función que llama al procedimiento almacenado.|  
|Procedimientos|Si el procedimiento se puede convertir directamente a [!INCLUDE[tsql](../../includes/tsql_md.md)], SSMA crea un procedimiento almacenado.<br /><br />En algunos casos, un procedimiento almacenado debe llamarse en una transacción autónoma. En este caso, SSMA crea dos procedimientos almacenados: uno que implementa el procedimiento y otro que se usa para llamar a la implementación de procedimiento almacenado.|  
|.|SSMA crea un conjunto de procedimientos almacenados y funciones que se unifican de nombres de objetos similares.|  
|Secuencias|SSMA crea objetos de secuencia (SQL Server 2012 o SQL Server 2014) o emula las secuencias de Oracle.|  
|Tablas con los objetos dependientes, como índices y desencadenadores|SSMA crea tablas con los objetos dependientes.|  
|Ver con los objetos dependientes, como los desencadenadores|SSMA crea vistas con los objetos dependientes.|  
|Vistas materializadas|**SSMA crea vistas indizadas en SQL server con algunas excepciones. Se producirá un error en la conversión si la vista materializada incluye una o varias de las construcciones siguientes:**<br /><br />Función definida por el usuario<br /><br />Campo no determinista / función / expresión SELECT, donde o cláusulas GROUP BY<br /><br />Uso de la columna de tipo Float de SELECT *, donde o cláusulas GROUP BY (caso especial de problema anterior)<br /><br />Tipo de datos personalizado (incluido anidadas tablas)<br /><br />COUNT (distinct &lt;campo&gt;)<br /><br />FETCH<br /><br />Combinaciones externas (LEFT, RIGHT o FULL)<br /><br />Subconsulta, otra vista<br /><br />OTRA VEZ, CLASIFICAR, CLIENTE POTENCIAL, INICIAR SESIÓN<br /><br />MIN, MAX<br /><br />UNION, MENOS, FORMAN UNA INTERSECCIÓN<br /><br />HAVING|  
|Desencadenador|**SSMA crea desencadenadores según las reglas siguientes:**<br /><br />ANTES de que los desencadenadores se convierten en desencadenadores INSTEAD OF.<br /><br />Desencadenadores AFTER se convierten en desencadenadores AFTER.<br /><br />Los desencadenadores INSTEAD OF se convierten en desencadenadores INSTEAD OF. Varios desencadenadores INSTEAD OF definidos en la misma operación se combinan en un desencadenador.<br /><br />Desencadenadores de nivel de fila se emulan con cursores.<br /><br />Desencadenadores en cascada se convierten en varios desencadenadores individuales.|  
|Sinónimos|**Sinónimos se crean para los siguientes tipos de objeto:**<br /><br />Tablas y las tablas de objeto<br /><br />Vistas y vistas de objetos<br /><br />Procedimientos almacenados<br /><br />Funciones<br /><br />**Sinónimos de los objetos siguientes están resueltas y reemplazados por las referencias de objeto directo:**<br /><br />Secuencias<br /><br />.<br /><br />Objetos de esquema de clase de Java<br /><br />Tipos de objetos definidos por el usuario<br /><br />Sinónimos de otro sinónimo no se pueden migrar y se marcarán como errores.<br /><br />Sinónimos no se crean para las vistas de Materialized.|  
|Tipos definidos por el usuario|**SSMA no proporciona compatibilidad para la conversión de tipos definidos por el usuario. Tipos definidos por el usuario, incluyendo su uso en programas de PL/SQL se marcan con errores de conversión especial guiados por las reglas siguientes:**<br /><br />Columna de tabla de un tipo definido por el usuario se convierte en VARCHAR(8000).<br /><br />Tipo definido por el argumento de entrada de usuario a un procedimiento almacenado o función se convierte en VARCHAR(8000).<br /><br />Variable de tipo definido por el usuario en el bloque de PL/SQL se convierte en VARCHAR(8000).<br /><br />Tabla de objetos se convierte en una tabla estándar.<br /><br />Vista de objeto se convierte en una vista estándar.|  
  
## <a name="converting-oracle-database-objects"></a>Convertir objetos de base de datos de Oracle  
Para convertir objetos de base de datos de Oracle, seleccione primero los objetos que se va a convertir y, a continuación, tener SSMA para realizar la conversión. Para ver los mensajes de salida durante la conversión, en la **vista** menú, seleccione **salida**.  
  
**Para convertir objetos de Oracle a la sintaxis de SQL Server**  
  
1.  En el Explorador de metadatos de Oracle, expanda el servidor de Oracle y, a continuación, expanda **esquemas**.  
  
2.  Seleccione los objetos que se va a convertir:  
  
    -   Para convertir todos los esquemas, active la casilla situada junto a **esquemas**.  
  
    -   Para convertir u omitir una base de datos, active la casilla de verificación situada junto al nombre de esquema.  
  
    -   Para convertir u omitir una categoría de objetos, expanda un esquema y, a continuación, active o desactive la casilla situada junto a la categoría.  
  
    -   Para convertir u omitir los objetos individuales, expanda la carpeta de la categoría y, a continuación, active o desactive la casilla de verificación situada junto al objeto.  
  
3.  Para convertir todos los objetos seleccionados, haga clic en **esquemas** y seleccione **convertir esquema**.  
  
    También puede convertir los objetos individuales o las categorías de objetos con el botón secundario en el objeto o su carpeta principal y, a continuación, seleccione **convertir esquema**.  
  
## <a name="viewing-conversion-problems"></a>Ver los problemas de conversión  
No se pueden convertir algunos objetos de Oracle. Puede determinar las tasas de éxito de conversión visualizando el informe de resumen de conversión.  
  
**Para ver un informe de resumen**  
  
1.  En el Explorador de metadatos de Oracle, seleccione **esquemas**.  
  
2.  En el panel derecho, seleccione la **informe** ficha.  
  
    Este informe muestra el informe de resumen de evaluación para todos los objetos de base de datos que se han evaluado o convertir. También puede ver un informe de resumen para objetos individuales:  
  
    -   Para ver el informe de un esquema en particular, seleccione el esquema en el Explorador de metadatos de Oracle.  
  
    -   Para ver el informe de un objeto individual, seleccione el objeto en el Explorador de metadatos de Oracle. Objetos que tienen problemas de conversión tienen un icono rojo de error.  
  
Para los objetos que no se pudo conversión, puede ver la sintaxis que produjo el error de conversión.  
  
**Para ver los problemas de conversión individuales**  
  
1.  En el Explorador de metadatos de Oracle, expanda **esquemas**.  
  
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
  
-   Puede modificar el objeto en la base de datos de Oracle para quitar o revisar cargue código problemático. Para cargar el código actualizado en SSMA, tendrá que actualizar los metadatos. Para obtener más información, consulte [conectarse a base de datos de Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   Puede excluir el objeto de la migración. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Explorador de metadatos y el Explorador de metadatos de Oracle, desactive la casilla de verificación situada junto al elemento antes de cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y migración de datos de Oracle.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso del proceso de migración consiste en [cargar los objetos convertidos en SQL Server](http://msdn.microsoft.com/en-us/a8ae33b2-1883-4785-922b-ea0e31c0b37a).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Oracle a SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

