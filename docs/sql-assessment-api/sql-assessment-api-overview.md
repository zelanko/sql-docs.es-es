---
title: API SQL Server Assessment
description: En este artículo se trata la API SQL Server Assessment.
ms.prod: sql
ms.technology: tools-other
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 11/04/2019
ms.openlocfilehash: 76a6e99d06061ae581b753ce0edd96a5a82d0f95
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "78946719"
---
# <a name="sql-assessment-api"></a>API de SQL Assessment

La API SQL Server Assessment ofrece un mecanismo para evaluar la configuración de la instancia de SQL Server a efectos de los procedimientos recomendados. La API se entrega con un conjunto de reglas que contiene las reglas de procedimientos recomendados sugeridas por el equipo de SQL Server. Este conjunto de reglas se está mejorando con el lanzamiento de nuevas versiones, pero cabe destacar que, al mismo tiempo, la API se ha diseñado con el objetivo de proporcionar una solución altamente personalizable y extensible. Por lo tanto, los usuarios pueden ajustar las reglas predeterminadas y crear las suyas propias.

La API SQL Server Assessment resulta útil si quiere asegurarse de que la configuración de SQL Server esté en consonancia con los procedimientos recomendados. Después de una valoración inicial, se puede realizar un seguimiento de la estabilidad de la configuración mediante evaluaciones programadas periódicamente.

La API se puede usar para evaluar Instancia administrada de Azure SQL Database y SQL Server (versión 2012 y posteriores). Asimismo, SQL se admite en Linux.

## <a name="rules"></a>Reglas

Las reglas, a las que a veces se hace referencia como "comprobaciones", se definen en archivos con formato JSON. El formato del conjunto de reglas requiere que se especifique el nombre y la versión de este. Por lo tanto, al usar conjuntos de reglas personalizados, podrá saber fácilmente qué recomendaciones proceden de los distintos conjunto de reglas. 

El conjunto de reglas de Microsoft está disponible en GitHub. Puede visitar el [repositorio de ejemplos](https://aka.ms/sql-assessment-api) para obtener más detalles.

## <a name="sql-assessment-cmdlets-and-smo-extension"></a>Cmdlets de SQL Assessment y extensión de SMO

La API SQL Server Assessment forma parte de la versión de lanzamiento de [Objetos de administración de SQL Server (SMO)](../relational-databases/server-management-objects-smo/installing-smo.md) de julio de 2019 y versiones posteriores, y de la versión de lanzamiento del módulo [SQL Server PowerShell](../powershell/download-sql-server-ps-module.md) de julio de 2019 y versiones posteriores.

* [Instalación de SMO](../relational-databases/server-management-objects-smo/installing-smo.md)

* [Instalación de un módulo de SQL Server PowerShell](../powershell/download-sql-server-ps-module.md)

El módulo SqlServer incluye dos nuevos cmdlets para trabajar con la API SQL Server Assessment:

* **Get-SqlAssessmentItem**: ofrece una lista de las comprobaciones de valoración disponibles para un objeto SQL Server.

* **Invoke-SqlAssessment**: facilita los resultados de una valoración.

El marco de SMO se complementa con la extensión de la API SQL Server Assessment que proporciona los métodos siguientes:

* **GetAssessmentItems** : devuelve las comprobaciones disponibles para un objeto SQL determinado (IEnumerable<…>).

* **GetAssessmentResults** : evalúa sincrónicamente la valoración y devuelve los resultados y errores, si hay alguno (IEnumerable<…>).

* **GetAssessmentResultsList** : evalúa sincrónicamente la valoración y devuelve los resultados y errores, si hay alguno (Task<…>).

## <a name="get-started-using-sql-assessment-cmdlets"></a>Introducción al uso de cmdlets de SQL Server Assessment

Se realiza una valoración en un objeto de SQL Server determinado. En el conjunto de reglas predeterminado, solo hay comprobaciones para dos tipos de objetos: Server y Database (además de ellos, la API admite dos tipos más, Filegroup y AvailabilityGroup). Si quiere evaluar una instancia de SQL y todas sus bases de datos, debe ejecutar los cmdlets de SQL Server Assessment para cada objeto por separado. También puede pasar objetos para su valoración a los cmdlets de SQL Server Assessment en una variable o la canalización.

Los objetos SqlServer y RegisteredServer son intercambiables, por lo que puede pasar cualquiera a los cmdlets de SQL Server Assessment.

Repase estos ejemplos para empezar.

1. Obtenga una lista de las comprobaciones disponibles para una instancia predeterminada local a fin de familiarizarse con las comprobaciones. En este ejemplo, se canaliza la salida del cmdlet Get-SqlInstance al cmdlet Get-SqlAssessmentItem para pasarle el objeto de la instancia.

    ```powershell
    Get-SqlInstance -ServerInstance 'localhost' | Get-SqlAssessmentItem
    ```

2. Obtenga una lista de las comprobaciones disponibles para todas las bases de datos de la instancia. Aquí se va a usar el cmdlet Get-Item y una ruta de acceso implementada con el proveedor de SQL Server de Windows PowerShell para obtener una lista de las bases de datos y, luego, canalizarla con el cmdlet Get-SqlDatabase.

    ```powershell
    Get-Item SQLSERVER:\SQL\localhost\default | Get-SqlAssessmentItem
    ```

    Además, puede usar el cmdlet Get-SqlDatabase para hacer lo mismo.

    ```powershell
    Get-SqlDatabase -ServerInstance 'localhost' | Get-SqlAssessmentItem
    ```

3. Obtenga una lista de las comprobaciones disponibles para todas las bases de datos de la instancia. Aquí se va a usar el cmdlet Get-Item y una ruta de acceso implementada con el proveedor de SQL Server de Windows PowerShell para obtener una lista de las bases de datos y, luego, canalizarla con el cmdlet Get-SqlDatabase.

    ```powershell
    Get-Item SQLSERVER:\SQL\localhost\default | Get-SqlAssessmentItem
    ```

    Además, puede usar el cmdlet Get-SqlDatabase para hacer lo mismo.

    ```powershell
    Get-SqlDatabase -ServerInstance 'localhost' | Get-SqlAssessmentItem
    ```

4. Invoque la valoración de la instancia y guarde los resultados en una tabla SQL. En este ejemplo, se canaliza la salida del cmdlet Get-SqlInstance al cmdlet Invoke-SqlAssessment, cuyos resultados se canalizan al cmdlet Write-SqlTableData. En este ejemplo, el cmdlet Invoke-Assessment se ejecuta con el parámetro `-FlattenOutput`. Este parámetro hace que la salida sea adecuada para el cmdlet Write-SqlTableData. En el último caso, se produce un error si se omite el parámetro.

    ```powershell
    Get-SqlInstance -ServerInstance 'localhost' |
    Invoke-SqlAssessment -FlattenOutput |
    Write-SqlTableData -ServerInstance 'localhost' -DatabaseName SQLAssessmentDemo -SchemaName Assessment -TableName Results -Force
    ```

    Ahora vamos a invocar una valoración para todas las bases de datos de la instancia y agregar los resultados a la misma tabla.

    ```powershell
    Get-SqlDatabase -ServerInstance 'localhost' |
    Invoke-SqlAssessment -FlattenOutput |
    Write-SqlTableData -ServerInstance 'localhost' -DatabaseName SQLAssessmentDemo -SchemaName Assessment -TableName Results -Force
    ```

5. Siga las descripciones y los vínculos de la tabla para comprender mejor las recomendaciones.

6. Personalice las reglas en función de su entorno y los requisitos de la organización; puede consultarlos a continuación.

7. Programe una tarea o un trabajo para ejecutar la valoración periódicamente o a petición para medir el progreso.

## <a name="customizing-rules"></a>Personalización de las reglas

Las reglas están diseñadas para ser personalizables y extensibles. El conjunto de reglas de Microsoft está diseñado para funcionar en la mayoría de los entornos. Sin embargo, es imposible tener un conjunto de reglas que funcione con todos los entornos. Los usuarios pueden escribir sus propios archivos JSON y personalizar las reglas existentes o agregar otras nuevas. En el [repositorio de ejemplos](https://aka.ms/sql-assessment-api) hay disponibles ejemplos de personalización y un conjunto de reglas completo publicado por Microsoft. Para obtener más información sobre cómo ejecutar los cmdlets de SQL Server Assessment con archivos JSON personalizados, use el cmdlet Get-Help.

### <a name="options-available-with-rule-customization-feature"></a>Opciones disponibles con la característica de personalización de reglas

#### <a name="enablingdisabling-certain-rules-or-groups-of-rules-using-tags"></a>Habilitación y deshabilitación de ciertas reglas o grupos de reglas (mediante etiquetas)

Puede silenciar reglas específicas cuando no sean aplicables a su entorno o hasta que se realicen trabajos programados para rectificar el problema.

#### <a name="changing-threshold-parameters"></a>Cambio de parámetros de umbral

Las reglas específicas tienen umbrales que se comparan con el valor actual de una métrica para averiguar un problema. Si los umbrales predeterminados no se ajustan a sus necesidades, puede cambiarlos.

#### <a name="adding-more-rules-written-by-you-or-third-parties"></a>Incorporación de otras reglas escritas por usted o por terceros

Puede encadenar conjuntos de reglas agregando uno o más archivos JSON como parámetros a la llamada API SQL Server Assessment. Su organización podría escribir esos archivos u obtenerlos de un tercero. Por ejemplo, puede tener el archivo JSON que deshabilite reglas específicas del conjunto de reglas de Microsoft y otro archivo JSON de un experto del sector que incluya reglas que le resulten útiles para su entorno, seguido de otro archivo JSON que cambie algunos valores de umbral en ese archivo JSON.

> [!IMPORTANT]  
> Le recomendamos que no utilice conjuntos de reglas que provengan de fuentes que no sean de confianza hasta que los haya revisado detenidamente para asegurarse de que sean seguros.

## <a name="next-steps"></a>Pasos siguientes

Eche un vistazo a [Objetos de administración de SQL Server (SMO)](../relational-databases/server-management-objects-smo/overview-smo.md) y [PowerShell](../powershell/download-sql-server-ps-module.md).
