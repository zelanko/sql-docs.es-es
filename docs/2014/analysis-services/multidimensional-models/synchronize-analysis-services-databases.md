---
title: Sincronizar bases de datos de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services deployments, Synchronize Database Wizard
- deploying [Analysis Services], Synchronize Database Wizard
- Synchronize Database Wizard
- synchronization [Analysis Services]
ms.assetid: 6aeff68d-8470-43fb-a3ed-a4b9685332c2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a561b348b30afcbfe5305681f56e4f8314fa510
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66072851"
---
# <a name="synchronize-analysis-services-databases"></a>Sincronizar bases de datos de Analysis Services
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluye una característica de sincronización de bases de datos hace que dos bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sean equivalentes; para ello, copia los datos y los metadatos de una base de datos de un servidor de origen en una base de datos de un servidor de destino. Use la característica Sincronizar base de datos para realizar cualquiera de las tareas siguientes:  
  
-   Implementar una base de datos de un servidor de ensayo en un servidor de producción.  
  
-   Actualizar una base de datos de un servidor de producción con los cambios realizados en los datos y metadatos de una base de datos de un servidor de ensayo.  
  
-   Generar un script XMLA que se pueda ejecutar a en el futuro para sincronizar las bases de datos.  
  
-   En las cargas de trabajo distribuidas donde se procesan los cubos y las dimensiones de varios servidores, use la sincronización de base de datos para combinar los cambios en una sola base de datos.  
  
 La sincronización de base de datos se inicia en el servidor de destino, extrayendo datos y metadatos en una copia de la base de datos del servidor de origen. Si la base de datos no existe, se creará. La sincronización es una operación única unidireccional que concluye una vez copiada la base de datos. No proporciona paridad en tiempo real entre las bases de datos.  
  
 Puede volver a sincronizar las bases de datos que ya existen en los servidores de origen y de destino para extraer los cambios más recientes de un servidor de ensayo en una base de datos de producción. Se comparan los archivos de los dos servidores para ver si hay cambios y se actualizan los que sean diferentes. Una base de datos existente en un servidor de destino sigue estando disponible mientras se realiza la sincronización en segundo plano. Los usuarios pueden seguir consultando la base de datos de destino mientras la sincronización está en curso. Una vez finalizada la sincronización, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cambia automáticamente los usuarios a los datos y metadatos recién copiados y quita los datos antiguos de la base de datos de destino.  
  
 Para sincronizar bases de datos, ejecute el Asistente para sincronizar bases de datos si desea sincronizar inmediatamente las bases de datos o úselo para generar un script de sincronización que puede ejecutar más adelante. Se puede usar cualquier enfoque para aumentar la disponibilidad y escalabilidad de las bases de datos y el cubo de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
> [!NOTE]  
>  Las notas del producto siguientes, escritas para versiones anteriores de Analysis Services, siguen siendo aplicables a las soluciones multidimensionales escalables compiladas con SQL Server 2012. Para obtener más información, vea [Scale-Out Querying with Analysis Services](https://go.microsoft.com/fwlink/?LinkId=253136) (Consulta de escalado horizontal con Analysis Services) y [Scale-Out Querying for Analysis Services with Read-Only Databases](https://go.microsoft.com/fwlink/?LinkId=253137.)(Consulta de escalado horizontal con Analysis Services con bases de datos de solo lectura).  
  
## <a name="prerequisites"></a>Requisitos previos  
 En el servidor de destino (o destino) desde el que se inicia la sincronización de base de datos, debe ser miembro del rol de administrador del servidor de Analysis Services. En el servidor de origen, su cuenta de usuario de Windows debe tener permisos Control total en la base de datos de origen. Si va a sincronizar la base de datos de forma interactiva, recuerde que la sincronización se ejecuta en el contexto de seguridad de su identidad de usuario de Windows. Si su cuenta tiene denegado el acceso a determinados objetos, esos objetos se excluirán de la operación. Para obtener más información acerca de los roles de administrador de servidor y los permisos de base de datos, vea [conceder permisos de administrador de servidor &#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md) y [conceder permisos de base de datos &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md).  
  
 El puerto TCP 2383 debe estar abierto en ambos servidores para permitir conexiones remotas entre las instancias predeterminadas. Para obtener más información sobre cómo crear una excepción en Firewall de Windows, vea [Configure the Windows Firewall to Allow Analysis Services Access](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
 Tanto el servidor de origen como el de destino deben tener la misma versión y Service Pack. Dado que los metadatos del modelo también están sincronizados, para garantizar la compatibilidad, el número de compilación de ambos servidores debe ser el mismo. La edición de cada instalación debe admitir la sincronización de base de datos. En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], la sincronización de base de datos se admite en las ediciones Enterprise, Developer y Business Intelligence. Para obtener más información sobre las características de cada edición, vea [características compatibles con las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 El modo de implementación del servidor debe ser idéntico en cada servidor. Si la base de datos que va a sincronizar es multidimensional, los servidores de origen y de destino deben estar configurados para el modo de servidor multidimensional. Para obtener más información acerca de los modos de implementación, vea [Determine the Server Mode of an Analysis Services Instance](../instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 Desactive el procesamiento diferido de agregaciones si lo está usando en el servidor de origen. Las agregaciones que se están procesando en segundo plano pueden interferir con la sincronización de base de datos. Para obtener más información acerca de la configuración de esta propiedad del servidor, vea [OLAP Properties](../server-properties/olap-properties.md).  
  
> [!NOTE]  
>  El tamaño de la base de datos es un factor que se debe tener en cuenta a la hora de determinar si la sincronización es un método adecuado. No existen requisitos generales, pero si la sincronización es demasiado lento, considere la posibilidad de sincronizar varios servidores en paralelo, como se describe en estas notas del producto: [Procedimientos recomendados para la sincronización de Analysis Services](https://go.microsoft.com/fwlink/?LinkID=253136).  
  
## <a name="synchronize-database-wizard"></a>Asistente para sincronizar bases de datos  
 Use el Asistente para sincronizar bases de datos con el fin de realizar una sincronización unidireccional desde una base de datos de origen a una de destino o para generar un script que especifique una operación de sincronización de base de datos. Puede sincronizar tanto particiones locales como remotas durante el proceso de sincronización y elegir si desea incluir roles.  
  
 El Asistente para sincronizar bases de datos le guía por los siguientes pasos:  
  
-   Seleccionar la instancia y la base de datos de origen desde la que desea realizar la sincronización.  
  
-   Seleccionar las ubicaciones de almacenamiento para las particiones locales en la instancia de destino.  
  
-   Seleccionar las ubicaciones de almacenamiento para las particiones remotas en otras instancias de destino.  
  
-   Seleccionar el nivel de seguridad e información de pertenencia para copiar desde la instancia de origen y la base de datos a la instancia de destino.  
  
-   Seleccionar entre sincronizar inmediatamente o guardar el comando **Sincronizar** de XML for Analysis (XMLA) generado por el Asistente para sincronizar bases de datos en un archivo de script para realizar una sincronización posterior.  
  
 De forma predeterminada, el asistente sincroniza todos los datos y metadatos, excepto los miembros de los grupos de seguridad existentes. También puede copiar u omitir toda la configuración de seguridad al sincronizar los datos y los metadatos.  
  
#### <a name="run-the-wizard"></a>Ejecutar el asistente  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que ejecutará la base de datos de destino. Por ejemplo, si va a implementar una base de datos en un servidor de producción, ejecutaría el asistente en el servidor de producción.  
  
2.  En el Explorador de objetos, haga clic con el botón derecho en la carpeta **Bases de datos** y, después, haga clic en **Sincronizar**.  
  
3.  Especifique el servidor de origen y la base de datos de origen. En la página Seleccione la base de datos que se va a sincronizar, en **Servidor de origen** y **Base de datos de origen**, escriba el nombre del servidor de origen y la base de datos de origen. Por ejemplo, si va a realizar la implementación desde un entorno de prueba en un servidor de producción, el origen es la base de datos del servidor de ensayo.  
  
     **Servidor de destino** muestra el nombre de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con la que se sincronizan los datos y metadatos de la base de datos seleccionada en **Base de datos de origen** .  
  
     La sincronización se llevará a cabo para las bases de datos de origen y de destino que tengan el mismo nombre. Si el servidor de destino ya tiene una base de datos que tiene el mismo nombre que la base de datos de origen, la base de datos de destino se actualizará con los metadatos y los datos de origen. Si no existe la base de datos, se creará en el servidor de destino.  
  
4.  Opcionalmente, cambie la ubicación de la partición local. Use la página **Especificar ubicaciones para particiones locales** para indicar dónde se deben almacenar las particiones locales en el servidor de destino.  
  
    > [!NOTE]  
    >  Esta página solo aparecerá si existe al menos una partición local en la base de datos especificada.  
  
     Si se instala un conjunto de particiones en la unidad C del servidor de origen, el asistente le permitirá copiar este conjunto de particiones en otra ubicación del servidor de destino. Si no cambia las ubicaciones predeterminadas, el asistente implementará las particiones del grupo de medida de cada cubo del servidor de origen en las mismas ubicaciones del servidor de destino. Del mismo modo, si el servidor de origen usa particiones remotas, se usarán las mismas particiones remotas en el servidor de destino.  
  
     En la opción **Ubicaciones** aparece una cuadrícula con la carpeta de origen, la carpeta de destino y el tamaño estimado de las particiones locales que se almacenarán en la instancia de destino. La cuadrícula contiene las columnas siguientes:  
  
     **Carpeta de origen**  
     Muestra el nombre de carpeta de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de origen que incluye la partición local. Si la columna incluye el valor "(Default)", la ubicación predeterminada de la instancia de origen incluirá la partición local.  
  
     **Carpeta de destino**  
     Muestra el nombre de carpeta de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de destino en la que se sincronizará la partición local. Si la columna incluye el valor "(Default)", la ubicación predeterminada de la instancia de destino incluirá la partición local.  
  
     Haga clic en el botón de puntos suspensivos (**…**) para que aparezca el cuadro de diálogo **Buscar carpeta remota** y especifique una carpeta en la instancia de destino en la que se deben sincronizar las particiones locales almacenadas en la ubicación seleccionada.  
  
    > [!NOTE]  
    >  Esta columna no se puede cambiar para las particiones locales almacenadas en la ubicación predeterminada para la instancia de origen.  
  
     **Tamaño**  
     Muestra el tamaño estimado de la partición local.  
  
     En **Particiones en la ubicación seleccionada** se muestra una cuadrícula en la que se describen las particiones locales almacenadas en la ubicación de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de origen especificada en la columna **Carpeta de origen** de la fila seleccionada en **Ubicaciones**.  
  
     **BD**  
     Muestra el nombre del cubo que contiene la partición.  
  
     **Grupo de medida**  
     Muestra el nombre del grupo de medida del cubo que contiene la partición.  
  
     **Nombre de la partición**  
     Muestra el nombre de la partición.  
  
     **Tamaño (Mb)**  
     Muestra el tamaño de la partición en megabytes (MB).  
  
5.  Opcionalmente, cambie la ubicación de las particiones remotas. Use la página **Especificar ubicaciones para particiones remotas** para indicar si se deben sincronizar las particiones remotas administradas por la base de datos especificada del servidor de origen, y para especificar una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y una base de datos de destino donde se deben almacenar las particiones remotas seleccionadas.  
  
    > [!NOTE]  
    >  Esta página solo aparece si hay al menos una partición remota administrada por la base de datos especificada en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de origen.  
  
     La opción **Ubicaciones** muestra una cuadrícula con detalles acerca de las ubicaciones en las que se almacenan las particiones remotas para la base de datos de origen, incluida la información de origen y destino y el tamaño de almacenamiento que usa cada ubicación, disponible en la base de datos seleccionada. La cuadrícula contiene las columnas siguientes:  
  
     **Sincronizar**  
     Seleccione esta opción para incluir una ubicación que incluye las particiones remotas durante la sincronización.  
  
    > [!NOTE]  
    >  Si no se selecciona esta opción para una ubicación, no se sincronizarán las particiones remotas incluidas en la misma.  
  
     **Servidor de origen**  
     Muestra el nombre de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que incluye las particiones remotas.  
  
     **Carpeta de origen**  
     Muestra el nombre de carpeta de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que incluye las particiones remotas. Si la columna incluye el valor "(Default)", la ubicación predeterminada de la instancia mostrada en **Servidor de origen** incluirá las particiones remotas.  
  
     **Servidor de destino**  
     Muestra el nombre de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se deben sincronizar las particiones remotas almacenadas en la ubicación especificada en **Servidor de origen** y **Carpeta de origen** .  
  
     Haga clic en el botón de puntos suspensivos (**…**) para que aparezca el cuadro de diálogo **Administrador de conexiones** y especifique una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se deben sincronizar las particiones remotas almacenadas en la ubicación seleccionada.  
  
     **Carpeta de destino**  
     Muestra el nombre de carpeta de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de destino en la que se sincronizará la partición remota. Si la columna incluye el valor "(Default)", la ubicación predeterminada de la instancia de destino incluirá la partición remota.  
  
     Haga clic en el botón de puntos suspensivos (**…**) para que aparezca el cuadro de diálogo **Buscar carpeta remota** y especifique una carpeta en la instancia de destino en la que se deben sincronizar las particiones remotas almacenadas en la ubicación seleccionada.  
  
     **Tamaño**  
     Muestra el tamaño estimado de las particiones remotas almacenadas en la ubicación.  
  
     En **Particiones en la ubicación seleccionada** se muestra una cuadrícula en la que se describen las particiones remotas almacenadas en la ubicación de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de origen especificada en la columna **Carpeta de origen** de la fila seleccionada en **Ubicaciones**. La cuadrícula contiene las columnas siguientes:  
  
     **BD**  
     Muestra el nombre del cubo que contiene la partición.  
  
     **Grupo de medida**  
     Muestra el nombre del grupo de medida del cubo que contiene la partición.  
  
     **Nombre de la partición**  
     Muestra el nombre de la partición.  
  
     **Tamaño (Mb)**  
     Muestra el tamaño de la partición en megabytes (MB).  
  
6.  Especifique si se debe incluir la información de permisos de usuario y si se debe usar compresión. De forma predeterminada, el asistente comprime todos los datos y metadatos antes de copiar los archivos al servidor de destino. Esta opción da como resultado una transmisión de archivos más rápida. Los archivos se descomprimen una vez que llegan al servidor de destino.  
  
     **Copiar todo**  
     Seleccione esta opción para incluir las definiciones de seguridad y la información acerca de los miembros durante la sincronización.  
  
     **Omitir pertenencia**  
     Seleccione esta opción para incluir las definiciones de seguridad pero excluir la información acerca de los miembros durante la sincronización.  
  
     **Omitir todo**  
     Seleccione esta opción para omitir la definición de seguridad y la información de pertenencia actuales de la base de datos de origen. Si se crea una base de datos de destino durante la sincronización, no se copiará ninguna definición de seguridad ni ninguna información de pertenencia. Si la base de datos de destino ya existe y tiene roles y pertenencias, la información de seguridad se conservará.  
  
7.  Elija el método de sincronización. Puede realizar la sincronización inmediatamente o generar un script que se guarda en un archivo. De forma predeterminada, el archivo se guarda con una extensión .xmla y se coloca en la carpeta Documentos.  
  
8.  Haga clic en **Finalizar** para sincronizar. Tras comprobar las opciones de la página **Finalización del asistente** , haga clic de nuevo en **Finalizar** .  
  
## <a name="next-steps"></a>Pasos a seguir  
 Si no sincronizó los roles o la pertenencia, recuerde especificar los permisos de acceso de usuario ahora en la base de datos de destino.  
  
## <a name="see-also"></a>Consulte también  
 [Elemento Synchronize &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)   
 [Implementar soluciones de modelo mediante XMLA](deploy-model-solutions-using-xmla.md)   
 [Implementar soluciones con el Asistente para la implementación](deploy-model-solutions-using-the-deployment-wizard.md)  
  
  
