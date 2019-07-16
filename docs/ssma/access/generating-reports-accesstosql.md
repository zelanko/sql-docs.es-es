---
title: Generación de informes (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: abb4264a-622e-4215-af5b-14e309b8a399
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: d9d1879cd5583ee7b87c12edb19bf5486cee4fcf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986435"
---
# <a name="generating-reports-accesstosql"></a>Generación de informes (AccessToSQL)
Se generan los informes de ciertas actividades realizadas mediante comandos en la consola de SSMA en nivel de árbol de objetos.  
  
Use el procedimiento siguiente para generar informes:  
  
1.  Especifique el **escritura-resumen-informe de** parámetro. El informe relacionado se almacena como el nombre de archivo (si se especifica) o en la carpeta que especifique. El nombre de archivo es definido por el sistema como se mencionó en la tabla siguiente where, **&lt;n&gt;** es el número de archivo único que se incrementa con un dígito con cada ejecución del mismo comando.  
  
    Los comandos de vis-con respecto de los informes son:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Command**|**Título de informe**|  
    |1|informe de evaluación generar|AssessmentReport&lt;n&gt;.XML|  
    |2|convertir esquema|SchemaConversionReport&lt;n&gt;.XML|  
    |3|migrar datos|DataMigrationReport&lt;n&gt;.XML|  
    |4|sincronizar de destino|TargetSynchronizationReport&lt;n&gt;.XML|  
    |5|actualización de base de datos|SourceDBRefreshReport&lt;n&gt;.XML|  
  
    > [!IMPORTANT]  
    > Un informe de salida es distinto de informe de evaluación. El primero es un informe sobre el rendimiento de un comando ejecutado al, el segundo es un informe XML para su consumo mediante programación.  
  
    Para las opciones de comando para los informes de salida (de Sl. No. 2 a 4 anteriores), consulte el [ejecutando la consola de SSMA &#40;AccessToSQL&#41; ](../../ssma/access/executing-the-ssma-console-accesstosql.md) sección.  
  
2.  Indicar el grado de detalle que desee en el informe de salida con la configuración de nivel de detalle del informe:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Parámetros y comandos**|**Descripción de salida**|  
    |1|verbose="false"|Genera un informe resumido de la actividad.|  
    |2|verbose="true"|Genera un informe de estado resumido y detallado para cada actividad.|  
  
    > [!NOTE]  
    > La configuración de nivel de detalle del informe especificada anteriormente son aplicable para el informe de evaluación generar, esquema de convert, comandos de migración de datos.  
  
3.  Indicar el grado de detalle que desea para los informes de errores mediante la configuración de informes de errores:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Parámetros y comandos**|**Descripción de salida**|  
    |1|informe de errores = "false"|No hay detalles de un error / advertencia / mensajes de información.|  
    |2|informe de errores = "true"|Error detallado / advertencia / mensajes de información.|  
  
    > [!NOTE]  
    > La configuración de informe de errores especificados anteriormente son aplicable para el informe de evaluación generar, esquema de convert, comandos de migración de datos.  
  
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
  
### <a name="synchronize-target"></a>sincronizar-target:  
El comando **destino sincronizar** tiene **informe de errores a** parámetro, que especifica la ubicación del informe de errores para la operación de sincronización. A continuación, un archivo con nombre **TargetSynchronizationReport&lt;n&gt;. XML** se crea en la ubicación especificada, donde **&lt;n&gt;** es el número de archivo único que se incrementa con un dígito con cada ejecución del mismo comando.  
  
**Nota:** Si se especifica la ruta de acceso de carpeta, parámetro 'informe de errores-to' se convierte en un atributo opcional para el comando 'sincronizar-target'.  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
    object-name="$TargetDB$.dbo"  
  
    on-error="fail-script"  
  
    report-errors-to="$SynchronizationReports$"  
  
/>  
```  
**object-name:** Especifica los objetos que se consideran para la sincronización (también puede tener nombres de objeto de la emisora o un nombre de objeto de grupo).  
  
**en caso de error:** Especifica si se debe especificar los errores de sincronización como advertencias o errores. Opciones disponibles para en caso de error:  
  
-   report-total-as-warning  
  
-   informes-each-como-warning  
  
-   Error de script  
  
### <a name="refresh-from-database"></a>actualización-de-database:  
El comando **actualización de base de datos** tiene **informe de errores a** parámetro, que especifica la ubicación del informe de errores para la operación de actualización. A continuación, un archivo con nombre **SourceDBRefreshReport&lt;n&gt;. XML** se crea en la ubicación especificada, donde **&lt;n&gt;** es el número de archivo único que se incrementa con un dígito con cada ejecución del mismo comando.  
  
**Nota:** Si se especifica la ruta de acceso de carpeta, parámetro 'informe de errores-to' se convierte en un atributo opcional para el comando 'sincronizar-target'.  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
    object-name="$SourceDatabaseStandard$"  
  
    object-type ="Databases"  
  
    on-error="fail-script"  
  
    report-errors-to="$RefreshDBFolder$\RefreshReport.xml"  
  
/>  
```  
**object-name:** Especifica los objetos que se consideran para la actualización (también puede tener nombres de objeto de la emisora o un nombre de objeto de grupo).  
  
**en caso de error:** Especifica si se debe especificar la actualización de errores como advertencias o errores. Opciones disponibles para en caso de error:  
  
-   report-total-as-warning  
  
-   informes-each-como-warning  
  
-   Error de script  
  
## <a name="see-also"></a>Vea también  
[Ejecución de la consola SSMA (acceso)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
