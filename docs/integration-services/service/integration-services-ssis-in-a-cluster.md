---
title: "Integration Services (SSIS) en un clúster | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: service
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0216266d-d866-4ea2-bbeb-955965f4d7c2
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 52fb4e913a48b65544aaca84408f847af74412be
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-ssis-in-a-cluster"></a>Integration Services (SSIS) en un clúster
  No se recomienda la agrupación en clústeres de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] porque el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no es un servicio en clúster o que reconozca clústeres, y no admite la conmutación por error de un nodo de clúster a otro. Por consiguiente, en un entorno en clúster, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se debería instalar e iniciar como un servicio independiente en cada nodo del clúster.  
  
 Aunque el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no es un servicio de clúster, puede configurar manualmente el servicio para que funcione como un recurso de clúster después de instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] por separado en cada nodo del clúster.  
  
 Sin embargo, si la alta disponibilidad es su objetivo a la hora de establecer un entorno de hardware en clúster, puede lograr este objetivo sin configurar el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como recurso de clúster.  Para administrar los paquetes de cualquier nodo del clúster desde cualquier nodo del clúster, modifique el archivo de configuración del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en cada nodo del clúster. Debe modificar cada uno de estos archivos de configuración de forma que indique todas las instancias disponibles de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en las que se guardan paquetes. Esta solución proporciona la alta disponibilidad que necesitan la mayoría de los clientes, sin los posibles problemas que se producen cuando el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se configura como un recurso de clúster. Para más información sobre cómo modificar el archivo de configuración, vea [Integration Services Service &#40;SSIS Service&#41;](../../integration-services/service/integration-services-service-ssis-service.md) (Servicio Integration Services [servicio SSIS]).  
  
 Entender el rol del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es esencial para tomar una decisión informada sobre cómo configurar el servicio en un entorno en clúster. Para más información, vea [Servicio Integration Services &#40;servicio SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
## <a name="disadvantages"></a>Inconvenientes
 A continuación se describen algunos de los posibles inconvenientes de configurar el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como recurso de clúster:  
  
-   **Cuando se produce una conmutación por error, los paquetes en ejecución no se reinician.**
    
    Puede recuperarse de los errores de paquete reiniciando los paquetes desde los puntos de comprobación. Puede reiniciar desde los puntos de comprobación sin configurar el servicio como recurso de clúster. Para obtener más información, vea [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
-   Al configurar el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un grupo de recursos distinto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no puede utilizar [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] desde los equipos cliente para administrar los paquetes almacenados en la base de datos msdb. El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no puede delegar las credenciales en este escenario de salto doble.  
  
-   Si tiene varios grupos de recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un clúster, una conmutación por error podría producir resultados inesperados. Considere el escenario siguiente. Grupo 1, que contiene el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , se está ejecutando en Nodo A. Grupo 2, que también contiene el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , se está ejecutando en Nodo B. Grupo 2 conmuta por error a Nodo A. El intento de iniciar otra instancia del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en Nodo A produce un error porque el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es un servicio de instancia única. El servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está intentando la conmutación por error a Nodo A también producirá un error en función de la configuración del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en Grupo 2. Si el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se había configurado para afectar a los demás servicios del grupo de recursos, se producirá un error en el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está creando la conmutación por error porque se ha producido un error en el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Si el servicio se había configurado para no afectar a los demás servicios del grupo de recursos, el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podrá realizar conmutación por error al Nodo A. A menos que el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en Grupo 2 estuviera configurado para no afectar a los demás servicios del grupo de recursos, el error del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que está conmutando por error podría hacer que el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está conmutando por error también produjera un error.  

## <a name="configure-the-service-as-a-cluster-resource"></a>Configuración del servicio como un recurso de clúster
Para los clientes que decidan que las ventajas de configurar el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como un recurso de clúster son más que los inconvenientes, esta sección contiene las instrucciones de configuración necesarias. Sin embargo, [!INCLUDE[msCoName](../../includes/msconame-md.md)] no recomienda que el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se configure como un recurso de clúster.  
  
 Para configurar el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como recurso de clúster, es necesario completar las siguientes tareas.  
  
-   Instale [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un clúster.  
  
     Para instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un clúster, debe instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en cada nodo del clúster.  
  
-   Configure [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como un recurso de clúster.  
  
     Con Integration Services instalado en cada nodo del clúster, debe configurar Integration Services como un recurso de clúster. Al configurar el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como un recurso de clúster, puede agregar el servicio al mismo grupo de recursos que [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]o a otro grupo. En la tabla siguiente se describen las posibles ventajas e inconvenientes de seleccionar un grupo de recursos.  
  
    |Cuando Integration Services y SQL Server están en el mismo grupo de recursos|Cuando Integration Services y SQL Server están en distintos grupos de recursos|  
    |-----------------------------------------------------------------------------|-------------------------------------------------------------------------------|  
    |Los equipos cliente pueden utilizar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para administrar los paquetes almacenados en la base de datos msdb porque [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se están ejecutando en el mismo servidor virtual. Esta configuración evita los problemas de delegación del escenario de salto doble.|Los equipos cliente no pueden usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para administrar los paquetes almacenados en la base de datos msdb. El cliente se puede conectar al servidor virtual en el que se está ejecutando el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Sin embargo, dicho equipo no puede delegar las credenciales del usuario al servidor virtual en el que se está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esto se denomina escenario de salto doble.|  
    |El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] compite con otros servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por el uso de la CPU y de otros recursos informáticos.|El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no compite con otros servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por el uso de la CPU y de otros recursos informáticos porque los distintos grupos de recursos se configuran en nodos diferentes.|  
    |La carga y almacenamiento de los paquetes en la base de datos msdb son más rápidos y generan menos tráfico de red porque ambos servicios se ejecutan en el mismo equipo.|Puede ocurrir que la carga y el almacenamiento de los paquetes en la base de datos msdb sean procesos más lentos y generen más tráfico de red.|  
    |Ambos servicios están en línea o sin conexión al mismo tiempo.|El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] podría estar en línea mientras [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] está sin conexión. De esta forma, los paquetes almacenados en la base de datos msdb de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] no están disponibles.|  
    |El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no se puede mover rápidamente a otro nodo, si es necesario.|El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se puede mover rápidamente a otro nodo, si es necesario.|  
  
     Después de haber decidido a qué grupo de recursos agregará [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], es necesario que configure [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como un recurso de clúster en ese grupo.  
  
-   Configure el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y el almacén de paquetes.  
  
     Cuando haya configurado [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como un recurso de clúster, debe modificar la ubicación y el contenido del archivo de configuración para el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en cada nodo del clúster. Estas modificaciones hacen que el archivo de configuración y el almacén de paquetes estén disponibles para todos los nodos si se produce una conmutación por error. Cuando haya modificado la ubicación y el contenido del archivo de configuración, debe volver a poner el servicio en línea.  
  
-   Establezca en línea el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como recurso de clúster.  
  
 Después de configurar el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en un clúster, o en cualquier servidor, es posible que necesite configurar permisos DCOM para poder conectarse a dicho servicio desde un equipo cliente. Para más información, vea [Servicio Integration Services &#40;servicio SSIS&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
 El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no puede delegar credenciales. Por ello, no puede utilizar [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para administrar los paquetes almacenados en la base de datos msdb cuando se dan las condiciones siguientes:  
  
-   Los servicios [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se están ejecutando en servidores independientes o en servidores virtuales.  
  
-   El cliente que está ejecutando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] es un tercer equipo.  
  
 El cliente se puede conectar al servidor virtual en el que se está ejecutando el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Sin embargo, dicho equipo no puede delegar las credenciales del usuario al servidor virtual en el que se está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esto se denomina escenario de salto doble.  
  
### <a name="to-install-integration-services-on-a-cluster"></a>Para instalar Integration Services en un clúster  
  
1.  Instale y configure un clúster con uno o varios nodos.  
  
2.  (Opcional) Instale servicios de clúster, como [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
3.  Instale [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en cada nodo del clúster.  
  
### <a name="to-configure-integration-services-as-a-cluster-resource"></a>Para configurar Integration Services como un recurso de clúster  
  
1.  Abra el **Administrador de clústeres**.  
  
2.  En el árbol de consola, seleccione la carpeta Grupos.  
  
3.  En el panel de resultados, seleccione el grupo al que desea agregar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
    -   Para agregar Integrations Services como un recurso de clúster al mismo grupo de recursos que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione el grupo al que pertenece [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Para agregar Integrations Services como un recurso de clúster a un grupo distinto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione un grupo distinto del grupo al que pertenece [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
4.  En el menú **Archivo** , seleccione **Nuevo**y, a continuación, haga clic en **Recurso**.  
  
5.  En la página **Nuevo recurso** del **Resource Wizard** (Asistente para recursos), escriba un nombre y elija **Servicio genérico**como tipo de servicio. No cambie el valor de **Group**(Grupo). Haga clic en **Siguiente**.  
  
6.  En la página **Possible Owners** (Posibles propietarios), agregue o quite los nodos del clúster como posibles propietarios del recurso. Haga clic en **Siguiente**.  
  
7.  Para agregar dependencias, en la página **Dependencias** , seleccione un recurso en **Recursos disponibles**y, a continuación, haga clic en **Agregar**. En caso de una conmutación por error, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el disco compartido que almacena los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] deberían volver a ponerse en línea antes de que se conecte [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Cuando haya seleccionado las dependencias, haga clic en **Siguiente**.  
  
     Para más información, consulte [Add Dependencies to a SQL Server Resource](../../sql-server/failover-clusters/windows/add-dependencies-to-a-sql-server-resource.md).  
  
8.  En la página **Generic Service Parameters** (Parámetros de servicio genéricos), especifique **MsDtsServer** como nombre del servicio. Haga clic en **Siguiente**.  
  
9. En la página **Replicación de Registro** , haga clic en **Agregar** para agregar la clave del Registro que identifica la ubicación del archivo de configuración para el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Este archivo debe estar ubicado en un disco compartido que esté en el mismo grupo de recursos que el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
10. En el cuadro de diálogo **Clave del Registro** , escriba **SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile**. Haga clic en **Aceptar**y, a continuación, en **Finalizar**.  
  
     El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se ha agregado como recurso de clúster.  
  
### <a name="to-configure-the-integration-services-service-and-package-store"></a>Para configurar el servicio Integration Services y el almacén de paquetes  
  
1.  Busque el archivo de configuración en %Archivos de programa%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.ini.xml. Copie el archivo en el disco compartido del grupo al que agregó el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  En el disco compartido, cree una nueva carpeta denominada **Packages** para que sea el almacén de paquetes. Conceda permisos de escritura y de carpetas de listas en la nueva carpeta a los grupos y usuarios que corresponda.  
  
3.  En el disco compartido, abra el archivo de configuración en un editor XML o de texto. Cambie el valor del elemento **ServerName** por el nombre del equipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] virtual que está en el mismo grupo de recursos.  
  
4.  Cambie el valor del elemento **StorePath** a la ruta de acceso completa de la carpeta **Packages** creada en el disco compartido en un paso anterior.  
  
5.  Actualice el valor de **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile** en el Registro a la ruta de acceso completa y el nombre de archivo del archivo de configuración del servicio en el disco compartido.  
  
### <a name="to-bring-the-integration-services-service-online"></a>Poner en línea el servicio Integration Services  
  
-   En el **Administrador de clústeres**, seleccione el servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , haga clic con el botón derecho y seleccione **Poner en línea** en el menú emergente. El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está en línea ahora como recurso de clúster.  
  
  
