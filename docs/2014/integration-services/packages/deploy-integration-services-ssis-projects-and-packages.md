---
title: Implementación de proyectos y paquetes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bea8ce8d-cf63-4257-840a-fc9adceade8c
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bf58e533b46304d4d8833626381e52e86d017404
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37221671"
---
# <a name="deployment-of-projects-and-packages"></a>Implementación de proyectos y paquetes
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] admite dos modelos de implementación, el modelo de implementación del proyecto y el modelo de implementación de paquetes. El modelo de implementación del proyecto le permite implementar sus proyectos en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Para más información sobre la implementación de proyectos en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Implementación de paquetes en el servidor de Integration Services](../deploy-projects-to-integration-services-server.md).  
  
 Para obtener más información acerca del modelo de implementación de paquetes, consulte [la implementación del paquete &#40;SSIS&#41;](legacy-package-deployment-ssis.md).  
  
## <a name="compare-project-deployment-and-package-deployment"></a>Comparar la implementación del proyecto y la implementación de paquetes  
 El tipo de modelo de implementación que elija para un proyecto determina qué opciones de desarrollo y administrativas están disponibles para ese proyecto. En la tabla siguiente se muestran las diferencias y similitudes entre utilizar el modelo de implementación del proyecto y utilizar el modelo de implementación de paquetes.  
  
|Cuando se usa el modelo de implementación del proyecto|Cuando se usa el modelo de implementación de paquetes|  
|---------------------------------------------|---------------------------------------------|  
|Un proyecto es la unidad de implementación.|Un paquete es la unidad de implementación.|  
|Los parámetros se usan para asignar valores a las propiedades del paquete.|Las configuraciones se usan para asignar valores a las propiedades del paquete.|  
|Un proyecto, que contiene paquetes y parámetros, se genera en un archivo de implementación del proyecto (extensión .ispac).|Los paquetes (extensión .dtsx) y las configuraciones (extensión .dtsConfig) se guardan por separado en el sistema de archivos.|  
|Un proyecto, que contiene paquetes y parámetros, se implementa en el catálogo de SSISDB en una instancia de SQL Server.|Los paquetes y las configuraciones se copian en el sistema de archivos en otro equipo. Los paquetes también pueden guardarse en la base de datos MSDB en una instancia de SQL Server.|  
|Se requiere la integración con CLR en el motor de base de datos.|No se requiere la integración con CLR en el motor de base de datos.|  
|Los valores de parámetros específicos del entorno se almacenan en variables de entorno.|Los valores de configuración específicos del entorno se almacenan en archivos de configuración.|  
|Los proyectos y los paquetes del catálogo se pueden validar en el servidor antes de la ejecución. Puede utilizar SQL Server Management Studio, procedimientos almacenados o código administrado para realizar la validación.|Los paquetes se validan inmediatamente antes de la ejecución. También puede validar un paquete con dtExec o con código administrado.|  
|Los paquetes se ejecutan iniciando una ejecución en el motor de base de datos. Se asignan un identificador del proyecto, valores de parámetros explícitos (opcional) y referencias de entorno (opcional) a una ejecución antes de que se inicie.<br /><br /> También puede ejecutar paquetes mediante `dtExec`.|Los paquetes se ejecutan utilizando el `dtExec` y `DTExecUI` utilidades de ejecución. Las configuraciones aplicables se identifican mediante los argumentos del símbolo del sistema (opcional).|  
|Durante la ejecución, los eventos producidos por el paquete se capturan automáticamente y se guardan en el catálogo. Puede consultar estos eventos con las vistas de Transact-SQL.|Durante la ejecución, los eventos producidos por un paquete no se capturan automáticamente. Un proveedor de registro se debe agregar al paquete para capturar eventos.|  
|Los paquetes se ejecutan en un proceso de Windows independiente.|Los paquetes se ejecutan en un proceso de Windows independiente.|  
|Se utiliza el Agente SQL Server para programar la ejecución del paquete.|Se utiliza el Agente SQL Server para programar la ejecución del paquete.|  
  
## <a name="features-of-project-deployment-model"></a>Características del modelo de implementación del proyecto  
 En la tabla siguiente se enumeran las características disponibles en los proyectos desarrollados solo para el modelo de implementación del proyecto.  
  
|Característica|Descripción|  
|-------------|-----------------|  
|Parámetros|Un parámetro especifica los datos que usará un paquete. Puede establecer el ámbito de los parámetros en el nivel de paquete o en el nivel de proyecto con parámetros de paquete y parámetros de proyecto, respectivamente. Los parámetros se pueden usar en expresiones o tareas. Cuando el proyecto se implementa en el catálogo, se puede asignar un valor literal para cada parámetro o utilizar el valor predeterminado que se asignó en tiempo de diseño. En lugar de un valor literal, se puede hacer referencia a una variable de entorno. Los valores de variables de entorno se resuelven en el momento de la ejecución del paquete.|  
|Entornos|Un entorno es un contenedor de variables a las que pueden hacer referencia los proyectos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Cada proyecto puede tener varias referencias de entorno, pero una instancia de ejecución del paquete solo puede hacer referencia a variables de un único entorno. Los entornos permiten organizar los valores que se asignan a un paquete. Por ejemplo, se pueden tener entornos denominados "Dev", "test" y "Production".|  
|Variables de entorno|Una variable de entorno define un valor literal que se puede asignar a un parámetro durante la ejecución del paquete. Para utilizar una variable de entorno, se debe crear una referencia de entorno (en el proyecto que corresponde al entorno que tiene el parámetro), asignar un valor de parámetro al nombre de la variable de entorno y especificar la referencia de entorno correspondiente al configurar una instancia de ejecución.|  
|Catálogo de SSISDB|Todos los objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se almacenan y administran en una instancia de SQL Server en una base de datos denominada catálogo de SSISDB. El catálogo permite utilizar carpetas para organizar los proyectos y los entornos. Cada instancia de SQL Server solo puede tener un catálogo. Cada catálogo puede tener cero o más carpetas. Cada carpeta puede tener cero o más proyectos y cero o más entornos. Una carpeta del catálogo también se puede utilizar como límite para los permisos a objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|Procedimientos almacenados y vistas de catálogo|Se puede utilizar un gran número de procedimientos almacenados y vistas para administrar los objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el catálogo. Por ejemplo, se pueden especificar valores para parámetros y variables de entorno, crear e iniciar ejecuciones y supervisar las operaciones de catálogo. Incluso se puede ver exactamente qué valores usará un paquete antes de que empiece la ejecución.|  
  
## <a name="project-deployment"></a>Implementación del proyecto  
 En el centro del modelo de implementación del proyecto está el archivo de implementación del proyecto (extensión .ispac). El archivo de implementación del proyecto es una unidad autónoma de implementación que incluye solamente la información esencial sobre los paquetes y los parámetros del proyecto. El archivo de implementación del proyecto no captura toda la información contenida en el archivo de proyecto de Integration Services (extensión .dtproj). Por ejemplo, los archivos de texto adicional que se utilizan para escribir notas no se almacenan en el archivo de implementación del proyecto y, por lo tanto, no se implementan en el catálogo.  
  
## <a name="required-tasks"></a>Tareas necesarias  
  
-   [Implementar proyectos en el servidor de Integration Services](../deploy-projects-to-integration-services-server.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Entrada del blog, sobre [consideraciones sobre las estrategias de bifurcación en los proyectos de SSIS](http://go.microsoft.com/fwlink/?LinkId=245739), en mattmasson.com.  
  
## <a name="see-also"></a>Vea también  
 [dtexec (utilidad)](dtexec-utility.md)  
  
  
