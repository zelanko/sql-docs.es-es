---
title: Tarea de Azure Data Lake Analytics | Microsoft Docs
ms.custom: ''
ms.date: 05/18/2018
ms.prod: sql
ms.prod_service: integration-services
ms.component: control-flow
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: yanancai
ms.author: yanacai
manager: craigg
ms.openlocfilehash: 395d790069294aed541f9756fa7caefbb62f9a7b
ms.sourcegitcommit: 44e9bf62f2c75449c17753ed66bf85c43928dbd5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2018
ms.locfileid: "37854433"
---
# <a name="azure-data-lake-analytics-task"></a>Tarea de Azure Data Lake Analytics

La tarea de Azure Data Lake Analytics permite que los usuarios envíen trabajos de U-SQL al servicio Azure Data Lake Analytics. [Azure Data Lake Analytics (ADLA)](https://azure.microsoft.com/services/data-lake-analytics/).

La tarea de Azure Data Lake Analytics Task es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

## <a name="configure-the-azure-data-lake-analytics-task"></a>Configuración de la Tarea de Azure Data Lake Analytics

Para agregar una tarea de Azure Data Lake Analytics a un paquete, arrástrela desde el cuadro de herramientas de SSIS al lienzo del diseñador. Después, haga doble clic en la tarea o clic con el botón derecho y seleccione **Editar**, para abrir el cuadro de diálogo **Azure Data Lake Analytics Task Editor** (Editor de la tarea de Azure Data Lake Analytics). Puede establecer propiedades a través del Diseñador de SSIS o mediante programación.

## <a name="general-page-configuration"></a>Configuración de la página General

Use la página **General** para configurar la tarea de Azure Data Lake Analytics y proporcione el script de U-SQL que la tarea envía. Para más información sobre el lenguaje U-SQL, consulte el artículo sobre la [referencia del lenguaje U-SQL](https://msdn.microsoft.com/azure/data-lake-analytics/u-sql/u-sql-language-reference).

### <a name="basic-configuration"></a>Configuración básica

- **Name** (Nombre): especifica el nombre de la tarea de Azure Data Lake Analytics.
- **Description** (Descripción): especifica la descripción de la tarea de Azure Data Lake Analytics.

### <a name="u-sql-configuration"></a>Configuración de U-SQL

La configuración de U-SQL tiene dos valores: **SourceType** y opciones dinámicas en función del valor de **SourceType**. 

- **SourceType**: especifica el origen del script de U-SQL. El script se enviará a una cuenta de Azure Data Lake Analytics durante la ejecución del paquete SSIS. Esta propiedad presenta tres opciones indicadas en la tabla siguiente.

|Valor|Descripción|  
|-----------|-----------------|  
|**DirectInput**|Especifica el script de U-SQL a través del editor insertado. Si selecciona este valor, se mostrará la opción dinámica **USQLStatement**.|  
|**FileConnection**|Especifica un archivo .usql local que contiene el script de U-SQL. Si selecciona esta opción, se mostrará la opción dinámica **FileConnection**.|  
|**Variable**|Especifica una variable SSIS que contiene el script de U-SQL. Si selecciona este valor, se mostrará la opción dinámica **SourceVariable**.|

- **SourceType Dynamic Options** (Opciones dinámicas de SourceType): especifica el contenido del script de la consulta U-SQL. 

|Tipo de origen|Opciones dinámicas|  
|-----------|-----------------|  
|**SourceType = DirectInput**|Escriba la consulta U-SQL que se enviará directamente en el cuadro de opción o haga clic en el botón Examinar (...) para escribir la consulta U-SQL en el cuadro de diálogo **Enter U-SQL Query** (Escribir consulta U-SQL).|  
|**SourceType = FileConnection**|Seleccione un administrador de conexiones de archivos existente o haga clic en <**Nueva conexión...**> para crear una nueva conexión de archivos. **Artículo relacionado:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md) (Administrador de conexiones de archivos), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md) (Editor del administrador de conexiones de archivos)|  
|**SourceType = Variable**|Seleccione una variable existente o haga clic en \<**Nueva variable…**> para crear una. **Artículo relacionado:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Agregar variable](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)|


### <a name="job-configuration"></a>Configuración del trabajo
La configuración del trabajo especifica las propiedades del envío del trabajo de U-SQL.

- **AzureDataLakeAnalyticsConnection**: especifica la cuenta de Azure Data Lake Analytics donde se enviará el script de U-SQL. Elija la conexión en la lista de administradores de conexión definidos. Para crear una conexión, seleccione <**Nueva conexión**>. Artículo relacionado: [Administrador de conexiones de Azure Data Lake Analytics](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md).

- **JobName**: especifica el nombre del trabajo de U-SQL. 
- **AnalyticsUnits**: especifica el número de unidades de análisis del trabajo de U-SQL.
- **Priority** (Prioridad): especifica la prioridad del trabajo de U-SQL. La prioridad se puede establecer de 0 a 1000 y cuanto menor sea el número, mayor será la prioridad.
- **RuntimeVersion**: especifica la versión en tiempo de ejecución de Azure Data Lake Analytics del trabajo de U-SQL. De manera predeterminada, está establecido en "default". Por lo general, no es necesario modificar esta propiedad.
- **Synchronous** (Sincrónico): un valor booleano especifica si la tarea espera que se complete la ejecución del trabajo o no. Si se establece en True, la tarea se marcará como realizada correctamente una vez que se complete el trabajo. Si se establece en False, la tarea se marcará como realizada correctamente una vez que el trabajo pase la fase de preparación.

|Valor|Descripción|
|-----------|-----------------|
|True|El resultado de la tarea se basa en el resultado de la ejecución del trabajo de U-SQL. El trabajo se realiza correctamente --> La tarea se realiza correctamente; El trabajo no se realiza --> La tarea no se realiza; La tarea se realiza correctamente o no se realiza --> La tarea se completa.|
|False|El resultado de la tarea se basa en el resultado de la preparación y el envío del trabajo de U-SQL. El envío del trabajo se realiza correctamente y pasa la fase de preparación --> La tarea se realiza correctamente; El envío del trabajo no se realiza o el trabajo no pasa la fase de preparación --> La tarea no se realiza; La tarea se realiza correctamente o no se realiza --> La tarea se completa.|

- **TimeOut** (Tiempo de espera): especifica un tiempo de espera en segundos para la ejecución del trabajo. El trabajo se cancelará y la tarea se marcará como no realizada una vez que se agote el tiempo de espera del trabajo. La propiedad TimeOut no está disponible si Synchronous (Sincrónico) está establecido en False. La propiedad TimeOut no está disponible si **Synchronous** (Sincrónico) está establecido en **false**.

## <a name="parameter-mapping-page-configuration"></a>Configuración de la página de asignación de parámetros

Use la página **Asignación de parámetros** del cuadro de diálogo **Azure Data Lake Analytics Task Editor** (Editor de la tarea de Azure Data Lake Analytics) para asignar variables a los parámetros (variables U-SQL) en el script de U-SQL.

- **Nombre de variable**: después de agregar una asignación de parámetros haciendo clic en **Agregar**, seleccione en la lista una variable del sistema o definida por el usuario, o bien haga clic en \<**Nueva variable...**> para agregar una nueva variable mediante el cuadro de diálogo **Agregar variable**. **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)  

- **Nombre de parámetro:** proporcione un nombre de variable o de parámetro en el script de U-SQL. Asegúrese de que el nombre del parámetro empieza con el signo @, como @Param1. 

Este es un ejemplo de cómo pasar parámetros al script de U-SQL.

**Script de U-SQL de ejemplo**
```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    TO @out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

En el ejemplo de script anterior, las rutas de acceso de entrada y salida se definen en los parámetros **@in** y **@out**. Los valores de los parámetros **@in** y **@out** en el script de U-SQL se pasan de manera dinámica mediante la configuración de la asignación de parámetros.

|Nombre de variable|Nombre de parámetro|
|-------------|--------------|
|Usuario: Variable1|@in|
|Usuario: Variable2|@out| 

## <a name="expression-page-configuration"></a>Configuración de la página de expresión

Todas las propiedades de la página General se pueden asignar como una expresión de propiedad para permitir la actualización dinámica de la propiedad en tiempo de ejecución. **Temas relacionados:** [Usar expresiones de propiedad en paquetes](../../integration-services/expressions/use-property-expressions-in-packages.md)

## <a name="see-also"></a>Ver también
- [Administrador de conexiones de Azure Data Lake Analytics](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md)
- [Tarea Sistema de archivos de Azure Data Lake Store](../../integration-services/control-flow/azure-data-lake-store-file-system-task.md)
- [Administrador de conexiones de Azure Data Lake Store ](../../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)

