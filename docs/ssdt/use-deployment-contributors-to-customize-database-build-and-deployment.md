---
title: Personalización de la compilación e implementación de bases de datos con colaboradores de implementación y compilación | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fe2064bb-e01e-4a12-9f12-a99aa9a5203f
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eddebb20455be6cf257cb40b6568c8cad3994882
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094782"
---
# <a name="customize-database-build-and-deployment-by-using-build-and-deployment-contributors"></a>Personalizar la compilación de bases de datos y la implementación con colaboradores de implementación y compilación
Visual Studio proporciona puntos de extensibilidad que puede utilizar para modificar el comportamiento de las acciones de compilación e implementación de los proyectos de base de datos.  
  
## <a name="available-extensibility-points"></a>Puntos de extensibilidad disponibles  
Puede crear una extensión de los puntos de extensibilidad, como se muestra en la siguiente tabla:  
  
|**Acción**|**Tipo de colaborador**|**Notas**|  
|--------------|------------------------|-------------|  
|Compilar|BuildContributor|Este tipo de extensión se ejecuta al compilar el proyecto de SQL después de que el modelo de proyecto se ha validado por completo. El colaborador de compilación puede tener acceso al modelo completado, además de a todas las propiedades de la Tarea de compilación y cualquier argumento personalizado.|  
|Implementar|DeploymentPlanModifier|Este tipo de extensión se ejecuta al implementar el proyecto de SQL, como parte de la canalización de implementación, después de generar el plan de implementación, pero antes de que este se ejecute. Puede utilizar un DeploymentPlanModifier para modificar el plan de implementación agregando o quitando pasos. Los colaboradores de implementación pueden tener acceso al plan de implementación, a los resultados de la comparación y a modelos de origen y de destino.|  
|Implementar|DeploymentPlanExecutor|Este tipo de extensión se ejecuta cuando el plan de implementación se ejecuta y proporciona acceso de solo lectura al plan de implementación. El DeploymentPlanExectutor realiza las acciones con base en el plan de implementación.|  
  
### <a name="supported-extensibility-scenarios"></a>Escenarios de extensibilidad admitidos  
Puede implementar colaboradores de compilación o de implementación para habilitar los siguientes escenarios de ejemplo:  
  
-   **Generar la documentación de esquema durante la compilación de un proyecto**: para admitir este escenario, se implementa un [BuildContributor](http://msdn.microsoft.com/en-us/library/microsoft.sqlserver.dac.deployment.buildcontributor.aspx) y se invalida el método OnExecute para generar la documentación de esquema. Puede crear un archivo de destino que defina los argumentos predeterminados que controlan si la extensión se ejecuta y para especificar el nombre del archivo de salida.  
  
-   **Generar un informe de diferencias al implementar un proyecto de SQL**: para admitir este escenario, se implementa un [DeploymentPlanExecutor](http://msdn.microsoft.com/en-us/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) que genera el archivo XML al implementar el proyecto de SQL.  
  
-   **Modificar el plan de implementación para cambiar se produce un movimiento de datos**: Para admitir este escenario, se implementa un [DeploymentPlanModifier](http://msdn.microsoft.com/en-us/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) y se efectúa una iteración sobre el plan de implementación. Para cada SqlTableMigrationStep de ese plan, examine el resultado de la comparación para determinar si el paso debe realizarse u omitirse.  
  
-   **Copiar archivos del dacpac generado al implementar un proyecto de SQL**: para admitir este escenario, se implementa un colaborador de implementación y se invalida el método OnEstablishDeploymentConfiguration para especificar qué archivos están marcados como DeploymentExtensionConfiguration por el sistema del proyecto. Estos archivos se deben copiar en la carpeta de resultados y agregar al dacpac generado. También puede modificar el colaborador para fusionar varios archivos en un nuevo archivo que se copia a la carpeta de resultados y se agrega al manifiesto de implementación. Durante la implementación, puede implementar el método OnApplyDeploymentConfiguration para extraer esos archivos del dacpac y prepararlos para usarlos en el método OnExecute.  
  
Además, puede exponer pares personalizados de argumentos de nombre/valor desde su colaborador que se escriben en el archivo de proyecto de base de datos. Puede utilizar estos argumentos para permitir que el colaborador extraiga información de MSBuild o para permitir al usuario final de su colaborador que personalice su comportamiento. Por ejemplo, puede permitir a los usuarios especificar el nombre de un archivo de entrada o de salida.  
  
## <a name="common-tasks"></a>Tareas comunes  
  
|**Tareas comunes**|**Contenido adicional**|  
|--------------------|--------------------------|  
|**Obtenga más información acerca de los puntos de extensibilidad:** puede obtener información acerca de las clases base que se utilizan para implementar colaboradores de compilación y de implementación.|[BuildContributor](http://msdn.microsoft.com/en-us/library/microsoft.sqlserver.dac.deployment.buildcontributor.aspx)<br /><br />[DeploymentContributor](http://msdn.microsoft.com/en-us/library/microsoft.sqlserver.dac.deployment.deploymentcontributor.aspx)|  
|**Crear colaboradores de ejemplo:** aprenda los pasos necesarios para crear un colaborador de compilación o de implementación. Si sigue estos tutoriales, debe:<br /><br />-   Crear un colaborador de compilación que genere un informe que enumera todos los elementos del modelo.<br />-   Crear un colaborador de implementación que cambie el plan de implementación antes de que se ejecute.<br />-   Crear un colaborador de implementación que genere un informe de implementación al implementar un proyecto de SQL.<br /><br />Puede crear todos los colaboradores en un único ensamblado o en varios ensamblados, dependiendo de cómo desee que estén distribuidos los colaboradores en el equipo.|[Tutorial: Ampliar la compilación del proyecto de base de datos para generar estadísticas de modelo](../ssdt/walkthrough-extend-database-project-build-to-generate-model-statistics.md)<br /><br />[Tutorial: Ampliar la implementación del proyecto de base de datos para modificar el plan de implementación](../ssdt/walkthrough-extend-database-project-deployment-to-modify-the-deployment-plan.md)<br /><br />[Tutorial: Ampliar la implementación del proyecto de base de datos para analizar el plan de implementación](../ssdt/walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan.md)|  
  
## <a name="see-also"></a>Ver también  
[Definir condiciones personalizadas para pruebas unitarias de SQL](http://msdn.microsoft.com/en-us/library/jj860449(v=vs.103).aspx)  
  
