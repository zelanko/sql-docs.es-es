---
title: Crear y administrar una partición remota (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- partitions [Analysis Services], remote
- remote partitions [Analysis Services]
ms.assetid: 4322b5cb-af07-4e79-8ecb-59e1121a9eb8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6c87de5fb72036848088afd2fbfd651be5d7b850
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84536177"
---
# <a name="create-and-manage-a-remote-partition-analysis-services"></a>Crear y administrar una partición remota (Analysis Services)
  Al crear particiones en un grupo de medida, puede configurar una base de datos secundaria en una instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como almacenamiento de partición.  
  
 Las particiones remotas para un cubo (denominado base de datos maestra) se almacenan en una base de datos dedicada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (denominada base de datos secundaria).  
  
 Una base de datos secundaria dedicada puede almacenar particiones remotas para una y solo una base de datos maestra, pero la base de datos maestra puede usar varias bases de datos secundarias, siempre y cuando todas las bases de datos secundarias estén en la misma instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Las dimensiones de una base de datos dedicada a las particiones remotas se crean como dimensiones vinculadas.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para poder crear una partición remota, deben cumplirse las siguientes condiciones:  
  
-   Debe tener una segunda instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y una base de datos dedicada para almacenar las particiones. La base de datos secundaria se usa para un único fin: proporciona almacenamiento para las particiones remotas de una base de datos maestra.  
  
-   Ambas instancias del servidor deben ser de la misma versión. Ambas bases de datos deben ser del mismo nivel funcional.  
  
-   Ambas instancias deben estar configuradas para conexiones TCP. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no admite la creación de particiones remotas mediante el protocolo HTTP.  
  
-   Se debe establecer la configuración de firewall de ambos equipos para que acepten conexiones externas. Para obtener más información sobre la configuración de firewall, vea [Configurar Firewall de Windows para permitir el acceso a Analysis Services](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
-   La cuenta de servicio para la instancia que ejecuta la base de datos maestra debe tener acceso administrativo a la instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Si la cuenta de servicio cambia, debe actualizar los permisos tanto en el servidor como en la base de datos.  
  
-   Debe ser administrador de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en ambos equipos.  
  
-   Debe asegurarse de que el plan de recuperación ante desastres contempla la copia de seguridad y la restauración de las particiones remotas. El uso de particiones remotas puede complicar las operaciones de copia de seguridad y restauración. No olvide probar el plan exhaustivamente para asegurarse de que puede restaurar los datos necesarios.  
  
## <a name="configure-remote-partitions"></a>Configurar particiones remotas  
 Dos equipos independientes que ejecutan una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] son los necesarios para crear una organización de particiones remotas que designe un equipo como servidor maestro y el otro equipo como servidor subordinado.  
  
 En el procedimiento siguiente se da por supuesto que tiene dos instancias de servidor, con una base de datos de cubo implementada en el servidor maestro. En este procedimiento, la base de datos de cubo se denomina db-master. La base de datos de almacenamiento que contiene particiones remotas se denomina db-storage.  
  
 Usará tanto [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] como [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para completar este procedimiento.  
  
> [!NOTE]  
>  Las particiones remotas solo se pueden mezclar con otras particiones remotas. Si va a usar una combinación de particiones locales y remotas, una solución alternativa consiste en crear nuevas particiones que incluyan los datos combinados, eliminando las particiones que ya no use.  
  
#### <a name="specify-valid-server-names-for-cube-deployment-in-ssdt"></a>Especificar nombres de servidor válidos para la implementación del cubo (en SSDT)  
  
1.  En el servidor maestro: en el Explorador de soluciones, haga clic con el botón derecho en el nombre de la solución y seleccione **Propiedades**. En el cuadro de diálogo **Propiedades** , haga clic en **Propiedades de configuración**, haga clic en **Implementación**y, a continuación, haga clic en **Servidor** ; después, establezca el nombre del servidor maestro.  
  
2.  En el servidor subordinado: en el Explorador de soluciones, haga clic con el botón derecho en el nombre de la solución y seleccione **Propiedades**. En el cuadro de diálogo **Propiedades** , haga clic en **Propiedades de configuración**, haga clic en **Implementación**y, a continuación, haga clic en **Servidor** ; después, establezca el nombre del servidor subordinado.  
  
#### <a name="create-and-deploy-a-secondary-database-in-ssdt"></a>Crear e implementar una base de datos secundaria (en SSDT)  
  
1.  En el servidor subordinado: cree un nuevo proyecto de Analysis Services para la base de datos de almacenamiento.  
  
2.  En el servidor subordinado: en el Explorador de soluciones, cree un nuevo origen de datos que apunte a la base de datos de cubo, db-master. Use el proveedor **Proveedor Microsoft OLE DB/OLE DB nativo para Analysis Services 11.0**.  
  
3.  En el servidor subordinado: implemente la solución.  
  
#### <a name="enable-features-in-ssms"></a>Habilitar características (en SSMS)  
  
1.  En el servidor subordinado: en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], haga clic con el botón derecho en la instancia conectada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el Explorador de objetos y seleccione **Propiedades**. Establezca **Feature\LinkToOtherInstanceEnabled** y **Feature\LinkFromOtherInstanceEnabled** en **True**.  
  
2.  En el servidor subordinado: haga clic con el botón derecho en el nombre del servidor en el Explorador de objetos y seleccione **Reiniciar**para reiniciar el servidor.  
  
3.  En el servidor maestro: en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], haga clic con el botón derecho en la instancia conectada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el Explorador de objetos y seleccione **Propiedades**. Establezca **Feature\LinkToOtherInstanceEnabled** y **Feature\LinkFromOtherInstanceEnabled** en **True**.  
  
4.  En el servidor maestro: para reiniciar el servidor, haga clic con el botón derecho en el nombre del servidor en el Explorador de objetos y seleccione **Reiniciar**.  
  
#### <a name="set-the-masterdatasourceid-database-property-on-the-remote-server-in-ssms"></a>Establecer la propiedad de base de datos MasterDataSourceID en el servidor remoto (en SSMS)  
  
1.  En el servidor subordinado: haga clic con el botón derecho en la base de datos de almacenamiento, dB-Storage, seleccione **incluir la base de datos**en el  |  Editor**de**  |  **consultas nuevo**.  
  
2.  Agregue **MasterDataSourceID** al código XMLA y especifique después el identificador de la base de datos de cubo, db-master, como valor. El XMLA debe ser similar a lo siguiente.  
  
    ```  
    <Alter ObjectExpansion="ExpandFull" xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
       <DatabaseID>DB-Storage</DatabaseID>  
    </Object>  
    <ObjectDefinition>  
       <Database xmlns:xsd="http://www.w3.org/2001/XMLSchema" 400"   
          <ID>DB-Storage</ID>  
          <Name>DB-StorageB</Name>  
          <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
          <Language>1033</Language>  
          <Collation>Latin1_General_CI_AS</Collation>  
          <DataSourceImpersonationInfo>  
    <ImpersonationMode>ImpersonateAccount</ImpersonationMode>  
             <Account>*********</Account>  
          </DataSourceImpersonationInfo>  
          <MasterDataSourceID>DB-Master</MasterDataSourceID>  
       </Database>  
    </ObjectDefinition>  
    </Alter>  
    ```  
  
3.  Presione F5 para ejecutar el script.  
  
#### <a name="set-up-the-remote-partition-in-ssdt"></a>Configurar la partición remota (en SSDT)  
  
1.  En el servidor maestro: Abra el cubo en el diseñador de cubos y haga clic en la pestaña **particiones** . Expanda el grupo de medida. Haga clic en **Nueva partición** si el grupo de medida ya está configurado para varias particiones o haga clic en el botón Examinar (. . ) en la columna Origen para editar la partición existente.  
  
2.  En el Asistente para particiones, en **Especificar información de origen**, seleccione la vista del origen de datos y la tabla de hechos originales.  
  
3.  Si se usa un enlace de consultas, proporcione una cláusula WHERE que segmente los datos para la nueva partición que va a crear.  
  
4.  En **Ubicaciones de procesamiento y almacenamiento**, bajo **Procesando ubicación**, elija **Origen de datos remoto de Analysis Services** y haga clic en **Nuevo** para crear un nuevo origen de datos que apunte a la base de datos subordinada, db-storage.  
  
    > [!NOTE]  
    >  Si obtiene un error que indica que el origen de datos no existe en la colección, debe abrir el proyecto de la base de datos de almacenamiento, db-storage, y crear un origen de datos que apunte a la base de datos maestra, db-master.  
  
5.  En el servidor maestro: haga clic con el botón derecho en el nombre del cubo en el Explorador de soluciones, seleccione **Procesar** y procese totalmente el cubo.  
  
## <a name="administering-remote-partitions"></a>Administrar particiones remotas  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite tanto el procesamiento paralelo como el procesamiento secuencial de las particiones remotas. La base de datos maestra, en la que se definieron las particiones, coordina las transacciones entre todas las instancias que participan en el procesamiento de las particiones de un cubo. A continuación se envían informes de procesamiento a todas las instancias que procesaron una partición.  
  
 Un cubo que contenga particiones remotas puede administrarse junto con sus particiones en una sola instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Sin embargo, los metadatos de la partición remota solo se pueden ver y actualizar en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en que se definieron la partición y su cubo primario. La partición remota no se puede ver ni actualizar en la instancia remota de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Aunque las bases de datos dedicadas al almacenamiento de particiones remotas no se exponen a los conjuntos de filas de esquema, las aplicaciones que usan Objetos de administración de análisis (AMO) pueden seguir detectando una base de datos dedicada mediante el uso del comando Discover de XML for Analysis. Cualquier comando CREATE o DELETE que se envíe directamente a una base de datos dedicada mediante un cliente TCP o HTTP se ejecutará correctamente, pero el servidor devolverá una advertencia que indica que la acción puede dañar la base de datos estrechamente administrada.  
  
## <a name="see-also"></a>Consulte también  
 [Particiones &#40;Analysis Services - Datos multidimensionales&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
