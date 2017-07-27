---
title: "Configuración de SQL Server para enviar comentarios a Microsoft | Microsoft Docs"
description: 
author: annashres
ms.author: anshrest
manager: jhubbard
ms.date: 07/12/2017
ms.topic: article
ms.prod: sql-server-2016
ms.technology: database-engine
ms.assetid: 
ms.translationtype: HT
ms.sourcegitcommit: dd279b20fdf0f42d4b44843244aeaf6f19f04718
ms.openlocfilehash: de638f50e6c11633859e7cdc3c6ddb208fe64f00
ms.contentlocale: es-es
ms.lasthandoff: 07/27/2017

---

# <a name="configure-sql-server-to-send-feedback-to-microsoft"></a>Configuración de SQL Server para enviar comentarios a Microsoft

## <a name="summary"></a>Resumen
De forma predeterminada, Microsoft SQL Server recopila información sobre cómo sus clientes usan la aplicación. En concreto, SQL Server recopila información sobre la experiencia de instalación, el uso y el rendimiento. Esta información ayuda a Microsoft a mejorar el producto para satisfacer mejor las necesidades del cliente. Por ejemplo, Microsoft recopila información sobre los tipos de códigos de error que encuentran los clientes para que podamos corregir errores relacionados, mejorar nuestra documentación sobre cómo usar SQL Server y determinar si deben agregarse características al producto para ofrecer un mejor servicio a los clientes.

En concreto, Microsoft no envía ninguno de los tipos de información siguientes a través de este mecanismo:
- Valores de dentro de las tablas de usuario
- Credenciales de inicio de sesión u otra información de autenticación
- Información de identificación personal (PII)

En el escenario de ejemplo siguiente se incluye información de uso de características que ayuda a mejorar el producto.

SQL Server 2017 admite índices de almacén de columnas para habilitar escenarios de análisis rápido. Los índices de almacén de columnas combinan una estructura de los índices “árbol B” tradicional para datos recién insertados con una estructura comprimida orientada a columnas especial para comprimir datos y acelerar la ejecución de consultas. El producto contiene heurística para migrar datos desde la estructura de árbol B hasta la estructura comprimida en el fondo, lo que acelera, por tanto, los resultados de la consulta futuros.

Si la operación en segundo plano no va al compás de la velocidad de inserción de los datos, el rendimiento de las consultas puede ser más lento de lo esperado. Para mejorar el producto, Microsoft recopila información sobre lo bien que SQL Server sigue el ritmo del proceso de compresión de datos automático. El equipo del producto usa esta información para ajustar la frecuencia y el paralelismo del código que realiza la compresión. Esta consulta se ejecuta de forma ocasional para recopilar esta información a fin de que nosotros, Microsoft, podamos evaluar la velocidad de movimiento de los datos. Esto nos ayuda a optimizar la heurística del producto.  

```sql
SELECT object_id, type_desc, data_space_id, db_id() AS database_id FROM sys.indexes WITH(nolock) WHERE type = 5 or type = 6 
```

```sql
SELECT cntr_value as merge_policy_evaluation
FROM sys.dm_os_performance_counters WITH(nolock)
WHERE object_name LIKE '%columnstore%' 
AND counter_name ='Total Merge Policy Evaluations' 
AND instance_name = '_Total'
```

Tenga en cuenta que este proceso se centra en los mecanismos necesarios para entregar valor a los clientes. El equipo del producto no examina los datos del índice ni envía dichos datos a Microsoft. SQL Server 2017 siempre recopila y envía información sobre la experiencia de instalación del proceso de configuración para que podamos encontrar y corregir con rapidez cualquier problema de instalación que experimente el cliente. SQL Server 2017 se puede configurar para que no se envíe información (por instancia por servidor) a Microsoft a través de los mecanismos siguientes:
- Mediante el uso de la aplicación Informes de uso y errores
- Mediante el establecimiento de subclaves del Registro en el servidor

Para SQL Server en Linux, consulte [Customer Feedback for SQL Server on Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-customer-feedback.md) (Comentarios del usuario para SQL Server en Linux)

> [!NOTE]
> Puede deshabilitar el envío de información a Microsoft solo en versiones de pago de SQL Server.

## <a name="error-and-usage-reporting-application"></a>Aplicación Informes de uso y errores 

Tras la instalación, la configuración de recopilación de datos de uso para componentes e instancias de SQL Server se puede cambiar a través de la aplicación Informes de uso y errores. Esta aplicación está disponible como parte de la instalación de SQL Server. Esta herramienta permite a cada instancia de SQL Server establecer su propia configuración Datos de uso.

> [!NOTE]
> La aplicación Informes de uso y errores se incluye en las herramientas de configuración de SQL Server. Puede usar esta herramienta para administrar su preferencia por la recopilación de comentarios de uso e informes de error de la misma forma que en SQL Server 2017. Los informes de error son independientes de la recopilación de comentarios de uso, de modo que pueden activarse o desactivarse independientemente de la recopilación de comentarios de uso. Los informes de errores recopilan volcados de memoria que se envían a Microsoft y que pueden contener información confidencial, como se describe en la declaración de privacidad.

Para iniciar Informes de uso y errores de SQL Server, haga clic o pulse **Iniciar** y, a continuación, busque en "Error" en el cuadro de búsqueda. Se mostrará el elemento Informes de uso y errores de SQL Server. Tras iniciar la herramienta, puede administrar comentarios de uso y errores graves que se recopilan para instancias y componentes instalados en ese equipo.

Para las versiones de pago, use las casillas “Informes de uso” para administrar el envío de comentarios de uso a Microsoft.

Para las versiones de pago o gratuitas, use las casillas “Informes de error” para administrar el envío de comentarios sobre errores graves y volcados de memoria a Microsoft.

## <a name="set-registry-subkeys-on-the-server"></a>Establecer subclaves del Registro en el servidor

Los clientes empresariales pueden establecer la configuración de directiva de grupo para participar o no en la recopilación de datos de uso. Esto se hace configurando una directiva basada en el Registro. La subclave del Registro y la configuración necesarias son:

- Para las características de instancia de SQL Server:
    
    Subclave = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{InstanceID}\CPE
    
    Nombre EntradaRegistro = CustomerFeedback
    
    Tipo de entrada DWORD: 0 para no utilizar el CEIP; 1 para utilizarlo
    
    {InstanceID} hace referencia al tipo de instancia y a la instancia, como en los ejemplos siguientes:

    - MSSQL14.CANBERRA para motor de base de datos SQL Server 2017 y nombre de instancia de "CANBERRA"
    - MSAS14.CANBERRA para SQL Server 2017 Analysis Services y nombre de instancia de "CANBERRA"
    - MSRS14.CANBERRA para SQL Server 2017 Reporting Services y nombre de instancia de "CANBERRA"

- Para todas las características compartidas:
    
    Subclave = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{Major Version}
    
    Nombre EntradaRegistro = CustomerFeedback
    
    Tipo de entrada DWORD: 0 para no utilizar el CEIP; 1 para utilizarlo

> [!NOTE]
> {Major Version} hace referencia a la versión de SQL Server (por ejemplo, 140 para SQL Server 2017).

- Para SQL Server Management Studio:
  
    Subclave = HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\140

    Nombre EntradaRegistro = CustomerFeedback

    Tipo de entrada DWORD: 0 para no utilizar el CEIP; 1 para utilizarlo

Además, para desactivar lnformes de uso y errores en el nivel de Visual Studio, establezca las siguientes subclave del Registro y configuración:

-    Subclave = HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\Telemetry

-    Nombre EntradaRegistro = TurnOffSwitch

-    Tipo de entrada DWORD: 0 para no utilizar el CEIP; 1 para utilizarlo
 
La recopilación de datos de uso de SQL Server 2017 respeta la directiva de grupo basada en el Registro sobre estas subclaves del Registro.

## <a name="set-registry-subkeys-for-crash-dump-collection"></a>Establecer subclaves del Registro para la recopilación de volcados de memoria

De forma similar al comportamiento en una versión anterior de SQL Server, los clientes de SQL Server 2017 Enterprise pueden establecer la configuración de directivas de grupo en el servidor para participar o no en la recopilación de volcados de memoria. Esto se hace configurando una directiva basada en el Registro. Las claves del Registro y la configuración necesarias son: 

- Para las características de instancia de SQL Server:

    Subclave = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{InstanceID}\CPE

    Nombre EntradaRegistro = EnableErrorReporting

    Tipo de entrada DWORD: 0 para no utilizar el CEIP; 1 para utilizarlo
 
    {InstanceID} hace referencia al tipo de instancia y a la instancia, como en los ejemplos siguientes: 

    - MSSQL14.CANBERRA para motor de base de datos SQL Server 2017 y nombre de instancia de "CANBERRA"
    - MSAS14.CANBERRA para SQL Server 2017 Analysis Services y nombre de instancia de "CANBERRA"
    - MSRS14.CANBERRA para SQL Server 2017 Reporting Services y nombre de instancia de "CANBERRA"
 

- Para todas las características compartidas:
    
    Subclave = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{Major Version}

    Nombre EntradaRegistro = EnableErrorReporting

    Tipo de entrada DWORD: 0 para no utilizar el CEIP; 1 para utilizarlo

> [!NOTE]
> {Major Version} hace referencia a la versión de SQL Server. Por ejemplo, "140" hace referencia a SQL Server 2017.

La recopilación de volcados de memoria de SQL Server 2017 respeta la directiva de grupo basada en el Registro sobre estas subclaves del Registro. 

## <a name="crash-dump-collection-for-ssms"></a>Recopilación de volcados de memoria para SSMS
SSMS no recopila su propio volcado de memoria. Cualquier volcado de memoria relativo a SSMS se recopila como parte de Informe de errores de Windows.

El procedimiento para activar o desactivar esta característica depende de la versión del SO. Para activar o desactivar la característica, siga los pasos en el artículo adecuado para su versión de Windows.
 
- Windows Server 2016 y Windows 10

    [Configurar la telemetría de Windows en la organización](https://technet.microsoft.com/en-us/itpro/windows/manage/configure-windows-telemetry-in-your-organization)
- Windows Server 2008 R2 y Windows 7

    [WER Settings](https://msdn.microsoft.com/en-us/library/windows/desktop/bb513638(v=vs.85).aspx) (Configuración de WER)
 
## <a name="feedback-for-analysis-services"></a>Comentarios sobre Analysis Services

Durante la instalación, SQL Server 2016 Analysis Services agrega una cuenta especial a su instancia de Analysis Services. Esta cuenta es miembro del rol de administrador del servidor de Analysis Services. La cuenta se usa para recopilar información de comentarios de la instancia de Analysis Services.  

Puede configurar su servicio para que no se envíen datos de uso, tal como se describe en la sección "Establecer subclaves del Registro en el servidor". Sin embargo, al hacer esto no se quita la cuenta de servicio. 
 

