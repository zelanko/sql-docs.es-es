---
title: Generación de informes (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Report Generation in Oracle Console, synchronize-target
- Report Generation in Oracle Console,refresh-from-database
- Report Generation in Oracle Console,write-summary-report-to
ms.assetid: ccad6262-01e1-447a-bd2b-c105154c80ce
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: a1f175de4b205b6af98ea9bcc29e7679711b0943
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192384"
---
# <a name="generating-reports-oracletosql"></a>Generación de informes (OracleToSQL)
Se generan los informes de ciertas actividades realizadas mediante comandos en la consola de SSMA en nivel de árbol de objetos.  
  
Use el procedimiento siguiente para generar informes:  
  
1.  Especifique el **escritura-resumen-informe de** parámetro. El informe relacionado se almacena como el nombre de archivo (si se especifica) o en la carpeta que especifique. El nombre de archivo es definido por el sistema como se mencionó en la tabla siguiente where, **&lt;n&gt;** es el número de archivo único que se incrementa con un dígito con cada ejecución del mismo comando.  
  
    Los comandos de vis-con respecto de los informes son:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Command**|**Título de informe**|  
    |1|generate-assessment-report|AssessmentReport&lt;n&gt;.XML|  
    |2|convert-schema|SchemaConversionReport&lt;n&gt;.XML|  
    |3|migrar datos|DataMigrationReport&lt;n&gt;.XML|  
    |4|convert-sql-statement|ConvertSQLReport&lt;n&gt;.XML|  
    |5|sincronizar de destino|TargetSynchronizationReport&lt;n&gt;.XML|  
    |6|refresh-from-database|SourceDBRefreshReport&lt;n&gt;.XML|  
  
    > [!IMPORTANT]  
    > Un informe de salida es distinto de informe de evaluación. El primero es un informe sobre el rendimiento de un comando ejecutado al, el segundo es un informe XML para su consumo mediante programación.  
  
    Para las opciones de comando para los informes de salida (de Sl. No. 2 a 4 anteriores), consulte el [ejecutando la consola de SSMA &#40;OracleToSQL&#41; ](../../ssma/oracle/executing-the-ssma-console-oracletosql.md) sección.  
  
2.  Indicar el grado de detalle que desee en el informe de salida con la configuración de nivel de detalle del informe:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Parámetros y comandos**|**Descripción de salida**|  
    |1|verbose="false"|Genera un informe resumido de la actividad.|  
    |2|verbose="true"|Genera un informe de estado resumido y detallado para cada actividad.|  
  
    > [!NOTE]  
    > La configuración de nivel de detalle del informe especificada anteriormente son aplicable para el informe de evaluación generar, esquema de convert, migrar datos, los comandos de la instrucción convert-sql.  
  
3.  Indicar el grado de detalle que desea para los informes de errores mediante la configuración de informes de errores:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Parámetros y comandos**|**Descripción de salida**|  
    |1|report-errors="false"|No hay detalles de un error / advertencia / mensajes de información.|  
    |2|report-errors="true"|Error detallado / advertencia / mensajes de información.|  
  
    > [!NOTE]  
    > La configuración de informe de errores especificados anteriormente son aplicable para el informe de evaluación generar, esquema de convert, migrar datos, los comandos de la instrucción convert-sql.  
  
**Ejemplo:**  
  
```  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-type>"  
  
   verbose="<true/false>"  
  
   report-erors="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   assessment-report-folder="<folder-name>"  
  
   assessment-report-overwrite="<true/false>"/>  
```  
  
### <a name="synchronize-target"></a>sincronizar-target:  
El comando **destino sincronizar** tiene **informe de errores a** parámetro, que especifica la ubicación del informe de errores para la operación de sincronización. A continuación, un archivo con nombre **TargetSynchronizationReport&lt;n&gt;. XML** se crea en la ubicación especificada, donde **&lt;n&gt;** es el número de archivo único que se incrementa con un dígito con cada ejecución del mismo comando.  
  
**Nota:** Si se especifica la ruta de acceso de carpeta, parámetro 'informe de errores-to' se convierte en un atributo opcional para el comando 'sincronizar-target'.  
  
```  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**object-name:** Especifica los objetos que se consideran para la sincronización (también puede tener nombres de objeto de la emisora o un nombre de objeto de grupo).  
  
**on-error:** Especifica si se debe especificar los errores de sincronización como advertencias o errores. Opciones disponibles para en caso de error:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   fail-script  
  
### <a name="refresh-from-database"></a>actualización-de-database:  
El comando **actualización de base de datos** tiene **informe de errores a** parámetro, que especifica la ubicación del informe de errores para la operación de actualización. A continuación, un archivo con nombre **SourceDBRefreshReport&lt;n&gt;. XML** se crea en la ubicación especificada, donde **&lt;n&gt;** es el número de archivo único que se incrementa con un dígito con cada ejecución del mismo comando.  
  
**Nota:** Si se especifica la ruta de acceso de carpeta, parámetro 'informe de errores-to' se convierte en un atributo opcional para el comando 'sincronizar-target'.  
  
```  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type ="<object-type>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**object-name:** Especifica los objetos que se consideran para la actualización (también puede tener nombres de objeto de la emisora o un nombre de objeto de grupo).  
  
**on-error:** Especifica si se debe especificar la actualización de errores como advertencias o errores. Opciones disponibles para en caso de error:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   fail-script  
  
## <a name="see-also"></a>Vea también  
[Ejecución de la consola SSMA (Oracle)](https://msdn.microsoft.com/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
