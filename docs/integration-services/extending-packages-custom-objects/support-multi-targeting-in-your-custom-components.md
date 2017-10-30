---
title: "Compatibilidad con múltiples versiones de los componentes personalizados | Documentos de Microsoft"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016)
ms.assetid: ec611374-16bf-4a56-8fd9-45d3ddd7befc
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: dc111f1d884a3553156b55ab490afef2f8df9d61
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="support-multi-targeting-in-your-custom-components"></a>Compatible con múltiples versiones de los componentes personalizados
 Ahora puede usar el Diseñador SSIS en SQL Server Data Tools (SSDT) para crear, mantener y ejecutar paquetes de ese destino SQL Server 2016, SQL Server 2014 o SQL Server 2012. Para obtener SSDT para Visual Studio 2015, consulte [descargar Latest SQL Server Data Tools](../../ssdt/download-sql-server-data-tools-ssdt.md). 

 En el Explorador de soluciones, haga clic con el botón derecho en un proyecto de Integration Services y seleccione **Propiedades** para abrir las páginas de propiedades del proyecto. En la pestaña **General** de **Propiedades de configuración**, seleccione la propiedad **TargetServerVersion** y luego elija SQL Server 2016, SQL Server 2014 o SQL Server 2012.  
   
 ![Propiedad TargetServerVersion en el cuadro de diálogo de propiedades de proyecto](../../integration-services/media/targetserverversion2.png "TargetServerVersion propiedad en el cuadro de diálogo de propiedades de proyecto")  
 
 ## <a name="multiple-version-support-and-multi-targeting-for-custom-components"></a>Varios compatibilidad de versiones y compatibilidad con múltiples versiones de componentes personalizados
 
Todos los cinco tipos de extensiones personalizadas SSIS admiten compatibilidad con múltiples versiones.
-   Administradores de conexión
-   Tareas
-   Enumeradores
-   Proveedores de registro
-   Componentes de flujo de datos

Las extensiones administradas, el Diseñador SSIS carga la versión de la extensión para la versión de destino especificado. Por ejemplo:
-   Cuando la versión de destino es SQL Server 2012, el diseñador carga la versión de 2012 de la extensión.
-   Cuando la versión de destino es SQL Server 2016, el diseñador carga la versión de la extensión de 2016.

Extensiones de COM no son compatibles con la compatibilidad con múltiples versiones. El Diseñador SSIS carga siempre la extensión de COM para la versión actual de SQL Server, independientemente de la versión de destino especificado.

## <a name="add-basic-support-for-multiple-versions-and-multi-targeting"></a>Agregar la compatibilidad básica para varias versiones y compatibilidad con múltiples versiones

Para obtener instrucciones básicas, consulte [obtener sus extensiones personalizadas de SSIS que deben admitir la compatibilidad con varias versiones de 2015 de SSDT para SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/). Esta entrada de blog describe los siguientes pasos o requisitos.

-   Implementar los ensamblados en las carpetas adecuadas.

-   Cree un archivo de asignación de extensión para SQL Server 2014 y versiones alta.

## <a name="add-code-to-switch-versions"></a>Agregue código para cambiar las versiones

### <a name="switch-versions-in-a-custom-connection-manager-task-enumerator-or-log-provider"></a>Versiones de conmutador en un administrador de conexiones personalizado, la tarea, el enumerador o el proveedor de registro

Para un administrador de conexiones personalizado, tarea, enumerador o proveedor de registro, agregar lógica de degradación en el **SaveToXML** método.

```csharp
public void SaveToXML(XmlDocument doc, IDTSInfoEvents events)
{
    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
    }

    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2012)
    {
         // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
    }
}
```

### <a name="switch-versions-in-a-custom-data-flow-component"></a>Versiones de conmutador en un componente de flujo de datos personalizados

Para un administrador de conexiones personalizado, tarea, enumerador o proveedor de registro, agregar lógica de degradación en el nuevo **PerformDowngrade** método.

```csharp
public override void PerformDowngrade(int pipelineVersion, DTSTargetServerVersion targetServerVersion)
{
    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
        ComponentMetaData.Version = 8;
    }

    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2012)
    {
          // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
        ComponentMetaData.Version = 6;
    }
}
```

## <a name="common-errors"></a>Errores comunes

### <a name="invalidcastexception"></a>InvalidCastException

**Mensaje de error.** No se puede convertir el objeto COM de tipo 'System.__ComObject' para la interfaz de tipo 'Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100'. La operación falló debido a un error de la llamada de QueryInterface en el componente COM para la interfaz con IID '{BE8C48A3-155B-4810-BA5C-BDF68A659E9E}' debido al siguiente error: No se admite dicha interfaz (excepción de HRESULT: 0 x 80004002 (E_NOINTERFACE)). (Microsoft.SqlServer.DTSPipelineWrap).

**Solución.** Si la extensión personalizada hace referencia a ensamblados de interoperabilidad de SSIS, como Microsoft.SqlServer.DTSPipelineWrap o Microsoft.SqlServer.DTSRuntimeWrap, establezca el valor de la **incrustar tipos de interoperabilidad** propiedad ** False ".

![Incrustar tipos de interoperabilidad](../../integration-services/extending-packages-custom-objects/media/embed-interop-types.png)

### <a name="unable-to-load-some-types-when-target-version-is-sql-server-2012"></a>No se pueden cargar algunos tipos cuando la versión de destino es SQL Server 2012

Este problema afecta a determinados tipos, como IErrorReportingService o IUserPromptService.

**Mensaje de error (ejemplo).** No se pudo cargar el tipo 'Microsoft.DataWarehouse.Design.IErrorReportingService' del ensamblado ' Microsoft.DataWarehouse, Version = 13.0.0.0, Culture = neutral, PublicKeyToken = 89845dcd8080cc91'.

**Solución alternativa.** Use un cuadro de mensajes en lugar de estas interfaces cuando la versión de destino es SQL Server 2012.


