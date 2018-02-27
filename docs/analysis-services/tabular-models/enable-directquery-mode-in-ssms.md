---
title: Habilitar el modo DirectQuery en SSMS | Documentos de Microsoft
ms.custom: 
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a5d439a9-5be1-4145-90e8-90777d80e98b
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 544725a89521eb86f61fcfd3194c3d56be9da606
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
---
# <a name="enable-directquery-mode-in-ssms"></a>Habilitar el modo DirectQuery en SSMS
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Puede cambiar las propiedades de acceso a datos de un modelo tabular que ya se haya implementado y habilitar de esta forma el modo DirectQuery. De esta forma, las consultas se ejecutarán en un origen de datos relacionales de back-end, en lugar de ejecutarse en datos en caché que residen en memoria.  
  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], los pasos de configuración de DirectQuery varían en función del nivel de compatibilidad del modelo. A continuación encontrará unos pasos que funcionan con todos los niveles de compatibilidad.  
  
 Este artículo se supone que ha creado y ha validado un modelo tabular en memoria en el nivel de compatibilidad 1200 o superior y solo es necesario para habilitar el acceso DirectQuery y actualizar las cadenas de conexión. Si empieza desde un nivel de compatibilidad inferior, primero necesitará actualizarlo de forma manual. Vea los pasos en [Actualizar Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) .  
  
> [!IMPORTANT]  
>  Se recomienda utilizar [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] en lugar de Management Studio para cambiar de modo de almacenamiento de datos. Si se utiliza  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para cambiar el modelo y, después, prosigue con la implementación en el servidor, el modelo y la base de datos permanecerán sincronizados. Además, al cambiar de modos de almacenamiento en el modelo, podrá revisar los errores de validación que se produzcan. Si se usa [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] como se describe en este artículo, los errores de validación no se notifican.  
  
## <a name="requirements"></a>Requisitos  
 La habilitación del uso del modo DirectQuery en un modelo tabular es un proceso compuesto de varias fases:  
  
-   Asegúrese de que el modelo no tiene características que pudieran provocar errores de validación en el modo DirectQuery y, después, cambie el modo de almacenamiento de datos en el modelo de en memoria a DirectQuery.  
  
     Una lista de restricciones de características se documenta en [Directquerymode](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).  
  
-   Revise la cadena de conexión y las credenciales que utiliza la base de datos implementada para recuperar datos de la base de datos back-end externa. Asegúrese de que solo hay una conexión y de que su configuración es adecuada para la ejecución de consultas.  
  
     Las bases de datos tabulares que no fueran diseñadas específicamente para DirectQuery podrían contar con diversas conexiones, que ahora deben reducirse a una, tal y como requiere el modo DirectQuery.  
  
     Las credenciales utilizadas originalmente para el procesamiento de datos se usarán ahora para realizar consultas en los datos. Como parte de la configuración de DirectQuery, revise y, en caso de proceder, cambie la cuenta si usa otras distintas para las operaciones específicas.  
  
     El modo DirectQuery representa el único escenario en el que Analysis Services realiza la delegación de confianza. Si su solución requiere delegación para obtener resultados de consulta específicos de los usuarios, la cuenta utilizada para conectarse a la base de datos back-end debe tener permiso para delegar la identidad del usuario que realiza la solicitud. Además, las identidades de usuarios deben disponer de permisos de lectura en dicha base de datos.  
  
-   Como último paso, confirme que el modo DirectQuery se encuentra operativo mediante la ejecución de una consulta.  
  
## <a name="step-1-check-the-compatibility-level"></a>Paso1: comprobación del nivel de compatibilidad  
 Las propiedades que definen el acceso a datos son varían según el nivel de compatibilidad. Como paso preliminar, compruebe qué nivel de compatibilidad presenta la base de datos.  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], conéctese a la instancia que contenga el modelo tabular.  
  
2.  En el Explorador de objetos, haga clic con el botón derecho en la base de datos > **Propiedades** > **Nivel de compatibilidad**.  
  
     El valor será **SQL Server 2016 (1200)** o un nivel anterior, como **SQL Server 2012 SP1 o versiones posteriores (1103)**. En el siguiente paso, siga las instrucciones aplicables al nivel de compatibilidad concreto.  
  
 Cuando se cambia un modelo tabular al modo DirectQuery, el nuevo modo de almacenamiento de datos se aplica de inmediato.  
  
## <a name="step-2a-switch-a-tabular-1200-database-to-directquery-mode"></a>Paso 2a: Cambiar una base de datos tabular 1200 al modo DirectQuery  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la base de datos > **Propiedades** > **Modelo** > **Modo predeterminado**.  
  
2.  Establezca el modo en **DirectQuery**.  
  
    |||  
    |-|-|  
    |**Valores válidos**|**Description**|  
    |**DirectQuery**|Las consultas se ejecutan en una base de datos relacional back-end mediante la conexión de origen de datos definida para el modelo.<br /><br /> Las consultas del modelo se convierten en consultas de bases de datos nativas y se redirigen al origen de datos.<br /><br /> Al procesar un modelo establecido en el modo DirectQuery, solo se compilan e implementan los metadatos. Los datos en sí son externos al modelo y residen en los archivos de base de datos del origen de datos operativo.|  
    |**Importar**|Las consultas se ejecutan en la base de datos tabular en MDX o DAX.<br /><br /> Al procesar un modelo establecido en el modo de importación, los datos se recuperan desde un origen de datos back-end y se almacenan en disco. Cuando haya cargado la base de datos, los datos se copian por completo en la memoria para ofrecer consultas y recorridos de tabla muy rápidos.<br /><br /> Este es el modo predeterminado de los modelos tabulares y es el único modo para determinados orígenes de datos (no relacionales).|  
  
## <a name="step-2b-switch-a-tabular-1100-1103-database-to-directquery-mode"></a>Paso 2b: Cambiar una base de datos tabular 1100-1103 al modo DirectQuery  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la base de datos > **Propiedades** > **Base de datos** > **DirectQueryMode**.  
  
2.  Establezca el modo en **DirectQuery**.  
  
     Estas son las propiedades predeterminadas del modo:  
  
    |||  
    |-|-|  
    |**Valores válidos**|**Description**|  
    |**InMemory**|Las consultas utilizan únicamente los datos en memoria almacenados en caché.|  
    |**InMemorywithDirectQuery**|Las consultas usan la memoria caché de forma predeterminada, a menos que se especifique lo contrario en la cadena de conexión desde el cliente.<br /><br /> Se trata de un modo híbrido en el que las particiones se configuran por separado para usar en memoria o DirectQuery.|  
    |**DirectQuery**|Las consultas solo usan el origen de datos relacional.|  
    |**DirectQuerywithInMemory**|Las consultas usan el origen de datos relacional de forma predeterminada, a menos que se especifique lo contrario en la cadena de conexión desde el cliente.<br /><br /> Se trata de un modo híbrido en el que las particiones se configuran por separado para usar en memoria o DirectQuery.|  
  
 **Almacenamiento de datos híbrido**  
  
 Cuando se utiliza una combinación de acceso basado en disco y en memoria, la memoria caché sigue estando disponible y puede utilizarse para las consultas. Un modo híbrido le ofrece muchas opciones:  
  
-   Si tanto la memoria caché como el origen de datos relacional están disponibles, puede establecer el método de conexión preferido, pero será el cliente el que en última instancia decida el origen que se utilizará, mediante la propiedad de cadena de conexión DirectQueryMode.  
  
-   Puede configurar particiones en la memoria caché de tal manera que la partición principal utilizada para el modo DirectQuery no se procese nunca y deba hacer siempre referencia al origen relacional. Hay muchas maneras de utilizar particiones para optimizar el diseño del modelo y la creación de informes. Para obtener más información, consulte [definir particiones en los modelos DirectQuery](../../analysis-services/tabular-models/define-partitions-in-directquery-models-ssas-tabular.md).  
  
-   Una vez implementado el modelo, puede cambiar el método de conexión preferido. Por ejemplo, puede utilizar un modo híbrido para las pruebas, y cambiar el modelo a **Solo DirectQuery** únicamente después de probar exhaustivamente los informes o las consultas utilizadas por este. Para más información, vea [Establecer o cambiar el método de conexión preferido para DirectQuery](http://msdn.microsoft.com/library/f10d5678-d678-4251-8cce-4e30cfe15751).  
  
## <a name="step-3-check-the-connection-properties-on-the-database"></a>Paso 3: comprobación de las propiedades de conexión en la base de datos  
 Según la configuración de la conexión de origen de datos, si cambia a DirectQuery, es posible que se modifique el contexto de seguridad de la conexión. Al cambiar el modo de acceso de datos, consulte las propiedades de la cadena de conexión y la suplantación a fin de comprobar que el inicio de sesión sea válido para las conexiones salientes a la base de datos back-end.  
  
 Consulte la sección **Configurar Analysis Services para la delegación de confianza** de [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md) para obtener información general sobre la delegación de una identidad de usuario para escenarios de DirectQuery.  
  
1.  En el Explorador de objetos, expanda **Conexiones** y haga doble clic en una conexión para ver sus propiedades.  
  
     Para los modelos DirectQuery, solo debe haber una conexión definida para la base de datos; por su parte, el origen de datos debe ser relacional y de un tipo de base de datos compatible. Vea [orígenes de datos admitidos](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md).  
  
2.  En**Cadena de conexión** se debe especificar el servidor, nombre de la base de datos y el método de autenticación utilizado en las operaciones de DirectQuery. Si utiliza la autenticación de SQL Server, puede especificar aquí el inicio de sesión de base de datos.  
  
3.  **Información de suplantación** se utiliza para la autenticación de Windows. Entre las opciones válidas para los modelos tabulares en el modo DirectQuery se incluyen las siguientes:  
  
    -   **Utilizar la cuenta de servicio**. Puede seleccionar esta opción si la cuenta de servicio de Analysis Services dispone de permisos de lectura en la base de datos relacional.  
  
    -   **Usar un nombre de usuario y contraseña específicos**. Especifique una cuenta de usuario de Windows que tenga permisos de lectura en la base de datos relacional.  
  
 Tenga en cuenta que estas credenciales solo se utilizan para responder a las consultas en el almacén de datos relacional; no son las mismas que se usan para procesar la memoria caché de un modelo híbrido.  
  
 No se puede utilizar la suplantación si el modelo solo se usa en la memoria. El valor **ImpersonateCurrentUser**no es válido a menos que el modelo utilice el modo DirectQuery.  
  
## <a name="step-4-validate-directquery-access"></a>Paso 4: validación del acceso DirectQuery  
  
1.  Inicie un seguimiento mediante SQL Server Profiler o XEvents en Management Studio, conectado a la base de datos relacional de SQL Server.  
  
     Si usa Oracle o Teradata, utilice las herramientas de seguimiento de esas plataformas de base de datos.  
  
2.  En Management Studio, escriba y ejecute una consulta MDX simple, como `select <some measure> on 0 from model.`.  
  
3.  En el seguimiento, debería ver pruebas de la ejecución de la consulta en la base de datos relacional.  
  
## <a name="see-also"></a>Vea también  
 [Nivel de compatibilidad](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Orígenes de datos admitidos](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)   
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)   
 [Supervisar una instancia de Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)  
  
  
