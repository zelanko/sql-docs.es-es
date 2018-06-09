---
title: Generación de informes (AccessToSQL) | Documentos de Microsoft
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: abb4264a-622e-4215-af5b-14e309b8a399
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 847fe8d703c003dd977945f1177bcaad9dae5185
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34773561"
---
# <a name="generating-reports-accesstosql"></a>Generación de informes (AccessToSQL)
Se generan los informes de ciertas actividades que se realizan mediante comandos en la consola SSMA al nivel de árbol de objetos.  
  
Utilice el procedimiento siguiente para generar informes:  
  
1.  Especifique el **escritura-resumen-informe de** parámetro. El informe al respecto se almacena como el nombre de archivo (si se especifica) o en la carpeta especifique. El nombre de archivo es definido por el sistema como se mencionó en la tabla siguiente where, **&lt;n&gt;** es el número de archivo único que se incrementa con un dígito con cada ejecución del mismo comando.  
  
    Los comandos de à respecto de los informes son:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Command**|**Título del informe**|  
    |1|informe de evaluación generar|AssessmentReport&lt;n&gt;. XML|  
    |2|convertir esquema|SchemaConversionReport&lt;n&gt;. XML|  
    |3|migrar datos|DataMigrationReport&lt;n&gt;. XML|  
    |4|destino sincronizar|TargetSynchronizationReport&lt;n&gt;. XML|  
    |5|actualización de base de datos|SourceDBRefreshReport&lt;n&gt;. XML|  
  
    > [!IMPORTANT]  
    > Un informe de salida es distinto de los informes de evaluación. El primero es un informe sobre el rendimiento de un comando ejecutado al, el segundo es un informe XML para su uso mediante programación.  
  
    Para las opciones de comando para los informes de salida (de Sl. No. 2 a 4 anteriores), consulte el [ejecutando la consola SSMA &#40;AccessToSQL&#41; ](../../ssma/access/executing-the-ssma-console-accesstosql.md) sección.  
  
2.  Indica el grado de detalle que desee en el informe de salida con la configuración de nivel de detalle del informe:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Parámetros y comandos**|**Descripción de salida**|  
    |1|detallado = "false"|Genera un informe resumido de la actividad.|  
    |2|detallado = "true"|Genera un informe de estado resumida y detallada para cada actividad.|  
  
    > [!NOTE]  
    > La configuración de nivel de detalle del informe especificada anteriormente son aplicable para informe de evaluación generar, convert-schema, comandos de migración de datos.  
  
3.  Indica el grado de detalle que desee en los informes de errores mediante la configuración de informe de errores:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Parámetros y comandos**|**Descripción de salida**|  
    |1|informe de errores = "false"|No hay detalles de error / advertencia / mensajes de información.|  
    |2|informe de errores = "true"|Error detallado / advertencia / mensajes de información.|  
  
    > [!NOTE]  
    > La configuración de informe de errores especificados anteriormente son aplicable para informe de evaluación generar, convert-schema, comandos de migración de datos.  
  
**Ejemplo:**  
  
```xml  
<generate-assessment-report  
  
    object-name="testschema"  
  
    object-type="Schemas"  
  
    verbose="yes"  
  
    report-erors="yes"  
  
    write-summary-report-to="$AssessmentFolder$\Report1.xml"  
  
    assessment-report-folder="$AssessmentFolder$\assesment_report"  
  
    assessment-report-overwrite="true"  
  
/>  
```  
  
### <a name="synchronize-target"></a>destino sincronizar:  
El comando **destino sincronizar** tiene **informe de errores a** parámetro, que especifica la ubicación del informe de error para la operación de sincronización. A continuación, un archivo con nombre **TargetSynchronizationReport&lt;n&gt;. XML** se crea en la ubicación especificada, donde **&lt;n&gt;** es el número de archivo único que se incrementa con un dígito con cada ejecución del mismo comando.  
  
**Nota:** si se proporciona la ruta de acceso de carpeta, el parámetro 'informe-errores-to' se convierte en un atributo opcional para el comando 'sincronizar el destino'.  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
    object-name="$TargetDB$.dbo"  
  
    on-error="fail-script"  
  
    report-errors-to="$SynchronizationReports$"  
  
/>  
```  
**nombre de objeto:** especifica los objetos que se consideran para la sincronización (también puede tener nombres de objeto de indivdual o un nombre de objeto de grupo).  
  
**error:** especifica si se debe especificar los errores de sincronización como advertencias o errores. Opciones disponibles en el error:  
  
-   total de informes como advertencia  
  
-   informes-each-como-advertencia  
  
-   Error-script  
  
### <a name="refresh-from-database"></a>actualización-de-base de datos:  
El comando **actualización de base de datos** tiene **informe de errores a** parámetro, que especifica la ubicación del informe de error para la operación de actualización. A continuación, un archivo con nombre **SourceDBRefreshReport&lt;n&gt;. XML** se crea en la ubicación especificada, donde **&lt;n&gt;** es el número de archivo único que se incrementa con un dígito con cada ejecución del mismo comando.  
  
**Nota:** si se proporciona la ruta de acceso de carpeta, el parámetro 'informe-errores-to' se convierte en un atributo opcional para el comando 'sincronizar el destino'.  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
    object-name="$SourceDatabaseStandard$"  
  
    object-type ="Databases"  
  
    on-error="fail-script"  
  
    report-errors-to="$RefreshDBFolder$\RefreshReport.xml"  
  
/>  
```  
**nombre de objeto:** especifica los objetos que se consideran para la actualización (también puede tener nombres de objeto de indivdual o un nombre de objeto de grupo).  
  
**error:** especifica si se debe especificar la actualización de errores como advertencias o errores. Opciones disponibles en el error:  
  
-   total de informes como advertencia  
  
-   informes-each-como-advertencia  
  
-   Error-script  
  
## <a name="see-also"></a>Vea también  
[Ejecutar la consola SSMA (Access)](http://msdn.microsoft.com/en-us/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
