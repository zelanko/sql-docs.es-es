---
title: Cmdlet Set-PowerPivotSystemService | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: f6ef197b-3d74-4339-ae73-8a7c1eaf0e91
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6157a4fc3b43c1a7dad7805c3efa5677d85b4d66
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-powerpivotsystemservice-cmdlet"></a>Cmdlet Set-PowerPivotSystemService
  
  [!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]
  
  Establece las propiedades globales del objeto PowerPivotSystemService en el nivel de granja.  

>[!NOTE] 
>En este artículo puede contener información no actualizada y ejemplos. Use el cmdlet Get-Help para la versión más reciente.
  
 **Se aplica a:** SharePoint 2010 y SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
Set-PowerPivotSystemService [-Identity <PowerPivotMidTierServicePipeBind>] [-UpdateAssemblyInformation <switch>] [-WorkbookUpgradeOnDataRefresh <boolean>] [-DirectTCPConnections <boolean>] [-Confirm <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 El cmdlet Set-PowerPivotSystemService actualiza las propiedades del objeto primario del Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la granja.  
  
## <a name="parameters"></a>Parámetros  
  
### <a name="-identity-powerpivotmidtierservicepipebind"></a>-Identity \<PowerPivotMidTierServicePipeBind >  
 Especifica el objeto primario para el que desea actualizar las propiedades. El valor debe ser un GUID válido que identifique de forma única el objeto en la granja.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|true|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-updateassemblyinformation-switch"></a>-UpdateAssemblyInformation \<cambiar >  
 Se usa solo para la actualización. Si la versión del ensamblado implementado en la granja es distinta de la versión que se almacena en la base de datos de configuración de SharePoint, puede ejecutar este cmdlet para actualizar la información de ensamblado en la base de datos de configuración. La información de versión del ensamblado está disponible en las propiedades del archivo de Microsoft.AnalysisServices.SharePoint.Integration.dll que se almacena en el ensamblado global.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|1|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-workbookupgradeondatarefresh-boolean"></a>-WorkbookUpgradeOnDataRefresh \<booleano >  
 Se usa para actualizar automáticamente un libro de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] al inicio de una actualización de datos programada en el servidor. La actualización de datos solo se admite para los libros que coincidan con la versión actual del servidor. Si habilita esta propiedad, el libro se actualizará automáticamente para que la actualización de datos pueda continuar. Esta propiedad se establece en el nivel de instancia del servidor. No puede variarla para libros, bibliotecas, sitios o usuarios específicos.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|2|  
|Valor predeterminado|false|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-directtcpconnections-boolean"></a>-DirectTCPConnections \<booleano >  
 Especifica que Excel Services envía todas las consultas directamente a la instancia de SQL Server Analysis Services (POWERPIVOT) que cargó una base de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , omitiendo el transporte del proveedor de datos y del canal MSOLAP que se usa en caso contrario para cada solicitud de consulta enviada a una base de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Al establecer este parámetro, se mejora el rendimiento y la escalabilidad de las consultas de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] al hacer que las conexiones a las bases de datos cargadas sean más eficaces. Observe que este parámetro no cambia el comportamiento del modo en que se asigna la solicitud de carga inicial. Otros parámetros, como –RoundRobinAllocation y –HealthBasedAllocation, que se usan para asignar las solicitudes de carga de base de datos entre varias instancias de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint en la granja no se ven afectados, porque –DirectTCPConnections solo se aplica a las consultas que se ejecutan después de cargar la base de datos.  
  
 En las topologías de granja de servidores que incluyen Excel Services y [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint en ejecución en servidores de aplicaciones independientes, debe abrir un puerto en el firewall para asegurarse de que las solicitudes llegan a la instancia de SQL Server Analysis Services (POWERPIVOT). Para obtener instrucciones sobre cómo habilitar las conexiones entrantes para una instancia con nombre de Analysis Services, vea [Configurar Firewall de Windows para permitir el acceso a Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|3|  
|Valor predeterminado|false|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-confirm-switch"></a>-Confirme \<cambiar >  
 Le solicita confirmación antes de ejecutar el comando. Este valor se habilita de forma predeterminada. Para omitir la respuesta de confirmación de un comando, especifique Confirm:$false en el comando.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet admite parámetros comunes: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable,OutBuffer y OutVariable. Para obtener más información, vea [about_Commonparameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas y salidas  
 El tipo de entrada es el tipo de objetos que se pueden canalizar al cmdlet. El tipo de valor devuelto es el tipo de objeto que el cmdlet devuelve.  
  
|||  
|-|-|  
|Entradas|Ninguno.|  
|Salidas|Ninguno.|  
  
## <a name="example-1"></a>Ejemplo 1  
  
```  
C:\PS>Set-PowerPivotSystemService -WorkbookUpgradeOnDataRefresh:$true  
```  
  
 Habilita la actualización automática de los libros de la versión anterior de modo que la actualización de datos programada pueda continuar.  
  
  

